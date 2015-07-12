---
layout: post
title: Now offering software under the Apache License
---

To facilitate its adoption in commercial applications such as [Deeplearning4j](http://deeplearning4j.org/), the core software of [JavaCPP](https://github.com/bytedeco/javacpp), [JavaCPP Presets](https://github.com/bytedeco/javacpp-presets), and [JavaCV](https://github.com/bytedeco/javacv) has been relicensed to offer users the [Apache License, Version 2.0](http://www.apache.org/licenses/LICENSE-2.0) as a new choice of license. No large technical changes has otherwise occurred, but we believe these core components have acquired a stable enough existence to merit an increment in their major version number to 1.0. Moreover, this way we keep a meaningful relationship between our version numbers and the ones of [OpenCV](http://opencv.org/), which has recently seen large changes in its API and has been updated to version 3.0.

In other news, we now provide [presets for CUDA](https://github.com/bytedeco/javacpp-presets/tree/master/cuda), mapping close to the entirety of its API, including [cuDNN](https://developer.nvidia.com/cudnn), for which no other wrappers that we are aware of currently exist. We hope that, along with the [presets for Caffe](https://github.com/bytedeco/javacpp-presets/tree/master/caffe), which are as far as we know also still a unique offering of ours, this will provide some useful tools to the new exciting world of deep learning.

As usual, if you have any questions, problems, or would like to contribute, but are unsure how to proceed, please feel free to share your concerns on the [mailing list of JavaCPP](http://groups.google.com/group/javacpp-project), on the [one for JavaCV](http://groups.google.com/group/javacv), or via "issues" on GitHub. We are looking forward to work with you in the future. Have fun!
