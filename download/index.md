---
layout: default
title: Bytedeco Download
---

Download
========

All binary and source artifacts are made available through the <a href="http://search.maven.org/#search|ga|1|bytedeco">Maven Central Repository</a>, so you can make your build files depend on them (as shown in the [Maven Dependencies](#maven-dependencies) section below), and they will get downloaded automatically. In the case of JavaCPP Presets, please remember to also include the platform-specific artifacts as well. One can also download everything manually. Below is a list of assembly archive files containing all that is available from the latest releases.

Archive Files
-------------

 * JavaCPP 0.11 binary archive  [javacpp-0.11-bin.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/javacpp/0.11/javacpp-0.11-bin.zip) (238 KB)
 * JavaCPP 0.11 source archive  [javacpp-0.11-src.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/javacpp/0.11/javacpp-0.11-src.zip) (219 KB)
 * JavaCPP Presets 0.11 binary archive  [javacpp-presets-0.11-bin.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/javacpp-presets/0.11/javacpp-presets-0.11-bin.zip) (216 MB)
 * JavaCPP Presets 0.11 source archive  [javacpp-presets-0.11-src.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/javacpp-presets/0.11/javacpp-presets-0.11-src.zip) (1298 KB)
 * JavaCV 0.11 binary archive  [javacv-0.11-bin.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/javacv/0.11/javacv-0.11-bin.zip) (142 MB)
 * JavaCV 0.11 source archive  [javacv-0.11-src.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/javacv/0.11/javacv-0.11-src.zip) (398 KB)
 * ProCamCalib 0.11 binary archive  [procamcalib-0.11-bin.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/procamcalib/0.11/procamcalib-0.11-bin.zip) (107 MB)
 * ProCamCalib 0.11 source archive  [procamcalib-0.11-src.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/procamcalib/0.11/procamcalib-0.11-src.zip) (49 KB)
 * ProCamTracker 0.11 binary archive  [procamtracker-0.11-bin.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/procamtracker/0.11/procamtracker-0.11-bin.zip) (114 MB)
 * ProCamTracker 0.11 source archive  [procamtracker-0.11-src.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/procamtracker/0.11/procamtracker-0.11-src.zip) (67 KB)


<a id="maven-dependencies"></a>
Maven Dependencies
------------------

Here is a sample list of dependencies that you can use as base for your own `pom.xml` file. Additionally, we need to either set the `platform.dependency` system property (via the `-D` command line option) to something like `android-arm`, or set the `platform.dependencies` one to `true` to get all the binaries for Android, Linux, Mac OS X, and Windows. On build systems where this does not work, we need to add the platform-specific artifacts manually.

```xml
    <dependency>
      <groupId>org.bytedeco</groupId>
      <artifactId>javacpp</artifactId>
      <version>0.11</version>
    </dependency>

    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>opencv</artifactId>
      <version>2.4.11-0.11</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>ffmpeg</artifactId>
      <version>2.6.1-0.11</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>flycapture</artifactId>
      <version>2.7.3.19-0.11</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>libdc1394</artifactId>
      <version>2.2.3-0.11</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>libfreenect</artifactId>
      <version>0.5.2-0.11</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>videoinput</artifactId>
      <version>0.200-0.11</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>artoolkitplus</artifactId>
      <version>2.3.1-0.11</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>flandmark</artifactId>
      <version>1.07-0.11</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>fftw</artifactId>
      <version>3.3.4-0.11</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>gsl</artifactId>
      <version>1.16-0.11</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>llvm</artifactId>
      <version>3.6.0-0.11</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>leptonica</artifactId>
      <version>1.71-0.11</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>tesseract</artifactId>
      <version>3.03-rc1-0.11</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>caffe</artifactId>
      <version>master-0.11</version>
    </dependency>

    <dependency>
      <groupId>org.bytedeco</groupId>
      <artifactId>javacv</artifactId>
      <version>0.11</version>
    </dependency>
```

