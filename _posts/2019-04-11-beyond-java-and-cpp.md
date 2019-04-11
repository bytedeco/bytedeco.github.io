---
layout: post
title: Beyond Java and C++
---

We are happy to announce the first release of Bytedeco in this new Japanese era! Version 1.5 is available for [JavaCPP](https://github.com/bytedeco/javacpp), [JavaCPP Presets](https://github.com/bytedeco/javacpp-presets), [JavaCV](https://github.com/bytedeco/javacv), [ProCamCalib](https://github.com/bytedeco/procamcalib), and [ProCamTracker](https://github.com/bytedeco/procamtracker). This release comes with new presets for NumPy (yes, the Python library, more on that below), NCCL, nGraph, Qt (providing an alternative to AWT, Swing, and JavaFX), and cpu_features, as well as updates for FFmpeg (now also including the [ffmpeg](http://bytedeco.org/javacpp-presets/ffmpeg/apidocs/org/bytedeco/ffmpeg/ffmpeg.html) and [ffprobe](http://bytedeco.org/javacpp-presets/ffmpeg/apidocs/org/bytedeco/ffmpeg/ffprobe.html) programs themselves), libfreenect, HDF5, MKL, MKL-DNN, LLVM, Leptonica, ARPACK-NG, CUDA, cuDNN, MXNet, TensorFlow, TensorRT, ONNX, LiquidFun, and Skia. Many thanks to all contributors! Since the [previous post]({% post_url 2019-01-11-importance-of-a-distribution %}) just 3 months ago, according to `git shortlog 1.4.4..1.5 --summary`, they were:

> Alex Merritt, Arnaud Jeansen, Greg Hart, HGuillemet, k3rnL, Samuel Audet, Simon Harris

However, as usual, this list does not contain anyone who very generously helped fix CI settings, test builds, debug code, file suggestions, make corrections, report bugs, propose ideas, update wiki pages, etc. One can find more detailed information about all these changes and fixes on the repositories listed above in the `CHANGELOG.md` files, among other places.

As hinted previously though, the most important update concerns the modularization of all the artifacts to comply with the [Java Platform Module System](https://en.wikipedia.org/wiki/Java_Platform_Module_System) (JPMS). In theory, we simply have to add irritating `module-info.java` files everywhere (we are grateful to [ModiTect](https://github.com/moditect/moditect) for the help with that), but one major restriction of JPMS is that we cannot split a Java package across multiple modules, so we had to update the packages of all the presets to comply, thus the minor version bump from 1.4.x to 1.5.x. In no small part thanks to Hervé Guillemet, we eventually managed to come up with a satisfactory naming scheme that not only complies with JPMS, but also produces top-level classes that are closer to typical Java APIs and that Javadoc can render more clearly into HTML. Instead of putting all classes in the `org.bytedeco.javacpp` package, all modules now have their own packages based on the names of their artifacts, for example, `org.bytedeco.opencv` in the case of OpenCV. Inside such a package we have top-level classes, further divided into subpackages when the artifact contains multiples native libraries, as well as a `global` subpackage containing, you guessed it, classes with native declarations for global C/C++ functions and variables. For most downstream projects, upgrading requires modifications to the import statements only. In the case of OpenCV and TensorFlow, for example, we would typically have statements like the following:

```java
import static org.bytedeco.javacpp.opencv_core.*;
import static org.bytedeco.javacpp.opencv_imgproc.*;
import static org.bytedeco.javacpp.opencv_calib3d.*;
import static org.bytedeco.javacpp.opencv_objdetect.*
import static org.bytedeco.javacpp.tensorflow.*;
```

Given these exact statements, to migrate to the new API, the only change required would be to replace them with the following:
```java
import org.bytedeco.opencv.opencv_core.*;
import org.bytedeco.opencv.opencv_imgproc.*;
import org.bytedeco.opencv.opencv_calib3d.*;
import org.bytedeco.opencv.opencv_objdetect.*;
import org.bytedeco.tensorflow.*;
import static org.bytedeco.opencv.global.opencv_core.*;
import static org.bytedeco.opencv.global.opencv_imgproc.*;
import static org.bytedeco.opencv.global.opencv_calib3d.*;
import static org.bytedeco.opencv.global.opencv_objdetect.*;
import static org.bytedeco.tensorflow.global.tensorflow.*;
```

To prevent conflicts with the old API, we also changed the `groupId` of all artifacts to `org.bytedeco`, so no more annoyingly long names containing `org.bytedeco.javacpp-presets`, which also reflects our evolving technical understanding of the world where the JVM cannot rule them all.

Java is able to abstract away the underlying operating system, and, along with tools such as Maven and now [jlink](https://docs.oracle.com/javase/9/tools/jlink.htm) to create compact self-contained standalone applications as per the [opencv-stitching-jlink](https://github.com/bytedeco/sample-projects/tree/master/opencv-stitching-jlink) sample project, its abilities to manage the complexity of software in the ecosystem is unparalleled. However, the JVM itself is failing miserably at supporting other existing programming languages. We obviously need access to native libraries written in C/C++ for compute intensive algorithms, but even popular scripting languages such as JavaScript and Python have never been able to feel at home on the JVM either, notwithstanding their own arguably inferior native runtimes. [Jython](https://www.jython.org/) is stuck at Python 2.7, while [Nashorn has been deprecated](http://openjdk.java.net/jeps/335) even before its proposed successor, [Graal JavaScript](https://github.com/graalvm/graaljs), is ready to take its place. Likewise, [Graal Python](https://github.com/graalvm/graalpython) is truly awesome technology, but is still an "early-stage experimental implementation" that runs pretty much nothing useful yet, let alone CUDA or any kind of support for GPU no where to be found on any roadmap. Whatever the cause is for the lack of the appearance of a universal VM that a majority of users would be happy with, it is instead possible to have multiple runtimes executing in the same process to share data efficiently, an approach that is also future-proof given that Graal still needs to implement JNI and the C API of Python anyway to be compatible with tools such as JNA, JNR, or JavaCPP, and libraries like NumPy or TensorFlow. We show that an initial implementation can be easily achieved today in the case of CPython and the current JDK, starting with the [JavaCPP Presets for NumPy](https://github.com/bytedeco/javacpp-presets/tree/master/numpy), which leaves all the high-level dependency management to Java and Maven, where JavaCPP automatically extracts the Python package to its cache, along with MKL on supported platforms, in a portable and repeatable fashion, without the need of any other less portable tools including Docker. In effect, this makes Python and NumPy available as a sort of domain-specific scripting language to Java developers. We plan on making more Python packages available this way, continuing next with the [JavaCPP Presets for TensorFlow](https://github.com/bytedeco/javacpp-presets/tree/master/tensorflow).

If you would like to participate in this effort, please communicate via the [mailing list from Google Groups](http://groups.google.com/group/javacpp-project), [issues on GitHub](https://github.com/bytedeco/javacpp/issues), or [the chat room at Gitter](https://gitter.im/bytedeco/javacpp). In any case, stay tuned for more exciting developments later this year!
