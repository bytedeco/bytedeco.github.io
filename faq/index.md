---
layout: default
title: SSS
---

SSS
===

Aşağıdaki listede yer alan sorularınızın yanıtlarını bulamazsanız, aşağıdaki uygun Google gruplarından bize ulaşmaktan çekinmeyin:

 * [JavaCPP Grubu](http://groups.google.com/group/javacpp-project)
 * [JavaCV Grubu](http://groups.google.com/group/javacv)


Gerçekten C++'ı parse etmeye mi çalışıyorsun? Kulağa çılgınca geliyor.
----------------------------------------------------------------------
[SWIG](http://www.swig.org/) veya [BridJ](https://code.google.com/p/bridj/) gibi diğer araçlardan farklı olarak, C++'ı dönüştürmeye çalışmıyoruz, sadece API ler için gerektiği kadarını dönüştürüyoruz. Yaklaşımımız, prototip olarak [JavaCPP](https://github.com/bytedeco/javacpp) geliştirerek, C++'ın mümkün olduğu kadar çok sayıda C ++ kütüphanesi için uygun şekilde uyarlayarak, C++' ın Java için gerekli özelliklerini almaktan yanayız. Bu yaklaşımımız henüz yanlış değil. Dolayısıyla, teknik olarak bu sorunun cevabı "hayır": C++ 'ın parçalarını, yerel kütüphanelere erişmek için gerekli olan mevcut başlık dosyalarında kullanılan kısmını desteklemeye çalışıyoruz.

OpenCV, TensorFlow, vb. wrapper'lardan farklı mı?
-------------------------------------------------
[JavaCPP](https://github.com/bytedeco/javacpp) maksimum performans ve esneklik için tasarlanmıştır. Java dilinin mantıklı bir şekilde ele alabildiği C++'ın çoğunu haritalamak için çaba harcıyor, farkında olduğumuz diğer çözümlerle eşleştirilebilen yerel işlevsellik için bir kullanılabilirlik seviyesi sunuyor. Aynı zamanda, Java platformundaki geliştirmelerimiz farklı yerel kütüphaneler arası birlikte çalışabilirliği arttırmak için bir dizi temel sınıf barındırır. Ayrıca, Maven gibi standart araçlarla entegrasyonu sağlar ve dağıtımı kolaylaştırır.

Bu lisanlar ticari kullanım için uygun mu?
------------------------------------------
Evet, yazılımlarımız lisanslıdır, bu lisanslar [Apache Lisans, Versiyon 2.0](http://www.apache.org/licenses/LICENSE-2.0), veya  [GPLv2](http://www.gnu.org/licenses/gpl-2.0.html) ile [Classpath exception](http://www.gnu.org/software/classpath/license.html): seçim yapmakta özgürsünüz. İkincisi ise LGPL'ye düşünce olarak benzesede daha az kısıtlamalarla, her iki şekilde de herhangi bir telif hakkı ödemek zorunda kalmadan kendi ticari ürünlerinizde kullanabilirsiniz. Bu tercihin arkasındaki sebep, LGPL ile karşılaştırıldığında, genel olarak Android'e ve sektöre olan ilgilerinin artmasıydı ve Sun Microsystems [OpenJDK](http://openjdk.java.net/legal/gplv2+ce.html)  gibi bir yazılım lisansı ile bir emsal sağladı. [NetBeans](https://netbeans.org/cddl-gplv2.html) gibi seçimi son kullanıcıya bırakıyor. Ve tabiki kullanıcıların hata düzeltmeleri gibi orijinal kodla doğrudan ilişkili olduğunda değişikliklere katkıda bulunmalarını da bekleriz. Projelerin keyfini çıkarın!

Maven Deposu'nda ne var?
------------------------
Örneğin, OpenCV'nin ön ayarlarına bir göz atın: [Search Central for "org.bytedeco.javacpp-presets opencv"](http://search.maven.org/#search%7Cga%7C1%7Corg.bytedeco.javacpp-presets%20opencv). Android, iOS, Linux, Mac OS X, Windows. ARM, ARM64, GÜÇ, x86 ve x86_64 permütasyonları. Doğal olarak, geliştirdiğimiz projeler oldukça fazla, ama pek çok platform için hazır.  Herkesin kullanabileceği şekilde bu depoya projeleri yükledik. Eğer özelliştirmek isterseniz özellikle Linux için, kendi Maven depolarınız için ön ayarları da kendiniz yapmak isteyebilirsiniz, burası size kalmış.

Yapılacaklar listenizde ne var?
-------------------------------
* Yeni kütüphaneler
* Üst limitlere ulaşmak için çabalıyoruz
* Destek için [contribute](/contribute/) sayfamız


Paralelleştirmenin güvenliği hakkında ne söyleyebilir siniz?
------------------------------------------------------------
Bu aşamada, ön ayarların çok iş parçacıklı bir şekilde ümit edeceğiniz gibi çalışacağını garanti edemeyiz. Ayrıca, hazır ayarların mükemmel şekilde yeniden yapılandırıldığını da belirleyemiyoruz.


Ticari destek sunuyor musunuz?
------------------------------
Henüz resmi değil, ama eğer bir ihtiyacınız varsa, lütfen çekinmeyin [iletişim](mailto:contact at bytedeco.org).

