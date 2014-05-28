---
layout: post
title: First release at Bytedeco
---

Welcome to Bytedeco! The new home of [JavaCPP](https://github.com/bytedeco/javacpp), [JavaCPP Presets](https://github.com/bytedeco/javacpp-presets), [JavaCV](https://github.com/bytedeco/javacv), [ProCamCalib](https://github.com/bytedeco/procamcalib), and [ProCamTracker](https://github.com/bytedeco/procamtracker), hosted at [GitHub](https://github.com). This post also coincides with their latest releases at version 0.8. Please click on the appropriate link to download and obtain more information about your favorite project. Further, all binary artifacts are now made available through the [Maven Central Repository](http://search.maven.org/#search|ga|1|bytedeco).

The projects under this new version number also come with a few big changes. First, the group of the artifacts and the package of the classes have been renamed to `org.bytedeco`. Second, JavaCV is now based on the JavaCPP Presets, which comes with an interface that maps the functionality of OpenCV more closely to its original C++ API, among other things. This is both a good thing, and a bad thing, because we lose some backward compatibility with previous versions of JavaCV. In the long run though, providing interfaces to C++ libraries that map as closely as possible to the original API is easier for both the mechanical parser and the ultimate user, so I feel that was the right choice to make. 

That said, to make the transition a bit less painful, here are a few tips to help you adapt your code:

1. In your build files, replace the `com.googlecode.javacpp` and `com.googlecode.javacv` groups with `org.bytedeco`. You may also have to add a couple of additional dependencies based on the new organization of the artifacts for the JavaCPP Presets.
2. Rename import statements based on the following mapping:
 - `com.googlecode.javacpp`     &rArr; `org.bytedeco.javacpp`
 - `com.googlecode.javacv.cpp`  &rArr; `org.bytedeco.javacpp`
 - `com.googlecode.javacv`      &rArr; `org.bytedeco.javacv`
3. For code that uses the C++ API of OpenCV, adjust the object types as follows:
 - `CvMat` and `IplImage` &rArr; `Mat`
 - `CvRect`       &rArr; `Rect`
 - `CvPoint`      &rArr; `Point`
 - `CvPoint2D32f` &rArr; `Point2f`
 - `CvPoint3D32f` &rArr; `Point3f`
 - `CvPoint2D64f` &rArr; `Point2d`
 - `CvPoint3D64f` &rArr; `Point3d`
 - `CvSize`       &rArr; `Size`
 - `CvSize2D32f`  &rArr; `Size2f`
 - `CvBox2D`      &rArr; `RotatedRect`
 - `CvScalar`     &rArr; `Scalar`  
The latter come with constructors to wrap the former, in addition to `as<OriginalTypeName>()` methods that map to the corresponding cast operators. Neither operations requires large amounts of data to be copied, so making the switch should not be too difficult.

There are a few other things here and there, but nothing else with major consequences, as far as I know. If you run up against something you are having a hard time solving though, please share your experience with everyone [on the mailing list](http://groups.google.com/group/javacv). I am sure a kind soul will help you out.

So, what next? At the moment, other than making news releases and a few useful blog posts every now and then, I am not planning anything in particular for this site, but for the future, who knows...
