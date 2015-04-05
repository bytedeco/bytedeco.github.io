---
layout: post
title: Introducing JavaCV frame converters
---

To supplement the long-standing functionality of [`CanvasFrame`](http://bytedeco.org/javacv/apidocs/org/bytedeco/javacv/CanvasFrame.html), [`FrameGrabber`](http://bytedeco.org/javacv/apidocs/org/bytedeco/javacv/FrameGrabber.html), [`FrameRecorder`](http://bytedeco.org/javacv/apidocs/org/bytedeco/javacv/FrameRecorder.html), and their implementation classes found in JavaCV, we are introducing the concept of [`FrameConverter`](http://bytedeco.org/javacv/apidocs/org/bytedeco/javacv/FrameConverter.html) starting with version 0.11, released today. Other more minor changes have been made to all the components since version 0.10, so be sure to check out the repositories on GitHub: [JavaCPP](https://github.com/bytedeco/javacpp), [JavaCPP Presets](https://github.com/bytedeco/javacpp-presets), [JavaCV](https://github.com/bytedeco/javacv), [ProCamCalib](https://github.com/bytedeco/procamcalib), and [ProCamTracker](https://github.com/bytedeco/procamtracker).

A [`FrameConverter`](http://bytedeco.org/javacv/apidocs/org/bytedeco/javacv/FrameConverter.html), in short, allows the user to share easily the same audio samples or video image data among different APIs, but without coupling their applications to all of those APIs. For example, JavaCV currently ships with [`AndroidFrameConverter`](http://bytedeco.org/javacv/apidocs/org/bytedeco/javacv/AndroidFrameConverter.html), [`Java2DFrameConverter`](http://bytedeco.org/javacv/apidocs/org/bytedeco/javacv/Java2DFrameConverter.html), and [`OpenCVFrameConverter`](http://bytedeco.org/javacv/apidocs/org/bytedeco/javacv/OpenCVFrameConverter.html) to let users represent image data as either [`android.graphics.Bitmap`](http://developer.android.com/reference/android/graphics/Bitmap.html), [`java.awt.image.BufferedImage`](http://docs.oracle.com/javase/6/docs/api/java/awt/image/BufferedImage.html), [`IplImage`](http://bytedeco.org/javacpp-presets/opencv/apidocs/org/bytedeco/javacpp/opencv_core.IplImage.html), or [`Mat`](http://bytedeco.org/javacpp-presets/opencv/apidocs/org/bytedeco/javacpp/opencv_core.Mat.html). The plain old data class adopted by JavaCV is [`Frame`](http://bytedeco.org/javacv/apidocs/org/bytedeco/javacv/Frame.html), which does not itself depend on either Android, FFmpeg, Java 2D, or OpenCV. A user could for example grab and record frames using [`FFmpegFrameGrabber`](http://bytedeco.org/javacv/apidocs/org/bytedeco/javacv/FFmpegFrameGrabber.html) and [`FFmpegFrameRecorder`](http://bytedeco.org/javacv/apidocs/org/bytedeco/javacv/FFmpegFrameRecorder.html), without requiring anything more than FFmpeg. We could further display those frames with [`CanvasFrame`](http://bytedeco.org/javacv/apidocs/org/bytedeco/javacv/CanvasFrame.html), creating a dependency on Java 2D, or alternatively, on Android, if we transfer the frames to video memory with [`AndroidFrameConverter`](http://bytedeco.org/javacv/apidocs/org/bytedeco/javacv/AndroidConverter.html). To further process the data, one might start using [`OpenCVFrameConverter`](http://bytedeco.org/javacv/apidocs/org/bytedeco/javacv/OpenCVFrameConverter.html), automatically creating a dependency on OpenCV that was not present until that point. We intentionally designed the API to be as easy to use as possible, but at the same time as efficient as possible, eliminating data copies whenever the underlying APIs allow. A typical usage scenario might look like this:

```java
   FFmpegFrameGrabber grabber = new FFmpegFrameGrabber("video.mp4");
   AndroidFrameConverter converterToBitmap = new AndroidFrameConverter();
   OpenCVFrameConverter.ToMat converterToMat = new OpenCVFrameConverter.ToMat();

   // Grab an image Frame from the video file
   Frame frame = grabber.grab();
   // Perform a shallow copy to represent frame as a Mat
   Mat mat = converterToMat.convert(frame);
   // Do some processing on mat with OpenCV
   Mat processedMat = ...
   // Convert processedMat back to a Frame
   frame = converterToMat.convert(processedMat);
   // Copy the data to a Bitmap for display or something
   Bitmap bitmap = converterToBitmap.convert(frame);
```

It is also possible to pass a [`FrameConverter`](http://bytedeco.org/javacv/apidocs/org/bytedeco/javacv/Java2DFrameConverter.html) in a generic way to prevent unnecessary processing of data, for example:

```java
    <I> void process(FrameConverter<I> converter, I image) {
        if (someCondition) {
            Frame frame = converter.convert(image);
            // Process frame.image...
        }
    }
```

As a side note, to implement [`Java2DFrameConverter`](http://bytedeco.org/javacv/apidocs/org/bytedeco/javacv/Java2DFrameConverter.html) we used code previously found inside the [`opencv_core` helper class](http://bytedeco.org/javacpp-presets/opencv/apidocs/org/bytedeco/javacpp/helper/opencv_core.html). On Android, this was problematic because it would cause the log file to fill up with warnings about classes missing from the [`java.awt`](http://docs.oracle.com/javase/6/docs/api/java/awt/package-summary.html) package. Moving that code out fixed this annoyance. As a less happy consequence, to recover the functionality that was lost, existing users need to refactor their code based on a combination of [`Java2DFrameConverter`](http://bytedeco.org/javacv/apidocs/org/bytedeco/javacv/Java2DFrameConverter.html) and [`OpenCVFrameConverter`](http://bytedeco.org/javacv/apidocs/org/bytedeco/javacv/OpenCVFrameConverter.html). To limit these kinds of breaking changes, the features are still very limited, but in a way, this is intentional. It allows users to focus on what is missing, rather than on figuring out how to use everything. We are aware of no precedent to a framework like JavaCV that has attempted to bridge the gap between multimedia and computer vision across platforms.

In any case, we hope that overall you find this "frame processing" technique practical for your own applications, and as usual, if you have any questions, problems, or would like to contribute, but are unsure how to proceed, please feel free to share your concerns [on the mailing list](http://groups.google.com/group/javacv) or via "issues" on GitHub. Enjoy and thank you for your continued interest!
