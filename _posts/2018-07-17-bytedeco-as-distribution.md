---
layout: post
title: Bytedeco as a distribution
---

With version 1.4.2 now released, it's time to publish a small blog post introducing the main innovations. As everyone probably knows, we've also released version 1.4.1 back in March. Thanks to the CI servers at [AppVeyor](https://www.appveyor.com/) and [Travis CI](https://www.travis-ci.org/), we are now able to produce full releases of all binaries without too much effort, so we will probably be maintaining a release cycle of about 3 months. This brings Bytedeco one step closer to a distribution such as Anaconda, Fedora, or Ubuntu, but cross-platform and for multiple languages (that is being able to access native libraries from other languages than C++), where the presets for [OpenCV](https://opencv.org/) and [TensorFlow](https://www.tensorflow.org/), for example, now also bundle the official Java APIs, but still provide users with access to the C/C++ APIs as well as additional features for better integration. [`PointerScope`](http://bytedeco.org/javacpp/apidocs/org/bytedeco/javacpp/PointerScope.html) is one such new feature that can help manage native memory, even when using multiple different APIs together.

Until now, to prevent garbage from hanging around too long in memory, we had to call manually `Pointer.deallocate()` on all native objects (either directly or with try-with-resources statements). We can now use a `PointerScope` to manage a group of such objects, which is similar to [workspaces in Deeplearning4j](https://deeplearning4j.org/workspaces) (but without the workspace memory) or [`Scope` from Panama](http://cr.openjdk.java.net/~jrose/panama/panama-status-2015-1216.pdf), and as exemplified below for OpenCV and TensorFlow, a single `PointerScope` works even across libraries:

```java
    static void checkStatus(Status s) {
        if (!s.ok()) {
            throw new RuntimeException(s.error_message().getString());
        }
    }

    static void detectObjects(File file, Session session) throws Exception {
        // load the image file
        Mat mat = imread(file.getCanonicalPath());
        if (mat == null || mat.empty()) return;
        cvtColor(mat, mat, CV_BGR2RGB);
        Tensor tensor = new Tensor(DT_UINT8,
            new TensorShape(1, mat.rows(), mat.cols(), mat.channels()),
            mat.arrayData().capacity(mat.arraySize()));

        // run inference
        String[] inputNames = {"image_tensor"};
        Tensor[] inputTensors = {tensor};
        String[] outputNames = {"detection_boxes", "detection_scores", "detection_classes", "num_detections"};
        TensorVector outputTensors = new TensorVector();
        checkStatus(session.Run(new StringTensorPairVector(inputNames, inputTensors),
                new StringVector(outputNames), new StringVector(), outputTensors));

        // do something with outputTensors...
    }

    public static void main(String args[]) throws Exception {
        // read the model
        GraphDef graph = new GraphDef();
        checkStatus(ReadBinaryProto(Env.Default(), "/path/to/frozen_inference_graph.pb", graph));

        // create the session
        Session session = new Session(new SessionOptions());
        checkStatus(session.Create(graph));

        // detect objects from all files in directory
        File dir = new File("/path/to/images/");
        for (File f : dir.listFiles()) {
            try (PointerScope scope = new PointerScope()) {
                detectObjects(f, session);
            }
            System.out.println(Pointer.physicalBytes());
        }
    }
```

When executing this code with `opencv-platform`, `tensorflow-platform`, and the model file from [ssd_inception_v2_coco_2017_11_17.tar.gz](http://download.tensorflow.org/models/object_detection/ssd_inception_v2_coco_2017_11_17.tar.gz), the output shows that memory usage rapidly stabilizes around 1 GB:
```
955539456
1039908864
1065193472
1085517824
1087553536
1093492736
1139658752
1140494336
1141108736
1145044992
1145335808
1162153984
1163288576
1163067392
...
```

However, if we take the `PointerScope` out of the loop, it goes on to fill up all the memory that we give it, which can easily exceed 16 GB by default on today's machines:
```
972619776
1058455552
1119633408
1162756096
1168207872
1189122048
1234366464
1306308608
1334439936
1362952192
1391730688
1421258752
1437138944
1493704704
1494519808
...
```

This is good not only to prevent wasting resources, but also to limit memory fragmentation. If you are interested in using TensorFlow this way, thanks to [Nico Hezel](https://github.com/neiko2002), who also fixed the build for TensorFlow with CUDA support on Windows, additional samples are now available at:

 * [https://github.com/bytedeco/javacpp-presets/tree/master/tensorflow/samples](https://github.com/bytedeco/javacpp-presets/tree/master/tensorflow/samples)

Finally, other important changes include:

 * New artifacts for CUDA and cuDNN containing their redistributable libraries similarly to [NVIDIA at Docker Hub](https://hub.docker.com/r/nvidia/cuda/), but that work also on Mac and Windows, to allow other libraries (Deeplearning4j, OpenCV, Caffe, TensorFlow, etc) to use GPUs without installing CUDA:
   * [https://github.com/bytedeco/javacpp-presets/tree/master/cuda](https://github.com/bytedeco/javacpp-presets/tree/master/cuda)
 * New presets for [ARPACK-NG](https://github.com/bytedeco/javacpp-presets/tree/master/arpack-ng), [CMINPACK](https://github.com/bytedeco/javacpp-presets/tree/master/cminpack), [TensorRT](https://github.com/bytedeco/javacpp-presets/tree/master/tensorrt), and [MKL-DNN](https://github.com/bytedeco/javacpp-presets/tree/master/mkl-dnn) (which bundles a free version of MKL that other presets can use via [OpenBLAS](https://github.com/bytedeco/javacpp-presets/tree/master/openblas)),
 * 64-bit builds for Android (`android-arm64` and `android-x86_64`) and iOS (`ios-arm64` and `ios-x86_64`) that work with both [Gluon VM](https://gluonhq.com/products/mobile/vm/) and [RoboVM](http://robovm.mobidevelop.com/),
 * New [`LeptonicaFrameConverter`](http://bytedeco.org/javacv/apidocs/org/bytedeco/javacv/LeptonicaFrameConverter.html) for Tesseract and [`JavaFXFrameConverter`](http://bytedeco.org/javacv/apidocs/org/bytedeco/javacv/JavaFXFrameConverter.html) for JavaFX (thanks to [Johan Vos](https://github.com/johanvos)), and
 * Support for audio frames in [`FFmpegFrameFilter`](http://bytedeco.org/javacv/apidocs/org/bytedeco/javacv/FFmpegFrameFilter.html) bringing it on par with [`FFmpegFrameGrabber`](http://bytedeco.org/javacv/apidocs/org/bytedeco/javacv/FFmpegFrameGrabber.html) and [`FFmpegFrameRecorder`](http://bytedeco.org/javacv/apidocs/org/bytedeco/javacv/FFmpegFrameRecorder.html).

Please find more information about these updates and other changes in the `CHANGELOG.md` files for [JavaCPP](https://github.com/bytedeco/javacpp), [JavaCPP Presets](https://github.com/bytedeco/javacpp-presets), [JavaCV](https://github.com/bytedeco/javacv), [ProCamCalib](https://github.com/bytedeco/procamcalib), and [ProCamTracker](https://github.com/bytedeco/procamtracker). Many thanks to all contributors! According to `git shortlog 1.4..1.4.2 --summary` they are:

> agiasmothi, Alex Black, Aman Gupta, canelzio, delthas, gunther82, Jeremy Apthorp, Jeremy Laviole, Johan Vos, Kevin Watters, louxiu, Mariano Scazzariello, Michael Haslgrübler, mifritscher, Nico Hezel, SIY1121, Sören Brunk, Stanislav Chizhik, Vincent Baines (vb216)

For completeness, here are all contributors since the beginning according to `git shortlog --summary`:

> Adam Gibson, agiasmothi, Agustin Alvarez, Alex Black, alicana, Aman Gupta, Amnon Owed, Amos Yuen, Andreas Eberle, Arseniy Pendryak, Ashley, beligum, Benjamin Hill, bennyveo, canelzio, Chetan Narsude, Chris Chow, Chris Nuernberger, Cyprien Noel (cypof), delthas, Djalma Antonio dos Passos Filho, Dmitriy Gerashenko, dragos-d, Edison Wang, Edu Garcia, egorapolonov, emilio1986, Fabrizio (Misto) Milo, Felix Andrews, Florian Enner, François Garillot, Fredrik Henricsson, Gabor Nagy, George Kankava, Gertjan Al, GroG (supertick), gunther82, HungHD, Jadon Fowler, Jarek Sacha (jarek), Jeremy Apthorp, Jeremy Laviole, Jeremy Martin, Jeroen Arens, jjYBdx4IL, Johan Vos, John Sichi, Jonathan Leitschuh, juergenuhl, kenji yoshida, Kevin Watters, leef, lfdversluis, Lloyd Chan (lloydmeta), louxiu, Luca Barbato, mabruce, Mariano Scazzariello, Martin, matrupihai, Maurice, Maurice Betzel (mbetzel), Michael Dietz, Michael Haslgrübler, Michael Tandy, Michal Conos, mifritscher, Miroslav Zoričák, mmanco, Mo Tao, mtandy, Nico Hezel, n-kai-cj, Oleg Kuliasov, Pachev Joseph, Paolo Bolettieri (paolobolettieri), Paul Gregoire, Paul Hammant, Paul Heideman, Pawel Hajduk, pchundi, Perry Nguyen, Philipp Moritz, Piotr, Richard Alam, Ryan Osial, Sam Carlberg, Samuel, Sean Carlisle, SIY1121, Sören Brunk, Stanislav Chizhik, Tatsuyuki Ishi, Teerapap Changwichukarn, The Gitter Badger, Tiago Daniel Jacobs, Tom Clark, Trejkaz (pen name), TwistedUmbrella, Vincent Baines (vb216), waldemarnt, Yizhi Liu, zhanhb, wmz7year, 李立强

This list does not include anyone who has helped in other ways, including but not limited to fixing CI settings, testing builds, debugging code, filing issues, making corrections, reporting bugs, proposing ideas, updating the wiki, etc, but please do continue to communicate with us via the [mailing list from Google Groups](http://groups.google.com/group/javacpp-project), [issues on GitHub](https://github.com/bytedeco/javacpp/issues), or [the chat room at Gitter](https://gitter.im/bytedeco/javacpp). Your input is valuable, we hope to continue hearing from all of you!
