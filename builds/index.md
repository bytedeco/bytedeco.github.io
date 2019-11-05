---
layout: default
title: Builds
---

Builds
======

We now have reliable automated builds using [Travis CI](https://www.travis-ci.org/) (to cover all Android, iOS, Linux, and Mac OS X builds) and [AppVeyor](https://www.appveyor.com/) (providing Windows builds). Thanks to both initiatives for providing such a great service to open source projects! Every pull request is built for all targets, and each commit generates a new snapshot build.

Using Snapshot Builds
---------------------

These builds can be used outside of the main release cycles to test latest features with only a few changes required to the `pom.xml` file to obtain the latest snapshot version from the snapshot repository. Taking the [sample usage for OpenCV](https://github.com/bytedeco/javacpp-presets/tree/master/opencv#sample-usage), the dependency in the `pom.xml` file would change to this, followed by the additional repository settings:

```xml
<project>
    <modelVersion>4.0.0</modelVersion>
    <groupId>org.bytedeco.opencv</groupId>
    <artifactId>stitching</artifactId>
    <version>1.5.3-SNAPSHOT</version>
    <properties>
        <exec.mainClass>Stitching</exec.mainClass>
    </properties>
    <dependencies>
        <dependency>
            <groupId>org.bytedeco</groupId>
            <artifactId>opencv-platform</artifactId>
            <version>4.1.2-1.5.3-SNAPSHOT</version>
        </dependency>
        <!-- ... -->
    </dependencies>
    <repositories>
        <repository>
            <id>sonatype-nexus-snapshots</id>
            <url>https://oss.sonatype.org/content/repositories/snapshots</url>
        </repository>
    </repositories>
    <pluginRepositories>
        <pluginRepository>
            <id>sonatype-nexus-snapshots</id>
            <url>https://oss.sonatype.org/content/repositories/snapshots</url>
        </pluginRepository>
    </pluginRepositories>
    <!-- ... -->
</project>
```

It is also advisable to specify your platform with the `javacpp.platform` system property and use the `--update-snapshots` option, for example, `mvn -Djavacpp.platform=linux-x86_64 --update-snapshots [...]`, as binaries for all platforms may not be available at all times.

The `pom.xml` file above can also be used to download snapshots for others tools such as Gradle or sbt, which are incapable of downloading the snapshot artifacts by themselves. Simply save a dummy `pom.xml` file outside of any project context, run `mvn -U compile` on it, and add the necessary settings for Gradle or sbt to use artifacts from your local Maven repository. In the case of Gradle, [we specify that with `repositories { mavenLocal() }` along with the `dependencies { }` block](https://docs.gradle.org/current/userguide/repository_types.html#example_adding_the_local_maven_cache_as_a_repository), in `app/build.gradle` for an Android project, while for sbt, [we can put `resolvers += Resolver.mavenLocal` next to the `libraryDependencies`](https://www.scala-sbt.org/1.x/docs/Library-Dependencies.html#Resolvers).

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

