---
layout: default
title: Builds
---

Builds
======

We now have reliable automated builds using [Travis CI](https://www.travis-ci.org/) (to cover all Android, iOS, Linux, and Mac OS X builds) and [AppVeyor](https://www.appveyor.com/) (providing Windows builds). Thanks to both initiatives for providing such a great service to open source projects! Every pull request is built for all targets, and each commit generates a new snapshot build.

Using Snapshot Builds
---------------------

These builds can be used outside of the main release cycles to test and use latest features with only two changes required.

Firstly, in your [Maven settings file](https://maven.apache.org/settings.html), for example at `~/.m2/settings.xml`, add a profile like the one below to enable snapshots:

```xml
<settings>
  <profiles>
    <!-- ... -->
    <profile>
      <id>allow-snapshots</id>
      <repositories>
        <repository>
          <id>sonatype-nexus-snapshots</id>
          <url>https://oss.sonatype.org/content/repositories/snapshots</url>
          <releases>
            <enabled>false</enabled>
          </releases>
          <snapshots>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
          </snapshots>
        </repository>
      </repositories>
    </profile>
    <!-- ... -->
  </profiles>
  <activeProfiles>
    <activeProfile>allow-snapshots</activeProfile>
  </activeProfiles>
</settings>
```

Secondly, update your `pom.xml` file to use the latest snapshot version. Taking the [OpenCV presets example](https://github.com/bytedeco/javacpp-presets/tree/master/opencv#sample-usage), the dependency in the `pom.xml` file would change to this:

```xml
<dependency>
  <groupId>org.bytedeco.javacpp-presets</groupId>
  <artifactId>opencv-platform</artifactId>
  <version>3.4.1-1.4.2-SNAPSHOT</version>
</dependency>
```

It is also advisable to specify your platform with the `javacpp.platform` system property and use the `--update-snapshots` option, for example, `mvn -Djavacpp.platform=linux-x86_64 --update-snapshots [...]`, as binaries for all platforms may not be available at all times.

For convenience, we can browse and download JAR files manually as well from the snapshot repository:
 * [https://oss.sonatype.org/content/repositories/snapshots/org/bytedeco/](https://oss.sonatype.org/content/repositories/snapshots/org/bytedeco/)

Current Build Status
---------------------

Builds information and history is available on

 * Travis CI for Android, iOS, Linux, and Mac OS X at
   * [bytedeco/javacpp](https://travis-ci.org/bytedeco/javacpp),
   * [bytedeco/javacpp-presets](https://travis-ci.org/bytedeco/javacpp-presets),
   * [bytedeco/javacv](https://travis-ci.org/bytedeco/javacv),
   * [bytedeco/sbt-javacpp](https://travis-ci.org/bytedeco/sbt-javacpp),
   * [bytedeco/sbt-javacv](https://travis-ci.org/bytedeco/sbt-javacv), and on
 * AppVeyor for Windows at
   * [bytedeco/javacpp-presets](https://ci.appveyor.com/project/Bytedeco/javacpp-presets).

