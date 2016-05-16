---
layout: default
title: Download
---

Download
========

All binary and source artifacts are made available through the <a href="http://search.maven.org/#search|ga|1|bytedeco">Maven Central Repository</a>, so you can make your build files depend on them (as shown in the [Maven Dependencies](#maven-dependencies) section below), and they will get downloaded automatically. In the case of JavaCPP Presets, please remember to also include the platform-specific artifacts as well. One can also download everything manually. Below is a list of assembly archive files containing all that is available from the latest releases.

Archive Files
-------------

 * JavaCPP 1.2 binary archive  [javacpp-1.2-bin.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/javacpp/1.2/javacpp-1.2-bin.zip) (293 KB)
 * JavaCPP 1.2 source archive  [javacpp-1.2-src.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/javacpp/1.2/javacpp-1.2-src.zip) (276 KB)
 * JavaCPP Presets 1.2 binary archive  [javacpp-presets-1.2-bin.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/javacpp-presets/1.2/javacpp-presets-1.2-bin.zip) (342 MB)
 * JavaCPP Presets 1.2 source archive  [javacpp-presets-1.2-src.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/javacpp-presets/1.2/javacpp-presets-1.2-src.zip) (2.3 MB)
 * JavaCV 1.2 binary archive  [javacv-1.2-bin.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/javacv/1.2/javacv-1.2-bin.zip) (169 MB)
 * JavaCV 1.2 source archive  [javacv-1.2-src.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/javacv/1.2/javacv-1.2-src.zip) (426 KB)
 * ProCamCalib 1.2 binary archive  [procamcalib-1.2-bin.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/procamcalib/1.2/procamcalib-1.2-bin.zip) (129 MB)
 * ProCamCalib 1.2 source archive  [procamcalib-1.2-src.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/procamcalib/1.2/procamcalib-1.2-src.zip) (50 KB)
 * ProCamTracker 1.2 binary archive  [procamtracker-1.2-bin.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/procamtracker/1.2/procamtracker-1.2-bin.zip) (135 MB)
 * ProCamTracker 1.2 source archive  [procamtracker-1.2-src.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/procamtracker/1.2/procamtracker-1.2-src.zip) (67 KB)


Maven Dependencies
------------------

Here is a sample list of dependencies that you can use as base for your own `pom.xml` file. Additionally, we need to either set the `javacpp.platform` system property (via the `-D` command line option) to something like `android-arm`, or set the `javacpp.platform.dependencies` one to `true` to get all the binaries for Android, Linux, Mac OS X, and Windows. **On build systems where this does not work, we need to add the platform-specific artifacts manually.** For examples with Gradle and sbt, please refer to the [README.md file of the JavaCPP Presets](https://github.com/bytedeco/javacpp-presets#downloads). Other options available for Scala users are [sbt-javacpp](https://github.com/bytedeco/sbt-javacpp) and [sbt-javacv](https://github.com/bytedeco/sbt-javacv).

```xml
    <dependency>
      <groupId>org.bytedeco</groupId>
      <artifactId>javacpp</artifactId>
      <version>1.2</version>
    </dependency>

    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>opencv</artifactId>
      <version>3.1.0-1.2</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>ffmpeg</artifactId>
      <version>3.0.2-1.2</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>flycapture</artifactId>
      <version>2.9.3.43-1.2</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>libdc1394</artifactId>
      <version>2.2.4-1.2</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>libfreenect</artifactId>
      <version>0.5.3-1.2</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>videoinput</artifactId>
      <version>0.200-1.2</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>artoolkitplus</artifactId>
      <version>2.3.1-1.2</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>chilitags</artifactId>
      <version>master-1.2</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>flandmark</artifactId>
      <version>1.07-1.2</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>fftw</artifactId>
      <version>3.3.4-1.2</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>gsl</artifactId>
      <version>2.1-1.2</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>llvm</artifactId>
      <version>3.8.0-1.2</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>leptonica</artifactId>
      <version>1.73-1.2</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>tesseract</artifactId>
      <version>3.04.01-1.2</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>caffe</artifactId>
      <version>rc3-1.2</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>cuda</artifactId>
      <version>7.5-1.2</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>mxnet</artifactId>
      <version>master-1.2</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>tensorflow</artifactId>
      <version>0.8.0-1.2</version>
    </dependency>

    <dependency>
      <groupId>org.bytedeco</groupId>
      <artifactId>javacv</artifactId>
      <version>1.2</version>
    </dependency>
```

