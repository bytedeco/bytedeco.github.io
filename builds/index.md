yout: default
title: Builds
---

<style>
table{
    border-collapse: collapse;
    border-spacing: 0;
    border:2px solid #000000;
}

th{
    border:2px solid #000000;
    padding: 3px;
}

td{
    border:1px solid #000000;
    padding: 3px;
}
</style>

Builds
======

A Jenkins CI server provides builds for the JavaCPP Presets, building across a range of platform targets and uploading snapshots. The current build status for this targets is below, with the tail of log files available to assist in any debugging. This is a recent addition and so any feedback is welcome!

Using snapshot builds
---------------------

These builds can be used instead of the main release cycles to test and use latest features with only two changes required. 

Firstly, in your maven settings file, add a profile like the one below to enable snapshots:

```xml
<profile>
  <id>allow-snapshots</id>
  <activation><activeByDefault>true</activeByDefault></activation>
  <repositories>
    <repository>
      <id>snapshots-repo-oss</id>
      <url>https://oss.sonatype.org/content/repositories/snapshots</url>
      <releases><enabled>false</enabled></releases>
      <snapshots><enabled>true</enabled></snapshots>
    </repository>
  </repositories>
</profile>
```

Secondly, update your pom file to use the latest snapshot. A full set of definitions based on the latest builds is provided at the end of this page. Taking the [OpenCV presets example](https://github.com/bytedeco/javacpp-presets/blob/master/opencv/README.md) , the dependency in pom file would change to this:

```xml
<dependency>
  <groupId>org.bytedeco.javacpp-presets</groupId>
  <artifactId>opencv-platform</artifactId>
      <version>3.1.0-1.3.1-SNAPSHOT</version>
</dependency>
```

It's also advisable to use specify your host platform with the javacpp.platform flag, e.g. for 64 bit linux "-Djavacpp.platform=linux-x86_64", as full distributions for all platforms may not be available.

Current build status
---------------------

These builds are currently run on a weekly basis, with any failed jobs left for further resolution. Fixes welcome!

|------------+-----------------------+---------------------+-----------------|---------|
| State | Target | Last Failed Build | Last Successful Build | Build Log |
|:----------:|-----------------------|---------------------|-----------------|---------|
| <img src="FAILURE.png" width="20" height="20" /> |Presets-Android|07-01-2017 14:00:47|20-12-2016 15:49:56|[Log](Presets-Android.log)|
| <img src="FAILURE.png" width="20" height="20" /> |Presets-Linux64|07-01-2017 11:29:28|21-12-2016 17:31:45|[Log](Presets-Linux64.log)|
| <img src="FAILURE.png" width="20" height="20" /> |Presets-Linux32|07-01-2017 12:05:10|21-12-2016 10:55:06|[Log](Presets-Linux32.log)|
| <img src="FAILURE.png" width="20" height="20" /> |Presets-LinuxArmhf|07-01-2017 13:12:54|05-01-2017 10:51:50|[Log](Presets-LinuxArmhf.log)|
| <img src="FAILURE.png" width="20" height="20" /> |Presets-Mac64|07-01-2017 12:00:52|01-12-2016 20:40:10|[Log](Presets-Mac64.log)|
| <img src="FAILURE.png" width="20" height="20" /> |Presets-PPC64LE|07-01-2017 12:31:55|31-12-2016 11:53:42|[Log](Presets-PPC64LE.log)|
| <img src="FAILURE.png" width="20" height="20" /> |Presets-Windows32|07-01-2017 14:33:25|31-12-2016 11:47:27|[Log](Presets-Windows32.log)|
| <img src="FAILURE.png" width="20" height="20" /> |Presets-Windows64|07-01-2017 12:53:11|05-01-2017 10:43:15|[Log](Presets-Windows64.log)|
| <img src="SUCCESS.png" width="20" height="20" /> |Presets-Linux64-OpenJDK9|21-12-2016 11:38:41|21-12-2016 16:56|[Log](Presets-Linux64-OpenJDK9.log)|
|------------+-----------------------+---------------------+-----------------|---------|

<br>

Full set of pom additions
-------------------------

Similarly to the Maven information information for full builds [provided here](http://bytedeco.org/download/#maven-dependencies), snapshot presets can be used with the following dependencies based on the latest build:

```xml
    <dependency>
      <groupId>org.bytedeco</groupId>
      <artifactId>javacpp</artifactId>
      <version>1.3</version>
    </dependency>

    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>opencv-platform</artifactId>
      <version>3.1.0-1.3.1-SNAPSHOT</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>ffmpeg-platform</artifactId>
      <version>3.2.1-1.3.1-SNAPSHOT</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>flycapture-platform</artifactId>
      <version>2.9.3.43-1.3.1-SNAPSHOT</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>libdc1394-platform</artifactId>
      <version>2.2.5-1.3.1-SNAPSHOT</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>libfreenect-platform</artifactId>
      <version>0.5.3-1.3.1-SNAPSHOT</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>librealsense-platform</artifactId>
      <version>1.9.6-1.3.1-SNAPSHOT</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>videoinput-platform</artifactId>
      <version>0.200-1.3.1-SNAPSHOT</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>artoolkitplus-platform</artifactId>
      <version>2.3.1-1.3.1-SNAPSHOT</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>chilitags-platform</artifactId>
      <version>master-1.3.1-SNAPSHOT</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>flandmark-platform</artifactId>
      <version>1.07-1.3.1-SNAPSHOT</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>hdf5-platform</artifactId>
      <version>1.10.0-patch1-1.3.1-SNAPSHOT</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>openblas-platform</artifactId>
      <version>0.2.19-1.3.1-SNAPSHOT</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>fftw-platform</artifactId>
      <version>3.3.5-1.3.1-SNAPSHOT</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>gsl-platform</artifactId>
      <version>2.2.1-1.3.1-SNAPSHOT</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>llvm-platform</artifactId>
      <version>3.9.1-1.3.1-SNAPSHOT</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>leptonica-platform</artifactId>
      <version>1.73-1.3.1-SNAPSHOT</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>tesseract-platform</artifactId>
      <version>3.04.01-1.3.1-SNAPSHOT</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>caffe-platform</artifactId>
      <version>master-1.3.1-SNAPSHOT</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>cuda-platform</artifactId>
      <version>8.0-1.3.1-SNAPSHOT</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>mxnet-platform</artifactId>
      <version>master-1.3.1-SNAPSHOT</version>
    </dependency>
    <dependency>
      <groupId>org.bytedeco.javacpp-presets</groupId>
      <artifactId>tensorflow-platform</artifactId>
      <version>0.11.0-1.3.1-SNAPSHOT</version>
    </dependency>

```

