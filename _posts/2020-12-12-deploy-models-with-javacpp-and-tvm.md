---
layout: post
title: Optimize and deploy models with JavaCPP and TVM
---

In the AI industry, the Java platform is used mainly when deploying to production. Consequently, it makes sense to provide easy access to all the tools and frameworks necessary to deploy deep learning models for Java. However, one of the most widely used frameworks, [Apache TVM](https://tvm.apache.org/), did not have very good support for Java, until recently. With the [JavaCPP Presets for TVM](https://github.com/bytedeco/javacpp-presets/tree/master/tvm), we now have proper support for the Java platform.

Still, according to the [GitHub repository of TVM](https://github.com/apache/tvm), over 50% of the code is written in Python. This means that, for most use cases, we probably need to run some of those modules as part of the deployment pipeline. Moreover, there are usually preprocessing algorithms among other things that have been implemented only as Python scripts. For these reasons, we might as well make it easy as possible to execute this Python code from Java. This is where the [JavaCPP Presets for CPython](https://github.com/bytedeco/javacpp-presets/tree/master/cpython), [LLVM](https://github.com/bytedeco/javacpp-presets/tree/master/llvm), [MKL](https://github.com/bytedeco/javacpp-presets/tree/master/mkl), [oneDNN (aka DNNL, MKL-DNN)](https://github.com/bytedeco/javacpp-presets/tree/master/dnnl), [OpenBLAS](https://github.com/bytedeco/javacpp-presets/tree/master/openblas), [NumPy](https://github.com/bytedeco/javacpp-presets/tree/master/numpy), and [SciPy](https://github.com/bytedeco/javacpp-presets/tree/master/scipy) come in. They are available as normal JAR files, which can be used as any other JAR files, but they can also be used to satisfy the dependencies of TVM---without having to install anything! For example, as shown in the following sample project for OpenCV, we can bundle everything with [GraalVM Native Image](https://www.graalvm.org/reference-manual/native-image/) as usual and it simply just works as expected with [Quarkus](https://quarkus.io/):

 * [https://github.com/bytedeco/sample-projects/tree/master/opencv-stitching-native](https://github.com/bytedeco/sample-projects/tree/master/opencv-stitching-native)

### Importing and optimizing a model

For the moment though, let us return to the focus of this post: Importing, optimizing, and deploying deep learning models with TVM in Java. One of the most recent and important breakthrough in the industry is the transformer architecture and models based on it such as BERT, for which TVM has been shown to deliver the highest performance, at least on CPU: [Speed up your BERT inference by 3x on CPUs using Apache TVM](https://medium.com/apache-mxnet/speed-up-your-bert-inference-by-3x-on-cpus-using-apache-tvm-9cf7776cd7f8). We can embed, for example, the whole [`optimize_bert.py` script](https://gist.github.com/icemelon9/860d3d2c9566d6f69fa8112840dd95c1) as is in Java as demonstrated in this example, which also contains all the code found in this post:

 * [https://github.com/bytedeco/javacpp-presets/blob/master/tvm/samples/DeployBERT.java](https://github.com/bytedeco/javacpp-presets/blob/master/tvm/samples/DeployBERT.java)

This script essentially imports a BERT model from GluonNLP and compares its performance with MXNet, but [TVM also supports models in Keras, TensorFlow, ONNX, PyTorch, etc formats](https://tvm.apache.org/docs/tutorials/index.html#compile-deep-learning-models). In any case, to run that kind of script, we need to install all those Python packages first. This is where JavaCPP can help. With only these 3 lines of code, we are installing everything we need in JavaCPP's cache, outside of any system or other user directories, so nothing gets broken, and the process is fully reproducible:

```java
// Extract to JavaCPP's cache CPython and obtain the path to the executable file
String python = Loader.load(org.bytedeco.cpython.python.class);

// Install in JavaCPP's cache GluonNLP and MXNet to download and import BERT model
new ProcessBuilder(python, "-m", "pip", "install", "gluonnlp", "mxnet", "pytest").inheritIO().start().waitFor();

// Add TVM and its dependencies to Python path using C API to embed script in Java
Py_AddPath(org.bytedeco.tvm.presets.tvm.cachePackages());
```

That makes it possible to execute the example successfully with a single Maven command and nothing more than a functional installation of the JDK, with everything getting downloaded, mainly from the Maven Central Repository and PyPI:
```bash
mvn clean compile exec:java -Djavacpp.platform.host -Dexec.mainClass=DeployBERT
```
This outputs relevant information such as the following for an Intel(R) Xeon(R) Gold 6126 CPU @ 2.60GHz with 12 cores:
```
MXNet latency for batch 1 and seq length 128: 57.88 ms
TVM latency for batch 1 and seq length 128: 22.45 ms
Running BERT runtime...
[ 0.06691778, 0.8569598 ]
```

### <br>Deploying the model

The above takes care of importing and optimizing models, but to achieve lower latency and/or higher throughput, we often need to perform inference without the additional overhead and restrictions of CPython. For this reason, after importing them, TVM can "export" models to native libraries. In this case, the DeployBERT example contains the following additional Python code to export the BERT model into a library named `libbert.so`:

```python
# Export the model to a native library
with tvm.transform.PassContext(opt_level=3, required_pass=["FastMath"]):
    compiled_lib = relay.build(mod, "llvm -libs=mkl", params=params)
compiled_lib.export_library("lib/libbert.so")
```

Once we have this native library, we are freed from the shackles of CPython. We can load and run inference on the model, where performance matters most, using only native code, plus (in our case) Java code based on the C/C++ API of the TVM runtime, which for our `libbert.so` looks like this:

```java
// load in the library
DLContext ctx = new DLContext().device_type(kDLCPU).device_id(0);
Module mod_factory = Module.LoadFromFile("lib/libbert.so");
// create the BERT runtime module
TVMValue values = new TVMValue(2);
IntPointer codes = new IntPointer(2);
TVMArgsSetter setter = new TVMArgsSetter(values, codes);
setter.apply(0, ctx);
TVMRetValue rv = new TVMRetValue();
mod_factory.GetFunction("default").CallPacked(new TVMArgs(values, codes, 1), rv);
Module gmod = rv.asModule();
PackedFunc set_input = gmod.GetFunction("set_input");
PackedFunc get_output = gmod.GetFunction("get_output");
PackedFunc run = gmod.GetFunction("run");

// Use the C++ API to create some random sequence
int batch = 1, seq_length = 128;
DLDataType dtype = new DLDataType().code((byte)kDLFloat).bits((byte)32).lanes((short)1);
NDArray inputs = NDArray.Empty(new long[]{batch, seq_length}, dtype, ctx);
NDArray token_types = NDArray.Empty(new long[]{batch, seq_length}, dtype, ctx);
NDArray valid_length = NDArray.Empty(new long[]{batch}, dtype, ctx);
NDArray output = NDArray.Empty(new long[]{batch, 2}, dtype, ctx);
FloatPointer inputs_data = new FloatPointer(inputs.accessDLTensor().data()).capacity(batch * seq_length);
FloatPointer token_types_data = new FloatPointer(token_types.accessDLTensor().data()).capacity(batch * seq_length);
FloatPointer valid_length_data = new FloatPointer(valid_length.accessDLTensor().data()).capacity(batch);
FloatPointer output_data = new FloatPointer(output.accessDLTensor().data()).capacity(batch * 2);
FloatIndexer inputs_idx = FloatIndexer.create(inputs_data, new long[]{batch, seq_length});
FloatIndexer token_types_idx = FloatIndexer.create(token_types_data, new long[]{batch, seq_length});
FloatIndexer valid_length_idx = FloatIndexer.create(valid_length_data, new long[]{batch});
FloatIndexer output_idx = FloatIndexer.create(output_data, new long[]{batch, 2});

Random random = new Random();
for (int i = 0; i < batch; ++i) {
    for (int j = 0; j < seq_length; ++j) {
        inputs_idx.put(i, j, random.nextInt(2000));
        token_types_idx.put(i, j, random.nextFloat());
    }
    valid_length_idx.put(i, seq_length);
}

// set the right input
setter.apply(0, new BytePointer("data0"));
setter.apply(1, inputs);
set_input.CallPacked(new TVMArgs(values, codes, 2), rv);
setter.apply(0, new BytePointer("data1"));
setter.apply(1, token_types);
set_input.CallPacked(new TVMArgs(values, codes, 2), rv);
setter.apply(0, new BytePointer("data2"));
setter.apply(1, valid_length);
set_input.CallPacked(new TVMArgs(values, codes, 2), rv);
// run the code
run.CallPacked(new TVMArgs(values, codes, 0), rv);
// get the output
setter.apply(0, 0);
setter.apply(1, output);
get_output.CallPacked(new TVMArgs(values, codes, 2), rv);
```

We can of course implement a high-level API on top of all this to simplify the usage, as with the official Java API called [TVM4J](https://github.com/apache/tvm/tree/main/jvm), which also comes bundled with the presets, so that works out of the box too, but it is quite limited and not always practical. Whichever API we use though, it should be clear that all the hard work can be done from the Java platform, in a portable and reproducible fashion, without having to install or build anything manually on the system.

For CUDA on GPUs, we can also do something similar with the [JavaCPP Presets for TensorRT](https://github.com/bytedeco/javacpp-presets/tree/master/tensorrt), so be sure to check out this API as well along with the sample code written in Java:

 * [https://github.com/bytedeco/javacpp-presets/blob/master/tensorrt/samples/SampleGoogleNet.java](https://github.com/bytedeco/javacpp-presets/blob/master/tensorrt/samples/SampleGoogleNet.java)


If you are having any issues with the code or would like to talk more about this subject, please feel free to communicate via the [mailing list from Google Groups](http://groups.google.com/group/javacpp-project), [discussions on GitHub](https://github.com/bytedeco/javacpp/discussions), or [the chat room at Gitter](https://gitter.im/bytedeco/javacpp). Happy New Year!
