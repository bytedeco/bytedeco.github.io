---
layout: default
title: Download
---

Download
========

All binary and source artifacts are made available through the <a href="http://search.maven.org/#search|ga|1|bytedeco">Maven Central Repository</a>, so you can make your build files depend on them (as shown in the [Maven Dependencies](#maven-dependencies) section below), and they will get downloaded automatically. In the case of JavaCPP Presets, please remember to also include the platform-specific artifacts as well. One can also download everything manually. Below is a list of assembly archive files containing all that is available from the latest releases.

Archive Files
-------------

 * JavaCPP 1.3 binary archive  [javacpp-1.3-bin.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/javacpp/1.3/javacpp-1.3-bin.zip) (319 KB)
 * JavaCPP 1.3 source archive  [javacpp-1.3-src.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/javacpp/1.3/javacpp-1.3-src.zip) (295 KB)
 * JavaCPP Presets 1.3 binary archive  [javacpp-platform-presets-1.3-bin.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/javacpp-presets-platform/1.3/javacpp-presets-platform-1.3-bin.zip) (516 MB)
 * JavaCPP Presets 1.3 source archive  [javacpp-platform-presets-1.3-src.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/javacpp-presets-platform/1.3/javacpp-presets-platform-1.3-src.zip) (2.8 MB)
 * JavaCV 1.3 binary archive  [javacv-platform-1.3-bin.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/javacv-platform/1.3/javacv-platform-1.3-bin.zip) (189 MB)
 * JavaCV 1.3 source archive  [javacv-platform-1.3-src.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/javacv-platform/1.3/javacv-platform-1.3-src.zip) (437 KB)
 * ProCamCalib 1.3 binary archive  [procamcalib-1.3-bin.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/procamcalib/1.3/procamcalib-1.3-bin.zip) (146 MB)
 * ProCamCalib 1.3 source archive  [procamcalib-1.3-src.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/procamcalib/1.3/procamcalib-1.3-src.zip) (51 KB)
 * ProCamTracker 1.3 binary archive  [procamtracker-1.3-bin.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/procamtracker/1.3/procamtracker-1.3-bin.zip) (153 MB)
 * ProCamTracker 1.3 source archive  [procamtracker-1.3-src.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/procamtracker/1.3/procamtracker-1.3-src.zip) (68 KB)


Maven Dependencies
------------------

Here is a sample list of dependencies that you can use as base for your own `pom.xml` file. This downloads binaries for all platforms, but to get binaries for only one platform we can set the `javacpp.platform` system property (via the `-D` command line option) to something like `android-arm`, `linux-x86_64`, `macosx-x86_64`, `windows-x86_64`, etc. For examples with Gradle and sbt, please refer to the [README.md file of the JavaCPP Presets](https://github.com/bytedeco/javacpp-presets#downloads). Other options available for Scala users are [sbt-javacpp](https://github.com/bytedeco/sbt-javacpp) and [sbt-javacv](https://github.com/bytedeco/sbt-javacv).

```xml
    <dependency>
      <groupId>org.bytedeco</groupId>
      <artifactId>javacpp</artifactId>
      <version>1.3</version>
    </dependency>

    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>opencv-platform</artifactId>
      <version>3.1.0-1.3</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>ffmpeg-platform</artifactId>
      <version>3.2.1-1.3</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>flycapture-platform</artifactId>
      <version>2.9.3.43-1.3</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>libdc1394-platform</artifactId>
      <version>2.2.4-1.3</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>libfreenect-platform</artifactId>
      <version>0.5.3-1.3</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>librealsense-platform</artifactId>
      <version>1.9.6-1.3</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>videoinput-platform</artifactId>
      <version>0.200-1.3</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>artoolkitplus-platform</artifactId>
      <version>2.3.1-1.3</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>chilitags-platform</artifactId>
      <version>master-1.3</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>flandmark-platform</artifactId>
      <version>1.07-1.3</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>hdf5-platform</artifactId>
      <version>1.10.0-patch1-1.3</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>openblas-platform</artifactId>
      <version>0.2.19-1.3</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>fftw-platform</artifactId>
      <version>3.3.5-1.3</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>gsl-platform</artifactId>
      <version>2.2.1-1.3</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>llvm-platform</artifactId>
      <version>3.9.0-1.3</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>leptonica-platform</artifactId>
      <version>1.73-1.3</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>tesseract-platform</artifactId>
      <version>3.04.01-1.3</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>caffe-platform</artifactId>
      <version>master-1.3</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>cuda-platform</artifactId>
      <version>8.0-1.3</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>mxnet-platform</artifactId>
      <version>master-1.3</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>tensorflow-platform</artifactId>
      <version>0.11.0-1.3</version>
    </dependency>

    <dependency>
      <groupId>org.bytedeco</groupId>
      <artifactId>javacv-platform</artifactId>
      <version>1.3</version>
    </dependency>
```

