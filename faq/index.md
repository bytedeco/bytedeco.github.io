---
layout: default
title: Bytedeco FAQ
---

FAQ
===

If you do not find answers to your questions in the list below, please do not hesitate to send a message to the appropriate mailing list:

 * [JavaCPP Group](http://groups.google.com/group/javacpp-project)
 * [JavaCV Group](http://groups.google.com/group/javacv)

How does it differ from wrappers in OpenCV, etc.?
-------------------------------------------------

[JavaCPP](https://github.com/bytedeco/javacpp) was designed for maximum performance and flexibility. It strives to map as much of C++ as the Java language can reasonably handle, offering a level of usability to native functionality unmatched by any other solutions that we are aware of. It also provides a common foundation, a set of basic classes, to increase the interoperability between different native libraries on the Java platform. Plus, its integration with standard tools such as Maven facilitates development and deployment.

Is the license business friendly? 
---------------------------------

Yes, the core of the software is licensed under the [GPLv2](http://www.gnu.org/licenses/gpl-2.0.html) with [Classpath exception](http://www.gnu.org/software/classpath/license.html), which is similar in spirit to the LGPL, but with less restrictions, so you can use it within your own commercial products without having to pay any royalties. The reason behind this choice was due to its better affinity with Android when compared to LGPL, and because that was [the license that Sun Microsystems chose when releasing the OpenJDK](http://openjdk.java.net/legal/gplv2+ce.html). Being GPL though, we expect people to contribute back changes when they are related directly to the original code, such as bug fixes, but nothing more. Enjoy!

Do you offer commercial support?
--------------------------------

Not officially yet, but if you have a need, please do not hesitate to [contact us](mailto:contact at bytedeco.org).

