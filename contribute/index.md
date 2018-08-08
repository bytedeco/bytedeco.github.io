---
layout: default
title: Katkıda bulun
---

Katkıda Bulun
=============

 Ne kadar zaman ve çaba harcamanız gerektiğine bağlı olarak, bu topluluğun büyümesine yardımcı olabileceğiniz birkaç farklı yol vardır. Bunlar aşağıda listelenmiştir: [soruları cevaplayarak](#answer-questions), [bug bildirerek](#report-bugs), [doküman yazarak](#write-documentation), [donanım sağlayarak](#provide-hardware), ve [kod göndererek](#submit-code). İlginiz için teşekkürler!

Soruları Cevaplayın
-------------------
Kullanıcılar sorularını aşağıdaki adreslere gönderirler, sizde burada soruları cevaplayarak bize yardımcı olabilirsiniz. Şu anda iki e-posta listemiz var:

 * [JavaCPP Group](http://groups.google.com/group/javacpp-project)
 * [JavaCV Group](http://groups.google.com/group/javacv)

İkinci mail grubu, JavaCV ve kullanımı ile ilgili daha yüksek seviyeli sorular için hazırlanmıştır. Birincisi grup ise JavaCPP ile ilgili daha düşük seviyeli sorularla ilgilenmektedir. Doğrudan başkalarına yardımcı olmak için, lütfen posta listelerinden birine veya her ikisine de abone olun ve soruları yanıtlamaya başlayın!

Bug Raporlayın
--------------
Yazılımı kullanırken, düzeltilmesi gerektirdiğini düşündüğünüz herhangi bir sorunla karşılaşırsanız lütfen bunu bizimle paylaşın.
Lütfen sorunuzu paylaşırken yeterince ayrıntı verdiğinizden emin olun. Bunun için aşağıdaki bağlantıları kullanabilirsiniz:

 * [JavaCPP Issues](https://github.com/bytedeco/javacpp/issues)
 * [JavaCPP Presets Issues](https://github.com/bytedeco/javacpp-presets/issues)
 * [JavaCV Issues](https://github.com/bytedeco/javacv/issues)
 * [JavaCV Örnek Issues](https://github.com/bytedeco/javacv-examples/issues)
 * [ProCamCalib Issues](https://github.com/bytedeco/procamcalib/issues)
 * [ProCamTracker Issues](https://github.com/bytedeco/procamtracker/issues)

Dokümantasyon Yazın
-------------------
Kullanıcı kılavuzları, öğreticiler ve diğer destekleyici belgeler, daha geniş bir geliştirici kitlesine ulaşmada önemli bir rol oynamaktadır. Bizimle yeni bir makale, dokümantasyon, vb. paylaşarak desktek olabilirsiniz. Bu belgeleri ilgili projenin wiki sayfasına yükleyebilirsiniz:

 * [JavaCPP Wiki](https://github.com/bytedeco/javacpp/wiki)
 * [JavaCPP Presets Wiki](https://github.com/bytedeco/javacpp-presets/wiki)
 * [JavaCV Wiki](https://github.com/bytedeco/javacv/wiki)
 * [JavaCV Örnek Wiki](https://github.com/bytedeco/javacv-examples/wiki)
 * [ProCamCalib Wiki](https://github.com/bytedeco/procamcalib/wiki)
 * [ProCamTracker Wiki](https://github.com/bytedeco/procamtracker/wiki)

API'ların belgelenmesi de önemlidir, ancak yukarıdakilerin aksine, bu belgeler Javadoc'un yardımıyla yazılır, bu yüzden kaynak kodunu değiştirmemiz gerekir, değişiklik neticesinde dokuman otomatik oluşturulkmaktadır. Kaynak kod göndermek için [Kod Gönder](#submit-code) bölümüne bakın.

Donanım Sağlayın
----------------
Birden fazla platformla uğraşmamız gerektiğinden, geliştirme ve testler için özel donanımlara sahip olmak, geliştiriciler için büyük rahatlık sağlayabilir. Şuanda talep ettiğimiz veya ihtiyacımız olan somut birşey yok ama önerilerinize açığız.

Daha fazla platform için JavaCPP Preset'lerinin (özellikle linux-arm) oluşturulmasını katkı sağlayabilirsiniz.

İletişim için [contact us](mailto:contact at bytedeco.org) teşekkürker.

Kod Gönderin
------------
Yeni özellikler ve örnekler eklemek, yorumları netleştirmek, hataları düzeltmek veya yazılımın işlevselliğini geliştirmek için kod gönderebilirsiniz! İlgilendiğiniz bir projede geliştirme yaptıktan sonra sonra, lütfen "istekleri" bize  gönderin:

 * [JavaCPP Pull Requests](https://github.com/bytedeco/javacpp/pulls)
 * [JavaCPP Presets Pull Requests](https://github.com/bytedeco/javacpp-presets/pulls)
 * [JavaCV Pull Requests](https://github.com/bytedeco/javacv/pulls)
 * [JavaCV Örnekler Pull Requests](https://github.com/bytedeco/javacv-examples/pulls)
 * [ProCamCalib Pull Requests](https://github.com/bytedeco/procamcalib/pulls)
 * [ProCamTracker Pull Requests](https://github.com/bytedeco/procamtracker/pulls)

### Proje Fikri

Belirli bir sıraya göre görevlerimizin bir listesi aşağıdadır, her durumda, her fikir kullanıcılar tarafından memnuniyetle karşılanacaktır:

 * JavaCPP'nin `Parser` ını geliştirmek
 * JavaCPP Preset'lerinin Bash / Maven build combo'yu daha iyisi ile değiştirerme (Gradle?)
 * [Creating JavaCPP Presets](https://github.com/bytedeco/javacpp-presets/wiki/Create-New-Presets) for more C/C++ libraries (FFTW, GSL, LLVM, OpenNI, OpenMesh, PCL, Tesseract, etc.)
 * Expanding `FFmpegFrameGrabber` and `FFmpegFrameRecorder` in JavaCV to support more features of FFmpeg, such as metadata and filtering
 * Birden çok platform için oluşturulabilen ve test ortamı sağlayan sürekli entegrasyon için bir çerçeve oluşturmak

 Uygulamak istediğiniz ilginç bir özellik belirledikten sonra, lütfen "issue" oluşturduğunuzdan emin olun. Bu, herkesin neyin üzerinde çalıştığının bilinmesini sağlar. Ayrıca, geliştirme başlamadan önce tasarım hakkında bir tartışma yapmak için fırsat yaratır. İş birliğiniz için teşekkürler.

### Yeni Wraper

Ulaştığımız bazı hedefler:

#### V8

A [V8](https://developers.google.com/v8/get_started) wrapper should including the ability for JS to call back to Java code, and Java to be able to observe JS object lifecycle events so it can release resources.

#### SQLite

Many developers are hugs fans of [SQLite](http://www.sqlite.org/), not just for embedded solutions but as an embeddable engine for creating custom distributed big data stores. There's already a JDBC interface but it only exposes a fraction of the power of the sqlite API. For example, it would be cool to be able to [register custom function / aggregate](http://www.sqlite.org/c3ref/create_function.html) by passing a Java lambda. Or [define our own virtual tables](http://www.sqlite.org/vtab.html) in Java, allowing custom data-structures/data-sources to be participate in SQL joins.

#### Berkeley / POSIX Sockets API

Refer [the wikipedia page](http://en.wikipedia.org/wiki/Berkeley_sockets), but there are others too.

Many of use, over time, have become more and more frustrated with Java's general networking and IO APIs. They are so over-abstracted and are lowest common denominator to support all operating systems. We would rather get much closer to the OS and be able to use all its features. The basics like open(), socket(), read(), write(), select(), poll(), etc. In addition to those, the OS specific enhancements like [SO_REUSEPORT](http://freeprogrammersblog.vhex.net/post/linux-39-introdued-new-way-of-writing-socket-servers/2) which was introduced in Linux 3.9 is amazingly useful and not available to Java users. Also unix domain sockets including their extended capabilities like being able to [find information about the process on the other end](http://welz.org.za/notes/on-peer-cred.html) and being able to [pass open file descriptors over them](http://infohost.nmt.edu/~eweiss/222_book/222_book/0201433079/ch17lev1sec4.html).

We know that [Oracle are looking into this too](http://www.oracle.com/technetwork/java/jvmls2013nutter-2013526.pdf).

#### libgit2

Manipulate git repositories. Build versioned data-stores directly on the git model. Using version control backends directly in apps is an exciting application direction, but accessing git from Java is incredibly painful, and [libgit2](https://libgit2.github.com/) capability would be great.

#### Browser engines

Namely [Blink](http://www.chromium.org/blink/public-c-api), [WebKit](http://www.paulirish.com/2013/webkit-for-developers/) and/or [WebCore](http://en.wikipedia.org/wiki/WebKit#WebCore), [Gecko](https://wiki.mozilla.org/Gecko:Home_Page). Allow Java apps to run complete headless or visible browsers in their apps and fully watch and manipulate the live DOM, provide services to web-pages, etc without complicated inter-process coordination.

#### Alternate windowing frameworks

Swing is controversial. Even with advanced look & feels it always looks out of place on a native desktop and doesn't fit just right with other things. [SWT](http://www.eclipse.org/swt/) uses native platform libraries that tightly integrate with desktop, but it is a gigantic beast. We would be interested to see if other native but lightweight widget libraries would excite the Java community such as [wxWidgets](http://www.wxwidgets.org/), [Fox Toolkit](http://www.fox-toolkit.org/) or [FLTK](http://www.fltk.org/index.php).  [Qt](http://qt-project.org/) too, but that could be another gigantic beast, and has some wrappers already.

#### LLVM

It would be cool to be create a Java API for generating and compiling [LLVM](http://llvm.org/) IR. There are lots of Java libraries that create bytecode on the fly (e.g. ASM), but imagine if you could generate native performance libraries on the fly too.

Sam has already mapped the C API of LLVM to Java (a subset of the larger task) and [it actually works](https://github.com/bytedeco/javacpp-presets/tree/master/llvm).

#### libusb

[Libwb](http://www.libusb.org/) C library for interop with USB. Not a job for JavaCPP, but a worthy deliverable given the cross-platform nature of it.

#### libffi

Though OpenJDK uses [libffi](https://sourceware.org/libffi/) to implement foreign-function interfaces, there's no general linkable library for this, that would be for all JavaSE versions.

#### libcap

From their website: [libpcap](http://sourceforge.net/projects/libpcap/) is a system-independent interface for user-level packet capture. libpcap provides a portable framework for low-level network monitoring. Applications include network statistics collection, security monitoring, network debugging, etc. Super-cool huh?

#### Lua

[Lua](http://www.lua.org/) is everyone's favoring game-centric embeddable scripting language.  It would be great to see it more interacting on a sort of peer-to-peer basis, [like Haskell](http://stackoverflow.com/a/10370902/523744).
    
