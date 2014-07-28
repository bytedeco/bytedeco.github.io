---
layout: post
title: Second release at Bytedeco
---

Today marks the second release at version 0.9 of the software suite at Bytedeco: [JavaCPP](https://github.com/bytedeco/javacpp), [JavaCPP Presets](https://github.com/bytedeco/javacpp-presets), [JavaCV](https://github.com/bytedeco/javacv), [ProCamCalib](https://github.com/bytedeco/procamcalib), and [ProCamTracker](https://github.com/bytedeco/procamtracker). Please click on the appropriate link to download and obtain more information about the changes that occurred in your favorite project.

For this release, we have been striving to add a few more C/C++ libraries that are frequently used to the set of modules under the JavaCPP Presets. I am thus happy to announce that the following new libraries are now supported:

 * [FlyCapture 2.6.x](http://ww2.ptgrey.com/sdk/flycap)
 * [flandmark 1.07](http://cmp.felk.cvut.cz/~uricamic/flandmark/)
 * [FFTW 3.3.4](http://www.fftw.org/)
 * [GSL 1.16](http://www.gnu.org/software/gsl/)
 * [LLVM 3.4.2](http://llvm.org/)
 * [Leptonica 1.71](http://www.leptonica.org/)
 * [Tesseract 3.03-rc1](https://code.google.com/p/tesseract-ocr/)

Using any of those libraries on the Java platform is now as easy and as efficient as [using JavaCV to access the functionality of OpenCV](https://github.com/bytedeco/javacv#quick-start-for-opencv-and-ffmpeg), as it has always been even before the switch to the JavaCPP Presets. For example, in the case of Tesseract, the first example on the [APIExample](https://code.google.com/p/tesseract-ocr/wiki/APIExample) wiki page maps to Java as follows:

```java
import org.bytedeco.javacpp.*;
import static org.bytedeco.javacpp.lept.*;
import static org.bytedeco.javacpp.tesseract.*;

public class TesseractDemo {
    public static void main(String[] args) {
        BytePointer outText;

        TessBaseAPI api = new TessBaseAPI();
        // Initialize tesseract-ocr with English, without specifying tessdata path
        if (api.Init(null, "eng") != 0) {
            System.err.println("Could not initialize tesseract.");
            System.exit(1);
        }

        // Open input image with leptonica library
        PIX image = pixRead("/usr/share/doc/tesseract/phototest.tif");
        api.SetImage(image);
        // Get OCR result
        outText = api.GetUTF8Text();
        System.out.println("OCR output:\n" + outText.getString());

        // Destroy used object and release memory
        api.End();
        outText.deallocate();
        pixDestroy(image);
    }
}
```

Furthermore, Jarek Sacha has prepared examples for FlyCapture 2 (that now also runs under Linux, in addition to Windows) and flandmark as part of the [JavaCV Examples](https://github.com/bytedeco/javacv-examples) repository:

 * [FlyCapture2-demo](https://github.com/bytedeco/javacv-examples/tree/master/FlyCapture2-demo)
 * [flandmark-demo](https://github.com/bytedeco/javacv-examples/tree/master/flandmark-demo)

If you have any questions, problems, or would like to contribute, but are unsure how to proceed, please feel free to share your concerns [on the mailing list](http://groups.google.com/group/javacpp-project) or via "issues" on GitHub. Enjoy and thank you for your interest!
