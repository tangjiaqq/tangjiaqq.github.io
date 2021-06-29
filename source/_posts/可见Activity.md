---
title: 可见Activity(当前页面的Activity名称)
date: 2019-06-20 17:37:54
tags:
description: 可见Activity(当前页面的Activity名称)
categories:
- Android
---

```shell
Win平台
adb shell dumpsys activity | grep "mFocusedActivity" 查看顶层Activity  <8.0 
adb shell dumpsys activity | grep "mResumedActivity" 查看顶层Activity  8.0>=
Linux平台
adb shell dumpsys activity | findstr "mFocusedActivity" 查看顶层Activity  <8.0
adb shell dumpsys activity | findstr "mResumedActivity" 查看顶层Activity  8.0>=

Android 如何快速定位当前页面是哪个Activity or Fragment
(1)查看当前Activity ：adb shell "dumpsys window w | grep name="
(2)查看当前栈顶的Activity ：adb shell dumpsys activity | grep "mFocusedActivity"
(3)查看当前栈顶的Activity的Fragment ：adb shell dumpsys activity your.package.name  
或者： adb shell dumpsys activity top
```

