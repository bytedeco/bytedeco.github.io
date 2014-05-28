---
layout: default
title: Bytedeco Contribute
---

Contribute
==========

Depending on how much time and effort you are willing to spend, there are a few different ways in which you could help make this community grow. They are listed below, ordered from the easiest to the most demanding: [answering questions](#answer-questions), [reporting bugs](#report-bugs), [writing documentation](#write-documentation), [providing hardware](#provide-hardware), and [submitting code](#submit-code). Thank you for your interest in contributing!

<a id="answer-questions"></a>
Answer Questions
----------------
To ask for support, users can post their questions on a mailing list. There are currently two mailing lists:

 * [JavaCPP Group](http://groups.google.com/group/javacpp-project)
 * [JavaCV Group](http://groups.google.com/group/javacv)

The latter is intended for higher-level questions regarding JavaCV and its usage, while the first one deals with more lower-level questions regarding JavaCPP. To help others directly, please subscribe to either one or both of the mailing lists, and start answering to questions!

<a id="report-bugs"></a>
Report Bugs
-----------
When using the software, if you encounter any problems that you believe require fixing, please make sure to create new issues for the affected projects, providing as part of your reports as much detail as possible, at least as much as is required to reproduce the incorrect behavior:

 * [JavaCPP Issues](https://github.com/bytedeco/javacpp/issues)
 * [JavaCPP Presets Issues](https://github.com/bytedeco/javacpp-presets/issues)
 * [JavaCV Issues](https://github.com/bytedeco/javacv/issues)
 * [JavaCV Examples Issues](https://github.com/bytedeco/javacv-examples/issues)
 * [ProCamCalib Issues](https://github.com/bytedeco/procamcalib/issues)
 * [ProCamTracker Issues](https://github.com/bytedeco/procamtracker/issues)

<a id="write-documentation"></a>
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

<a id="provide-hardware"></a>
Provide Hardware
----------------
Since we need to deal with multiple platforms, having dedicated hardware for builds and tests can be of great relief to developers. Right now, there is not much of anything concrete with respect to automated builds, but this is something that we will eventually require, so knowing where the hardware is will be of great help.

That said, providing builds of JavaCPP Presets for more platforms, most notably `linux-arm`, is already something you could contribute.

In either case, please be sure to [contact me](mailto:contact at bytedeco.org) personally to discuss arrangements, thank you!

<a id="submit-code"></a>
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

Here is a list of coding tasks in no particular order that, as far as I know, would be most welcome by users:

 * Improving the `Parser` of JavaCPP
 * Replacing the Bash/Maven build combo of JavaCPP Presets by something better (Gradle?)
 * [Creating JavaCPP Presets](https://github.com/bytedeco/javacpp-presets/wiki/Create-New-Presets) for more C/C++ libraries (LLVM, OpenMesh, PCL, Tesseract, etc.)
 * Expanding `FFmpegFrameGrabber` and `FFmpegFrameRecorder` in JavaCV to support more features of FFmpeg, such as metadata and filtering
 * Designing and building a framework for continuous integration that could provide builds for multiple platforms and test for regression

After determining an interesting feature that you would like to implement, please make sure to create an "issue". This lets everyone know who is working on what. It also creates the occasion to have a discussion about the design before starting to code. Thank you for your cooperation!
