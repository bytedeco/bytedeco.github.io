---
layout: default
title: Bytedeco Download
---

Download
========

All binary and source artifacts are made available through the <a href="http://search.maven.org/#search|ga|1|bytedeco">Maven Central Repository</a>, so you can make your build files depend on them (as shown in the [Maven Dependencies](#maven-dependencies) section below), and they will get downloaded automatically. In the case of JavaCPP Presets, please remember to also include the platform-specific artifacts as well. One can also download everything manually. Below is a list of assembly archive files containing all that is available from the latest releases.

Archive Files
-------------

 * JavaCPP 0.9 binary archive  [javacpp-0.9-bin.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/javacpp/0.9/javacpp-0.9-bin.zip) (195 KB)
 * JavaCPP 0.9 source archive  [javacpp-0.9-src.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/javacpp/0.9/javacpp-0.9-src.zip) (171 KB)
 * JavaCPP Presets 0.9 binary archive  [javacpp-presets-0.9-bin.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/javacpp-presets/0.9/javacpp-presets-0.9-bin.zip) (198 MB)
 * JavaCPP Presets 0.9 source archive  [javacpp-presets-0.9-src.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/javacpp-presets/0.9/javacpp-presets-0.9-src.zip) (1156 KB)
 * JavaCV 0.9 binary archive  [javacv-0.9-bin.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/javacv/0.9/javacv-0.9-bin.zip) (129 MB)
 * JavaCV 0.9 source archive  [javacv-0.9-src.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/javacv/0.9/javacv-0.9-src.zip) (374 KB)
 * ProCamCalib 0.9 binary archive  [procamcalib-0.9-bin.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/procamcalib/0.9/procamcalib-0.9-bin.zip) (98 MB)
 * ProCamCalib 0.9 source archive  [procamcalib-0.9-src.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/procamcalib/0.9/procamcalib-0.9-src.zip) (49 KB)
 * ProCamTracker 0.9 binary archive  [procamtracker-0.9-bin.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/procamtracker/0.9/procamtracker-0.9-bin.zip) (99 MB)
 * ProCamTracker 0.9 source archive  [procamtracker-0.9-src.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/procamtracker/0.9/procamtracker-0.9-src.zip) (66 KB)


<a id="maven-dependencies"></a>
Maven Dependencies
------------------

Here is a sample list of dependencies that you can use as base for your own `pom.xml` file. Additionally, we need to either set the `platform.dependency` property to something like `android-arm`, or set the `platform.dependencies` one to `true` to get all the binaries for Linux, Mac OS X, and Windows.

```xml
    <dependency>
      <groupId>org.bytedeco</groupId>
      <artifactId>javacpp</artifactId>
      <version>0.9</version>
    </dependency>

    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>opencv</artifactId>
      <version>2.4.9-0.9</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>ffmpeg</artifactId>
      <version>2.3-0.9</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>flycapture</artifactId>
      <version>2.6.3.4-0.9</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>libdc1394</artifactId>
      <version>2.2.2-0.9</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>libfreenect</artifactId>
      <version>0.5-0.9</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>videoinput</artifactId>
      <version>0.200-0.9</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>artoolkitplus</artifactId>
      <version>2.3.0-0.9</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>flandmark</artifactId>
      <version>1.07-0.9</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>fftw</artifactId>
      <version>3.3.4-0.9</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>gsl</artifactId>
      <version>1.16-0.9</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>llvm</artifactId>
      <version>3.4.2-0.9</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>leptonica</artifactId>
      <version>1.71-0.9</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>tesseract</artifactId>
      <version>3.03-rc1-0.9</version>
    </dependency>

    <dependency>
      <groupId>org.bytedeco</groupId>
      <artifactId>javacv</artifactId>
      <version>0.9</version>
    </dependency>
```

