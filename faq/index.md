---
layout: default
title: FAQ
---

FAQ
===

If you do not find answers to your questions in the list below, please do not hesitate to send a message to the appropriate mailing list:

 * [JavaCPP Group](http://groups.google.com/group/javacpp-project)
 * [JavaCV Group](http://groups.google.com/group/javacv)


How does it compare to other tools for Java (JNA, JNR, etc)?
------------------------------------------------------------

JavaCPP is currently pretty much the only tool specialized for Java that works with C++ *and* matches the performance of manually written JNI. The table below summarizes the main differences between other popular tools available.

|                                                  | &ensp; C &ensp; | &nbsp; C++ &nbsp; | Java SE 7+ | Android | &nbsp; iOS &nbsp; | GraalVM<br>Native | JPMS<br>jlink |  OSGi   | Presets |   Speed     |
|--------------------------------------------------|:---------------:|:-----------------:|:----------:|:-------:|:-----------------:|:-----------------:|:-------------:|:-------:|:-------:|:------------|
| [JNA](https://github.com/java-native-access/jna) | &#9989;         | &mdash;           | &#9989;    | &#9989; | &mdash;           | &mdash;           | &mdash;       | &#9989; | &mdash; | &#8810; JNI |
| [JNR](https://github.com/jnr)                    | &#9989;         | &mdash;           | &#9989;    | &mdash; | &mdash;           | &mdash;           | &mdash;       | &#9989; | &mdash; | &asymp; JNI |
| [Panama](http://jdk.java.net/panama/)            | &#9989;         | &mdash;           | &mdash;    | &mdash; | &mdash;           | &mdash;           | &#9989;       | &mdash; | &mdash; | &asymp; JNI |
| [JavaCPP](https://github.com/bytedeco/javacpp)   | &#9989;         | &#9989;           | &#9989;    | &#9989; | &#9989;           | &#9989;           | &#9989;       | &#9989; | &#9989; | &asymp; JNI |

Contributions to the table are welcome! Please send a pull request with your new rows and/or columns to the [bytedeco/bytedeco.github.io](https://github.com/bytedeco/bytedeco.github.io) repository.


Are you really trying to parse C++? That sounds insane.
-------------------------------------------------------
Unlike other tools such as [SWIG](http://www.swig.org/) or [BridJ](https://code.google.com/p/bridj/), we are not attempting to support C++ per se, but merely the subset required to access the API of libraries from the header files, and only what is actually used in the wild by actual C++ libraries. However, until now, no attempt has been made to try and understand what that subset might be, or how it could be mapped to Java. Our approach consists in developing [JavaCPP](https://github.com/bytedeco/javacpp) as prototype, adapting it as appropriate for as many C++ libraries as possible, finding new tricks to map most naturally the required features of C++ to Java along the way, and hopefully end up one day with a clearer understanding of what we need to map and how. Our approach has not failed (yet). This is what differentiates us from past (failed, in our opinion) attempts. So, technically the answer to the question is "no": We are trying to support the parts of C++ as used in existing header files that are useful to access native libraries, not the whole of C++.


How does it differ from wrappers in OpenCV, TensorFlow, etc?
------------------------------------------------------------
[JavaCPP](https://github.com/bytedeco/javacpp) was designed for maximum performance and flexibility. It strives to map as much of C++ as the Java language can reasonably handle, offering a level of usability to native functionality unmatched by any other solutions that we are aware of. It also provides a common foundation, a set of basic classes, to increase the interoperability between different native libraries on the Java platform. Plus, its integration with standard tools such as Maven facilitates development and deployment. Bytedeco also provides builds with support for CUDA, MKL, and Python, enabled as optional extensions. For compatibility, the official Java APIs of the libraries are bundled as well.


Is the license business friendly? 
---------------------------------
Yes, the core of the software is licensed under the [Apache License, Version 2.0](http://www.apache.org/licenses/LICENSE-2.0), or the [GPLv2](http://www.gnu.org/licenses/gpl-2.0.html) with [Classpath exception](http://www.gnu.org/software/classpath/license.html): You are free to choose. The latter is similar in spirit to the LGPL, but with less restrictions, so either way you can use it within your own commercial products without having to pay any royalties. The reason behind this choice was due to their better affinity with Android and the industry in general when compared to LGPL, and because Sun Microsystems provided a precedent by licensing software such as the [OpenJDK](http://openjdk.java.net/legal/gplv2+ce.html) and [NetBeans](https://netbeans.org/cddl-gplv2.html) in the same way leaving the final choice with the user. Still, we expect people to contribute back changes when they are related directly to the original code, such as bug fixes, but nothing more. Enjoy!


What is available in the Maven Central Repository?
--------------------------------------------------
Take a look, for example, at the presets for OpenCV: [Search Central for "org.bytedeco opencv"](http://search.maven.org/#search%7Cga%7C1%7Corg.bytedeco%20opencv). The gist of it is all there - Android, iOS, Linux, Mac OS X, Windows. ARM, ARM64, POWER, x86, and x86_64 permutations too. With and without CUDA (GPU). Naturally, the artifacts are quite big, but we hope they are ready to go for many. We uploaded that for the benefit of all, but it is also possible that you have a version of, say, Linux that's more specialized than we've targeted here - in which case you might want to build the presets yourself for your own Maven repository.


What is on your to-do list?
---------------------------
* More presets (yet to enumerate)
* Working through upper limits of the parser, as we encounter them
* Anything on the [contribute](../contribute/) page


What about thread safety and reentrant aspects of the presets?
--------------------------------------------------------------
At this stage, we are not able to guarantee that presets will function as you would hope in a multithreaded way. We're also unable to state that presets are perfectly reentrant. It would be great to set up test harnesses, to somehow indicate (if not prove) that usage characteristics are what we expect, but we're somewhat overstretched as it is.


Do you offer commercial support?
--------------------------------
Not officially yet, but if you have a need, please do not hesitate to [contact us](mailto:contact at bytedeco.org).

