---
layout: default
title: Builds
---

Builds
======

We now have reliable automated builds using [Travis CI](https://www.travis-ci.org/) (to cover testing of JavaCPP and JavaCV on ARM, POWER, and x86 architectures for all platforms) and [GitHub Actions](https://github.com/features/actions) (providing Android, iOS, Linux, Mac OS X, and Windows builds for the JavaCPP Presets). Thanks to both initiatives for providing such a great service to open source projects! Every pull request is built for all targets, and each commit generates a new snapshot build.

Using Snapshot Builds
---------------------

These builds can be used outside of the main release cycles to test latest features with only a few changes required to the build files to obtain the latest snapshot version from the snapshot repository.

### Maven
Taking the [sample usage for JavaCV](https://github.com/bytedeco/javacv#sample-usage), the dependency in the `pom.xml` file would change to this, followed by the additional repository settings:

```xml
<project>
    <modelVersion>4.0.0</modelVersion>
    <groupId>org.bytedeco.javacv</groupId>
    <artifactId>demo</artifactId>
    <version>1.5.10-SNAPSHOT</version>
    <dependencies>
        <dependency>
            <groupId>org.bytedeco</groupId>
            <artifactId>javacv-platform</artifactId>
            <version>1.5.10-SNAPSHOT</version>
        </dependency>
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


### Gradle
For Gradle, the equivalent would look like below in `build.gradle` (the one inside the `app` subdirectory for an Android project), as documented at [Gradle - Declaring repositories](https://docs.gradle.org/current/userguide/declaring_repositories.html):
```groovy
repositories {
    maven { url 'https://oss.sonatype.org/content/repositories/snapshots' }
}

dependencies {
    api 'org.bytedeco:javacv-platform:1.5.10-SNAPSHOT'
}

// ...
```
It is also recommended to use the [platform plugin of Gradle JavaCPP](https://github.com/bytedeco/gradle-javacpp#the-platform-plugin) as exemplified in the [`javacv-demo` sample](https://github.com/bytedeco/gradle-javacpp/tree/master/samples/javacv-demo), as well as the `--refresh-dependencies` option, for example, `gradle -PjavacppPlatform=macosx-x86_64 --refresh-dependencies [...]`, as binaries for all platforms may not be available at all times.


### sbt
We can do similarly for sbt in `build.sbt`, as documented at [sbt - Resolvers](https://www.scala-sbt.org/1.x/docs/Library-Dependencies.html#Resolvers):
```scala
resolvers += "Sonatype OSS Snapshots" at "https://oss.sonatype.org/content/repositories/snapshots"

libraryDependencies += "org.bytedeco" % "javacv-platform" % "1.5.10-SNAPSHOT"

// ...
```
Along with either [SBT-JavaCPP](https://github.com/bytedeco/sbt-javacpp) or [SBT-JavaCV](https://github.com/bytedeco/sbt-javacv).


### Other options
If your build tools are having issues downloading snapshot artifacts, the `pom.xml` file above can also be used to download snapshots for them. Simply save a dummy `pom.xml` file outside of any project context, run `mvn -U compile` on it, and the artifacts will get downloaded into `~/.m2/repository` from which other tools can use them, for example, in the case of Gradle with `repositories { mavenLocal() }` or when using sbt with `resolvers += Resolver.mavenLocal`.

For convenience, we can browse and download JAR files manually as well from the snapshot repository:
 * [https://oss.sonatype.org/content/repositories/snapshots/org/bytedeco/](https://oss.sonatype.org/content/repositories/snapshots/org/bytedeco/)

Current Build Status
---------------------

Builds information and history is available on

 * Travis CI at
   * [bytedeco/javacpp](https://travis-ci.org/bytedeco/javacpp),
   * [bytedeco/javacpp-presets](https://travis-ci.org/bytedeco/javacpp-presets),
   * [bytedeco/javacv](https://travis-ci.org/bytedeco/javacv),
   * [bytedeco/gradle-javacpp](https://travis-ci.org/bytedeco/gradle-javacpp),
   * [bytedeco/sbt-javacpp](https://travis-ci.org/bytedeco/sbt-javacpp),
   * [bytedeco/sbt-javacv](https://travis-ci.org/bytedeco/sbt-javacv), and on
 * GitHub Actions at
   * [bytedeco/javacpp](https://github.com/bytedeco/javacpp/actions),
   * [bytedeco/javacpp-presets](https://github.com/bytedeco/javacpp-presets/actions),
   * [bytedeco/javacv](https://github.com/bytedeco/javacv/actions),
   * [bytedeco/gradle-javacpp](https://github.com/bytedeco/gradle-javacpp/actions),
   * [bytedeco/sbt-javacpp](https://github.com/bytedeco/sbt-javacpp/actions),
   * [bytedeco/sbt-javacv](https://github.com/bytedeco/sbt-javacv/actions).

