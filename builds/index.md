---
layout: default
title: Builds
---

<style>
table{
    border-collapse: collapse;
    border-spacing: 0;
    border:2px solid #000000;
}

th{
    border:2px solid #000000;
    padding: 3px;
}

td{
    border:1px solid #000000;
    padding: 3px;
}
</style>

Builds
======

A Jenkins CI server provides builds for the JavaCPP Presets, building across a range of platform targets and uploading snapshots. The current build status for this targets is below, with the tail of log files available to assist in any debugging.


|------------+-----------------------+---------------------+-----------------|---------|
| State | Target | Last Failed Build | Last Successful Build | Build Log |
|:----------:|-----------------------|---------------------|-----------------|---------|
| <img src="SUCCESS.png" width="20" height="20" /> |Presets-Android|15-12-2016 19:12:232 |15-12-2016 21:12:07| [Log](Presets-Android.log)|
| <img src="FAILURE.png" width="20" height="20" /> |Presets-Linux64|20-12-2016 13:12:940 | 17-12-2016 22:12:323| [Log](Presets-Linux64.log)|
| <img src="SUCCESS.png" width="20" height="20" /> |Presets-Linux32|20-12-2016 19:12:450|20-12-2016 19:12:605|[Log](Presets-Linux32.log)|
| <img src="SUCCESS.png" width="20" height="20" /> |Presets-LinuxArmhf|15-12-2016 17:12:314|20-12-2016 13:12:865|[Log](Presets-LinuxArmhf.log)|
| <img src="FAILURE.png" width="20" height="20" /> |Presets-Mac64|20-12-2016 10:12:184 | 01-12-2016 20:12:304 |[Log](Presets-Mac64.log)|
| <img src="SUCCESS.png" width="20" height="20" /> |Presets-PPC64LE|01-12-2016 20:12:369|25-11-2016 14:11:850|[Log](Presets-PPC64LE.log)|
| <img src="FAILURE.png" width="20" height="20" /> |Presets-Windows32|20-12-2016 15:12:517 | 16-12-2016 12:12:472 |[Log](Presets-Windows32.log)|
| <img src="FAILURE.png" width="20" height="20" /> |Presets-Windows64|15-12-2016 22:12:610 | 16-12-2016 09:12:638 |[Log](Presets-Windows64.log)|
| <img src="SUCCESS.png" width="20" height="20" /> |Presets-Linux64-OpenJDK9|21-12-2016 10:12:21|21-12-2016 10:12:225|[Log](Presets-Linux64-OpenJDK9.log)|
|------------+-----------------------+---------------------+-----------------|---------|



