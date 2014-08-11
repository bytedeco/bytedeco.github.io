---
layout: default
title: Bytedeco FAQ
---

FAQ
===

If you do not find answers to your questions in the list below, please do not hesitate to send a message to the appropriate mailing list:

 * [JavaCPP Group](http://groups.google.com/group/javacpp-project)
 * [JavaCV Group](http://groups.google.com/group/javacv)


Are you really trying to parse C++? That sounds insane.
-------------------------------------------------------
Unlike other tools such as [SWIG](http://www.swig.org/) or [BridJ](https://code.google.com/p/bridj/), we are not attempting to support C++ per se, but merely the subset required to access the API of libraries from the header files, and only what is actually used in the wild by actual C++ libraries. However, until now, no attempt has been made to try and understand what that subset might be, or how it could be mapped to Java. Our approach consists in developing [JavaCPP](https://github.com/bytedeco/javacpp) as prototype, adapting it as appropriate for as many C++ libraries as possible, finding new tricks to map most naturally the required features of C++ to Java along the way, and hopefully end up one day with a clearer understanding of what we need to map and how. Our approach has not failed (yet). This is what differentiates us from past (failed, in our opinion) attempts. So, technically the answer to the question is "no": We are trying to support the parts of C++ as used in existing header files that are useful to access native libraries, not the whole of C++.


How does it differ from wrappers in OpenCV, etc.?
-------------------------------------------------
[JavaCPP](https://github.com/bytedeco/javacpp) was designed for maximum performance and flexibility. It strives to map as much of C++ as the Java language can reasonably handle, offering a level of usability to native functionality unmatched by any other solutions that we are aware of. It also provides a common foundation, a set of basic classes, to increase the interoperability between different native libraries on the Java platform. Plus, its integration with standard tools such as Maven facilitates development and deployment.


Is the license business friendly? 
---------------------------------
Yes, the core of the software is licensed under the [GPLv2](http://www.gnu.org/licenses/gpl-2.0.html) with [Classpath exception](http://www.gnu.org/software/classpath/license.html), which is similar in spirit to the LGPL, but with less restrictions, so you can use it within your own commercial products without having to pay any royalties. The reason behind this choice was due to its better affinity with Android when compared to LGPL, and because that was [the license that Sun Microsystems chose when releasing the OpenJDK](http://openjdk.java.net/legal/gplv2+ce.html). Being GPL though, we expect people to contribute back changes when they are related directly to the original code, such as bug fixes, but nothing more. Enjoy!


What is available in the Maven Central Repository?
--------------------------------------------------
Take a look at the JavaCPP Presets 0.9 for OpenCV 2.4.9: [Artifact Details For org.bytedeco.javacpp-presets : opencv : 2.4.9-0.9](http://search.maven.org/#artifactdetails|org.bytedeco.javacpp-presets|opencv|2.4.9-0.9|jar). The gist of it is all there - Linux, Mac OS X, Windows, Android. x86, x86_64, and ARM permutations too. Naturally, the artifacts are quite big, but we hope they are ready to go for many. We uploaded that for the benefit of all, but it is also possible that you have a version of, say, Linux that's more specialized than we've targeted here - in which case you might want to build the presets yourself for your own Maven repo.


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

