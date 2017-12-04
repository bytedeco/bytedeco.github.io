---
layout: default
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

We now have reliable automated builds using Travis (to cover all Linux / Docker builds) and AppVeyor (providing Windows builds). Thanks to both initiatives for providing such a great service to open source projects! Every pull request is built for all targets, and each commit generates a new snapshot build. 

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

Secondly, update your pom file to use the latest snapshot. Taking the [OpenCV presets example](https://github.com/bytedeco/javacpp-presets/blob/master/opencv/README.md) , the dependency in pom file would change to this:

```xml
<dependency>
  <groupId>org.bytedeco.javacpp-presets</groupId>
  <artifactId>opencv-platform</artifactId>
      <version>3.3.1-1.3.4-SNAPSHOT</version>
</dependency>
```

It's also advisable to use specify your host platform with the javacpp.platform flag, e.g. for 64 bit linux "-Djavacpp.platform=linux-x86_64", as full distributions for all platforms may not be available.

Current build status
---------------------

Windows builds information and history is available on AppVeyor [here](https://ci.appveyor.com/project/Bytedeco/javacpp-presets) and Linux builds information and history is available on Travis [here](https://travis-ci.org/bytedeco/javacpp-presets).

