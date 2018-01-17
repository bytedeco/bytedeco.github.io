---
layout: default
title: Download
---

Download
========

All binary and source artifacts are made available through the <a href="http://search.maven.org/#search|ga|1|bytedeco">Maven Central Repository</a>, so you can make your build files depend on them (as shown in the [Maven Dependencies](#maven-dependencies) section below), and they will get downloaded automatically. In the case of JavaCPP Presets, please remember to also include the platform-specific artifacts as well. One can also download everything manually. Below is a list of assembly archive files containing all that is available from the latest releases.

Archive Files
-------------

 * JavaCPP 1.4 binary archive  [javacpp-1.4-bin.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/javacpp/1.4/javacpp-1.4-bin.zip) (348 KB)
 * JavaCPP 1.4 source archive  [javacpp-1.4-src.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/javacpp/1.4/javacpp-1.4-src.zip) (319 KB)
 * JavaCPP Presets 1.4 binary archive  [javacpp-platform-presets-1.4-bin.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/javacpp-presets-platform/1.4/javacpp-presets-platform-1.4-bin.zip) (738 MB)
 * JavaCPP Presets 1.4 source archive  [javacpp-platform-presets-1.4-src.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/javacpp-presets-platform/1.4/javacpp-presets-platform-1.4-src.zip) (3.9 MB)
 * JavaCV 1.4 binary archive  [javacv-platform-1.4-bin.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/javacv-platform/1.4/javacv-platform-1.4-bin.zip) (255 MB)
 * JavaCV 1.4 source archive  [javacv-platform-1.4-src.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/javacv-platform/1.4/javacv-platform-1.4-src.zip) (463 KB)
 * ProCamCalib 1.4 binary archive  [procamcalib-1.4-bin.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/procamcalib/1.4/procamcalib-1.4-bin.zip) (199 MB)
 * ProCamCalib 1.4 source archive  [procamcalib-1.4-src.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/procamcalib/1.4/procamcalib-1.4-src.zip) (51 KB)
 * ProCamTracker 1.4 binary archive  [procamtracker-1.4-bin.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/procamtracker/1.4/procamtracker-1.4-bin.zip) (205 MB)
 * ProCamTracker 1.4 source archive  [procamtracker-1.4-src.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/procamtracker/1.4/procamtracker-1.4-src.zip) (68 KB)


Maven Dependencies
------------------

Here is a sample list of dependencies that you can use as base for your own `pom.xml` file. This downloads binaries for all platforms, but to get binaries for only one platform we can set the `javacpp.platform` system property (via the `-D` command line option) to something like `android-arm`, `linux-x86_64`, `macosx-x86_64`, `windows-x86_64`, etc. For examples with Gradle and sbt, please refer to the [README.md file of the JavaCPP Presets](https://github.com/bytedeco/javacpp-presets#downloads). Other options available for Scala users are [sbt-javacpp](https://github.com/bytedeco/sbt-javacpp) and [sbt-javacv](https://github.com/bytedeco/sbt-javacv).

```xml
    <dependency>
      <groupId>org.bytedeco</groupId>
      <artifactId>javacpp</artifactId>
      <version>1.4</version>
    </dependency>

    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>opencv-platform</artifactId>
      <version>3.4.0-1.4</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>ffmpeg-platform</artifactId>
      <version>3.4.1-1.4</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>flycapture-platform</artifactId>
      <version>2.11.4.121-1.4</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>libdc1394-platform</artifactId>
      <version>2.2.5-1.4</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>libfreenect-platform</artifactId>
      <version>0.5.3-1.4</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>libfreenect2-platform</artifactId>
      <version>0.2.0-1.4</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>librealsense-platform</artifactId>
      <version>1.12.1-1.4</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>videoinput-platform</artifactId>
      <version>0.200-1.4</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>artoolkitplus-platform</artifactId>
      <version>2.3.1-1.4</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>chilitags-platform</artifactId>
      <version>master-1.4</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>flandmark-platform</artifactId>
      <version>1.07-1.4</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>hdf5-platform</artifactId>
      <version>1.10.1-1.4</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>mkl-platform</artifactId>
      <version>2018.1-1.4</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>openblas-platform</artifactId>
      <version>0.2.20-1.4</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>fftw-platform</artifactId>
      <version>3.3.7-1.4</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>gsl-platform</artifactId>
      <version>2.4-1.4</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>llvm-platform</artifactId>
      <version>5.0.1-1.4</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>libpostal-platform</artifactId>
      <version>1.1-alpha-1.4</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>leptonica-platform</artifactId>
      <version>1.74.4-1.4</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>tesseract-platform</artifactId>
      <version>3.05.01-1.4</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>caffe-platform</artifactId>
      <version>1.0-1.4</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>cuda-platform</artifactId>
      <version>9.1-7.0-1.4</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>mxnet-platform</artifactId>
      <version>1.0.0-1.4</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>tensorflow-platform</artifactId>
      <version>1.5.0-rc1-1.4</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>ale-platform</artifactId>
      <version>0.6.0-1.4</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>liquidfun-platform</artifactId>
      <version>20170717-43d53e0-1.4</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>skia-platform</artifactId>
      <version>20170511-53d6729-1.4</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>systems-platform</artifactId>
      <version>1.4</version>
    </dependency>

    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>opencv</artifactId>
      <version>3.4.0-1.4</version>
      <classifier>linux-x86_64-gpu</classifier>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>opencv</artifactId>
      <version>3.4.0-1.4</version>
      <classifier>macosx-x86_64-gpu</classifier>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>opencv</artifactId>
      <version>3.4.0-1.4</version>
      <classifier>windows-x86_64-gpu</classifier>
    </dependency>

    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>caffe</artifactId>
      <version>1.0-1.4</version>
      <classifier>linux-x86_64-gpu</classifier>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>caffe</artifactId>
      <version>1.0-1.4</version>
      <classifier>macosx-x86_64-gpu</classifier>
    </dependency>

    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>tensorflow</artifactId>
      <version>1.5.0-rc1-1.4</version>
      <classifier>linux-x86_64-gpu</classifier>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>tensorflow</artifactId>
      <version>1.5.0-rc1-1.4</version>
      <classifier>macosx-x86_64-gpu</classifier>
    </dependency>

    <dependency>
      <groupId>org.bytedeco</groupId>
      <artifactId>javacv-platform</artifactId>
      <version>1.4</version>
    </dependency>
```

