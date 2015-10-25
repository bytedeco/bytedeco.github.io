---
layout: post
title: Moving to Java SE 7
---

A few months have already passed since the last release, encouraging us to create a new one, which we have just done! Version 1.1 of [JavaCPP](https://github.com/bytedeco/javacpp), [JavaCPP Presets](https://github.com/bytedeco/javacpp-presets), [JavaCV](https://github.com/bytedeco/javacv), [ProCamCalib](https://github.com/bytedeco/procamcalib), and [ProCamTracker](https://github.com/bytedeco/procamtracker) are now available, and they depend on Java SE 7. We felt that since everyone is now comfortable with Java SE 8, it was time to drop compatibility with Java SE 6. :) Seriously, the main reason behind the change was to provide support for the [try-with-resources construct](https://docs.oracle.com/javase/tutorial/essential/exceptions/tryResourceClose.html), instead of relying solely on the garbage collector to imitate C++-like memory management semantics, aka "Resource Acquisition Is Initialization (RAII)". This required making the `Pointer` class implement the `AutoCloseable` interface, a tiny but important interface. Many thanks to Adam Gibson and Cyprien Noel for having successfully convinced me to make this change. Android also provides that interface since version 4.0, covering more than 95% of all Android users at the time of this writing, according to [Android Dashboards](http://developer.android.com/about/dashboards/). So, the choice was not so hard to make after all, and JavaCPP now requires Android 4.0.

That said, what does try-with-resources gets us anyway? It provides a user-friendly way to release resources in a deterministic manner, something that a lot of C++ libraries take for granted. There is no guarantees that the garbage collector will ever run. It only cares about memory allocated on the Java heap, and if we allocate chunks of memory only from the native heap, it might decide to never run, a situation that can easily become problematic. Also, we cannot predict on which thread memory eventually gets deallocated. We cannot force any given thread used for an allocation to come back at some point for deallocation: It might disappear at any time without any warning. The point is, for more than a few reasons, people came up with this concept to provide services garbage collection was unable to provide. As a concrete example, in the traditional paradigm, there are occasions when we would write the following:

```java
    MyPointer data = new MyPointer();
    try {
        // use data...
    } finally {
        data.deallocate();
    }
```

With try-with-resources, we can rewrite the logic above into a single statement like this:

```java
    try (MyPointer data = new MyPointer()) {
        // use data ...
    }
```

A lot cleaner, and thus a lot less error-prone. Exceptions also behave better, but that is about the gist of it. By the way, this also works with native smart pointers such as `boost::shared_ptr` (Boost), `std::shared_ptr` (C++11), `cv::Ptr` (OpenCV), and others. JavaCPP provides a new transparent bridge to any such references by holding on to a set of two pointers for each native object: the actual pointer of the object to access the data and call functions, and an "owner pointer" corresponding to a smart pointer allocated on the heap, which gets accessed only during deallocation when applying the `delete` operator. Check the documentation of the [`@SharedPtr`](http://bytedeco.org/javacpp/apidocs/org/bytedeco/javacpp/annotation/SharedPtr.html) annotation and the associated C++ template `SharedPtrAdapter` for more information.

On top of that, `Pointer` now also checks for the "org.bytedeco.javacpp.nopointergc" system property, and if "true", disables completely the garbage collector safety net, potentially saving a significant amount of time for some applications. To make sure that yours does not rely on the garbage collector for any deallocation, we have also added debug messages that are logged when a `Pointer` gets allocated, collected as garbage, and eventually deallocated. They can be captured by setting the "org.bytedeco.javacpp.logger" system property to "slf4j", and by setting the log level to "debug", for example, via the "org.slf4j.simpleLogger.defaultLogLevel" system property in the case of `SimpleLogger` from [SL4J](http://www.slf4j.org/).

In closing, let us give credit where credit is due. Cyprien Noel was the one that not only brought up all these ideas, but helped to implement them, and tested them out for their own framework of [Caffe-on-Spark](http://yahoohadoop.tumblr.com/post/129872361846/large-scale-distributed-deep-learning-on-hadoop). Discussions with Adam Gibson were also extremely fruitful, providing valuable feedback. They have since adopted JavaCPP for their own use as part of [Deeplearning4j](http://deeplearning4j.org/). Though grateful to them and everyone else who helped out, there is still much work to be done. If you are interested by where this is going, or would like to make your own recommendations and contributions, be sure to contact us via the [mailing list from Google Groups](http://groups.google.com/group/javacpp-project), [issues on GitHub](https://github.com/bytedeco/javacpp/issues), or [the chat room at Gitter](https://gitter.im/bytedeco/javacpp). Thank you for your interest, and enjoy!
