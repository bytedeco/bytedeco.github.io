---
layout: post
title: Third release at Bytedeco
---

Today, Bytedeco releases the third major iteration of its software, synchronized at version 0.10. For more information about what changed in each software component, please be sure to check out the repositories on GitHub: [JavaCPP](https://github.com/bytedeco/javacpp), [JavaCPP Presets](https://github.com/bytedeco/javacpp-presets), [JavaCV](https://github.com/bytedeco/javacv), [ProCamCalib](https://github.com/bytedeco/procamcalib), and [ProCamTracker](https://github.com/bytedeco/procamtracker).

The most prominent innovation in this release is the addition of the [indexer package](http://bytedeco.org/javacpp/apidocs/org/bytedeco/javacpp/indexer/package-summary.html) in JavaCPP, many thanks in no small part to Viliam Durina for the lengthy discussions on this subject and for offering invaluable advice. The classes found in that package allow easy, type-safe, and efficient access to multidimensional arrays, often useful when processing numerical matrices or image data. It is so fast, it can even be used as a way to accelerate some things over what can be done with OpenCV alone – all that from the comfort of Java, without increasing code complexity! For example, OpenCV does not come with any built-in optimized functions to do alpha blending on the CPU. We need to use more primitive arithmetic functions and implement custom processing to this effect, as shown in the sample code below:

```java
import org.bytedeco.javacv.*;
import org.bytedeco.javacpp.*;
import org.bytedeco.javacpp.indexer.*;

import static org.bytedeco.javacpp.opencv_core.*;

public class Blend {

    /** Does alpha blending using high-level functions from OpenCV. */
    static void blendSlow(final Mat rgbaImg, final Mat bgrImg, final Mat dstImg) {
        final MatVector rgba = new MatVector();
        final MatVector bgr = new MatVector();
        final MatVector dst = new MatVector();
        Parallel.run(new Runnable() { public void run() { split(rgbaImg, rgba); }},
                     new Runnable() { public void run() { split(bgrImg, bgr); }},
                     new Runnable() { public void run() { split(dstImg, dst); }});

        final Mat alpha = rgba.get(3);
        final Mat beta = new Mat(alpha.rows(), alpha.cols(), CV_8UC1);
        final Mat one = new Mat(new double[] { 255 });
        subtract(one, alpha, beta);

        Parallel.loop(0, 3, 3, new Parallel.Looper() { 
            public void loop(int from, int to, int i) {
                multiply(rgba.get(2 - i), alpha, rgba.get(2 - i), 1.0/255.0, -1);
                multiply(bgr.get(i), beta, bgr.get(i), 1.0/255.0, -1);
                add(rgba.get(2 - i), bgr.get(i), dst.get(i));
            }
        });
        merge(dst, dstImg);
    }

    /** Does alpha blending with high-performance Indexer from JavaCPP. */
    static void blendFast(final Mat rgbaImg, final Mat bgrImg, final Mat dstImg) {
        final ByteIndexer rgbaIdx = rgbaImg.createIndexer();
        final ByteIndexer bgrIdx = bgrImg.createIndexer();
        final ByteIndexer dstIdx = dstImg.createIndexer();
        final int rows = rgbaImg.rows(), cols = rgbaImg.cols();

        Parallel.loop(0, rows, new Parallel.Looper() { 
        public void loop(int from, int to, int looperID) {
        for (int i = from; i < to; i++) {
            for (int j = 0; j < cols; j++) {
                float a = (rgbaIdx.get(i, j, 3) & 0xFF) * (1.0f/255.0f);
                float b = (rgbaIdx.get(i, j, 2) & 0xFF) * a + (bgrIdx.get(i, j, 0) & 0xFF) * (1.0f - a);
                float g = (rgbaIdx.get(i, j, 1) & 0xFF) * a + (bgrIdx.get(i, j, 1) & 0xFF) * (1.0f - a);
                float r = (rgbaIdx.get(i, j, 0) & 0xFF) * a + (bgrIdx.get(i, j, 2) & 0xFF) * (1.0f - a);
                dstIdx.put(i, j, 0, (byte)b);
                dstIdx.put(i, j, 1, (byte)g);
                dstIdx.put(i, j, 2, (byte)r);
            }
        }}});
        rgbaIdx.release();
        bgrIdx.release();
        dstIdx.release();
    }

    public static void main(String[] args) {
        // generate some random source images
        Mat rgbaImg = new Mat(480, 640, CV_8UC4);
        Mat bgrImg = new Mat(480, 640, CV_8UC3);
        Mat dst1Img = new Mat(480, 640, CV_8UC3);
        Mat dst2Img = new Mat(480, 640, CV_8UC3);

        randu(rgbaImg, new Mat(new int[] { 0, 0, 0, 0 }), new Mat(new int[] { 255, 255, 255, 255 }));
        randu(bgrImg, new Mat(new int[] { 0, 0, 0 }), new Mat(new int[] { 255, 255, 255 }));

        // warm up
        for (int i = 0; i < 100; i++) {
            blendSlow(rgbaImg, bgrImg, dst1Img);
        }
        for (int i = 0; i < 100; i++) {
            blendFast(rgbaImg, bgrImg, dst2Img);
        }

        // benchmark
        long time1 = System.nanoTime();
        for (int i = 0; i < 100; i++) {
            blendSlow(rgbaImg, bgrImg, dst1Img);
        }
        long time2 = System.nanoTime();
        for (int i = 0; i < 100; i++) {
            blendFast(rgbaImg, bgrImg, dst2Img);
        }
        long time3 = System.nanoTime();
        System.out.println("blendSlow(): " + (time2 - time1) / 100000000.0f + " ms");
        System.out.println("blendFast(): " + (time3 - time2) / 100000000.0f + " ms");

        // compare
        ByteIndexer dst1Idx = dst1Img.createIndexer();
        ByteIndexer dst2Idx = dst2Img.createIndexer();
        int rows = bgrImg.rows(), cols = bgrImg.cols(), channels = bgrImg.channels();
exit:
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                for (int k = 0; k < channels; k++) {
                    int val1 = dst1Idx.get(i, j, k) & 0xFF;
                    int val2 = dst2Idx.get(i, j, k) & 0xFF;
                    if (Math.abs(val1 - val2) > 1) {
                        System.out.println(val1 + " != " + val2 + " at (" + i + ", " + j + ")");
                        break exit;
                    }
                }
            }
        }
        System.exit(0);
    }
}
```

In this case, the `blendSlow()` method uses OpenCV functions to perform alpha blending, while `blendFast()` makes use of `Indexer` objects to obtain similar results. Both exploit multithreading to some extent via the `Parallel` class found in JavaCV. However, `blendFast()` is much faster. On my machine (Intel Core i7-3632QM CPU @ 2.20GHz, Fedora 20, GCC 4.8.3, and OpenJDK 8) the `main()` method above outputs something like the following:

```
blendSlow(): 5.623936 ms
blendFast(): 1.42263 ms
```

So, the version using `Indexer` objects runs almost 4 times faster! This is because it allows the user to save on memory bandwidth by keeping intermediate values in cache memory, something that cannot be done with the batch operations found in OpenCV.

I hope you find this functionality useful, and as usual, if you have any questions, problems, or would like to contribute, but are unsure how to proceed, please feel free to share your concerns [on the mailing list](http://groups.google.com/group/javacpp-project) or via "issues" on GitHub. Enjoy and thank you for your continued interest!
