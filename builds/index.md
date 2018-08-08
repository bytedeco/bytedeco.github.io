---
layout: default
title: Derlemeler
---

Derlemeler
==========

Şu anda [Travis CI](https://www.travis-ci.org/) (tüm Android, iOS, Linux ve Mac OS X sürümlerini kapsayacak şekilde) ve [AppVeyor](https://www.appveyor.com/) için otomatikleştirilmiş yapılarımız var. Her iki girişim sayesinde böylesi bir hizmeti sunabiliyoruz. Her commit ve pull request sonrası derlemeler ile yeni bir snapshot oluşturuyoruz.

Snapshot Derlemesi Kullanımı
----------------------------

Bu derlemeler, yalnızca iki değişiklikle test etmek ve kullanmak için ana sürüm döngüleri dışında kullanılabilir.

Öncelikle [Maven settings dosyasına](https://maven.apache.org/settings.html), örneğin `~/.m2/settings.xml` için, aşağıdakine benzer bir profil ekleyin.

snapshots:
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
        </repository>
      </repositories>
      <pluginRepositories>
        <pluginRepository>
          <id>sonatype-nexus-snapshots</id>
          <url>https://oss.sonatype.org/content/repositories/snapshots</url>
        </pluginRepository>
      </pluginRepositories>
    </profile>
    <!-- ... -->
  </profiles>
  <activeProfiles>
    <activeProfile>allow-snapshots</activeProfile>
  </activeProfiles>
</settings>
```

İkinci olarak, en son anlık görüntü sürümünü kullanmak için `pom.xml` dosyanızı güncelleyin. [OpenCV örneğini](https://github.com/bytedeco/javacpp-presets/tree/master/opencv#sample-usage) kullanarak yapabilirsiniz, pom.xml dosyasındaki bağımlılıklar aşağıdaki gibidir:

```xml
<dependency>
  <groupId>org.bytedeco.javacpp-presets</groupId>
  <artifactId>opencv-platform</artifactId>
  <version>3.4.2-1.4.3-SNAPSHOT</version>
</dependency>
```

Platformunuzu ayrıca belirtebilirsiniz `javacpp.platform` sistem özelliği ve kullanımı `--update-snapshots` örneğin, `mvn -Djavacpp.platform=linux-x86_64 --update-snapshots [...]`, tüm platformlar için binary dosyalar her zaman mevcut olmayabilir.

Kolaylık olması açısından, son buildler sonrası oluşan Jar dosyasnı da indirebilirsiniz:
 * [https://oss.sonatype.org/content/repositories/snapshots/org/bytedeco/](https://oss.sonatype.org/content/repositories/snapshots/org/bytedeco/)

Derleme Durumları
-----------------

Derleme bilgileri ve derleme geçmişi

 * Android, iOS, Linux, ve  Mac OS X için Travis CI
   * [bytedeco/javacpp](https://travis-ci.org/bytedeco/javacpp),
   * [bytedeco/javacpp-presets](https://travis-ci.org/bytedeco/javacpp-presets),
   * [bytedeco/javacv](https://travis-ci.org/bytedeco/javacv),
   * [bytedeco/sbt-javacpp](https://travis-ci.org/bytedeco/sbt-javacpp),
   * [bytedeco/sbt-javacv](https://travis-ci.org/bytedeco/sbt-javacv), and on
 * Windows için AppVeyor
   * [bytedeco/javacpp-presets](https://ci.appveyor.com/project/Bytedeco/javacpp-presets).

