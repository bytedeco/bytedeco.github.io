---
layout: default
title: Contribute
---

Contribute
==========

Depending on how much time and effort you are willing to spend, there are a few different ways in which you could help make this community grow. They are listed below, ordered from the easiest to the most demanding: [answering questions](#answer-questions), [reporting bugs](#report-bugs), [writing documentation](#write-documentation), [providing hardware](#provide-hardware), and [submitting code](#submit-code). Thank you for your interest in contributing!

Answer Questions
----------------
To ask for support, users can post their questions on a mailing list. There are currently two mailing lists:

 * [JavaCPP Group](http://groups.google.com/group/javacpp-project)
 * [JavaCV Group](http://groups.google.com/group/javacv)

The latter is intended for higher-level questions regarding JavaCV and its usage, while the first one deals with more lower-level questions regarding JavaCPP. To help others directly, please subscribe to either one or both of the mailing lists, and start answering to questions!

Report Bugs
-----------
When using the software, if you encounter any problems that you believe require fixing, please make sure to create new issues for the affected projects, providing as part of your reports as much detail as possible, at least as much as is required to reproduce the incorrect behavior:

 * [JavaCPP Issues](https://github.com/bytedeco/javacpp/issues)
 * [JavaCPP Presets Issues](https://github.com/bytedeco/javacpp-presets/issues)
 * [JavaCV Issues](https://github.com/bytedeco/javacv/issues)
 * [JavaCV Examples Issues](https://github.com/bytedeco/javacv-examples/issues)
 * [ProCamCalib Issues](https://github.com/bytedeco/procamcalib/issues)
 * [ProCamTracker Issues](https://github.com/bytedeco/procamtracker/issues)

Write Documentation
-------------------
User guides, tutorials, and other supporting documentation play an essential role in reaching a wider audience of developers. New articles can be added directly to the set of wiki pages of the projects to which you would like to contribute:

 * [JavaCPP Wiki](https://github.com/bytedeco/javacpp/wiki)
 * [JavaCPP Presets Wiki](https://github.com/bytedeco/javacpp-presets/wiki)
 * [JavaCV Wiki](https://github.com/bytedeco/javacv/wiki)
 * [JavaCV Examples Wiki](https://github.com/bytedeco/javacv-examples/wiki)
 * [ProCamCalib Wiki](https://github.com/bytedeco/procamcalib/wiki)
 * [ProCamTracker Wiki](https://github.com/bytedeco/procamtracker/wiki)

APIs also need to be documented, but unlike the above, it is written with the help of Javadoc, so we need to modify the source code instead. To contribute API documentation as part of the source code, please refer to the [Submit Code](#submit-code) section below.

Provide Hardware
----------------
Since we need to deal with multiple platforms, having dedicated hardware for builds and tests can be of great relief to developers. Right now, there is not much of anything concrete with respect to automated builds, but this is something that we will eventually require, so knowing where the hardware is will be of great help.

That said, providing builds of JavaCPP Presets for more platforms, most notably `linux-arm`, is already something you could contribute.

In either case, please be sure to [contact us](mailto:contact at bytedeco.org) personally to discuss arrangements, thank you!

Submit Code
-----------
Last but not least, contributions of new code to add features, provide samples, clarify comments, fix bugs, or enhance the functionality of the software are highly welcome! After forking a project you are interested in, please make sure to send "pull requests" as required:

 * [JavaCPP Pull Requests](https://github.com/bytedeco/javacpp/pulls)
 * [JavaCPP Presets Pull Requests](https://github.com/bytedeco/javacpp-presets/pulls)
 * [JavaCV Pull Requests](https://github.com/bytedeco/javacv/pulls)
 * [JavaCV Examples Pull Requests](https://github.com/bytedeco/javacv-examples/pulls)
 * [ProCamCalib Pull Requests](https://github.com/bytedeco/procamcalib/pulls)
 * [ProCamTracker Pull Requests](https://github.com/bytedeco/procamtracker/pulls)

### Project Ideas

Here is a list of coding tasks in no particular order that, in all likelihood, would be most welcome by users:

 * Improving the `Parser` of JavaCPP
 * Replacing the Bash/Maven build combo of JavaCPP Presets by something better (Gradle?)
 * [Creating JavaCPP Presets](https://github.com/bytedeco/javacpp-presets/wiki/Create-New-Presets) for more C/C++ libraries (FFTW, GSL, LLVM, OpenNI, OpenMesh, PCL, Tesseract, etc.)
 * Expanding `FFmpegFrameGrabber` and `FFmpegFrameRecorder` in JavaCV to support more features of FFmpeg, such as metadata and filtering
 * Designing and building a framework for continuous integration that could provide builds for multiple platforms and test for regression

After determining an interesting feature that you would like to implement, please make sure to create an "issue". This lets everyone know who is working on what. It also creates the occasion to have a discussion about the design before starting to code. Thank you for your cooperation!

### New Wrappers

Specific targets for wrapping, that we have in mind:

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
    
