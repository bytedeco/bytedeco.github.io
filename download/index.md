---
layout: default
title: Bytedeco Download
---

Download
========

All binary and source artifacts are made available through the <a href="http://search.maven.org/#search|ga|1|bytedeco">Maven Central Repository</a>, so you can make your build files depend on them (as shown in the [Maven Dependencies](#maven-dependencies) section below), and they will get downloaded automatically. In the case of JavaCPP Presets, please remember to also include the platform-specific artifacts as well. One can also download everything manually. Below is a list of assembly archive files containing all that is available from the latest releases.

Archive Files
-------------

 * JavaCPP 0.8 binary archive  [javacpp-0.8-bin.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/javacpp/0.8/javacpp-0.8-bin.zip) (192 KB)
 * JavaCPP 0.8 source archive  [javacpp-0.8-src.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/javacpp/0.8/javacpp-0.8-src.zip) (167 KB)
 * JavaCPP Presets 0.8 binary archive  [javacpp-presets-0.8-bin.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/javacpp-presets/0.8/javacpp-presets-0.8-bin.zip) (121 MB)
 * JavaCPP Presets 0.8 source archive  [javacpp-presets-0.8-src.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/javacpp-presets/0.8/javacpp-presets-0.8-src.zip) (708 KB)
 * JavaCV 0.8 binary archive  [javacv-0.8-bin.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/javacv/0.8/javacv-0.8-bin.zip) (121 MB)
 * JavaCV 0.8 source archive  [javacv-0.8-src.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/javacv/0.8/javacv-0.8-src.zip) (369 KB)
 * ProCamCalib 0.8 binary archive  [procamcalib-0.8-bin.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/procamcalib/0.8/procamcalib-0.8-bin.zip) (93 MB)
 * ProCamCalib 0.8 source archive  [procamcalib-0.8-src.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/procamcalib/0.8/procamcalib-0.8-src.zip) (49 KB)
 * ProCamTracker 0.8 binary archive  [procamtracker-0.8-bin.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/procamtracker/0.8/procamtracker-0.8-bin.zip) (94 MB)
 * ProCamTracker 0.8 source archive  [procamtracker-0.8-src.zip](http://search.maven.org/remotecontent?filepath=org/bytedeco/procamtracker/0.8/procamtracker-0.8-src.zip) (66 KB)


<a id="maven-dependencies"></a>
Maven Dependencies
------------------

Here is a sample list of dependencies that you can use as base for your own `pom.xml` file. `${platform}` should be expanded to the name of your platform: `android-arm`, `android-x86`, `linux-x86`, `linux-x86_64`, `macosx-x86_64`, `windows-x86`, `windows-x86_64`, etc.

```xml
    <dependency>
      <groupId>org.bytedeco</groupId>
      <artifactId>javacpp</artifactId>
      <version>0.8</version>
    </dependency>

    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>opencv</artifactId>
      <version>2.4.9-0.8</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>ffmpeg</artifactId>
      <version>2.2.1-0.8</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>flycapture</artifactId>
      <version>1.7.17-0.8</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>libdc1394</artifactId>
      <version>2.2.2-0.8</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>libfreenect</artifactId>
      <version>0.4-0.8</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>videoinput</artifactId>
      <version>0.200-0.8</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>artoolkitplus</artifactId>
      <version>2.3.0-0.8</version>
    </dependency>

    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>opencv</artifactId>
      <version>2.4.9-0.8</version>
      <classifier>${platform}</classifier>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>ffmpeg</artifactId>
      <version>2.2.1-0.8</version>
      <classifier>${platform}</classifier>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>flycapture</artifactId>
      <version>1.7.17-0.8</version>
      <classifier>${platform}</classifier>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>libdc1394</artifactId>
      <version>2.2.2-0.8</version>
      <classifier>${platform}</classifier>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>libfreenect</artifactId>
      <version>0.4-0.8</version>
      <classifier>${platform}</classifier>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>videoinput</artifactId>
      <version>0.200-0.8</version>
      <classifier>${platform}</classifier>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>artoolkitplus</artifactId>
      <version>2.3.0-0.8</version>
      <classifier>${platform}</classifier>
    </dependency>

    <dependency>
      <groupId>org.bytedeco</groupId>
      <artifactId>javacv</artifactId>
      <version>0.8</version>
    </dependency>
```

