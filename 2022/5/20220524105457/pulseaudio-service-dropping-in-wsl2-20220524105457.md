---
path: '/2022/5/pulseaudio-service-dropping-in-wsl2-20220524105457'
title: 'pulseaudio service dropping in wsl2'
date: '20220524105457'
category: 'linux'
tags: ['wsl2', 'audio']
---

# pulseaudio service dropping in wsl2
Occassionally when working in my WSL2 environment I've noticed that audio will
not be passed to my Windows default output device.

The issue seems to occur more frequently when the WSL2 instance was left running
after the computer has gone to sleep, or if connected audio devices were changed
at some point.

## Solution
Simply navigating to the `PulseAudio` service in the Task Manager services tab
then selecting "restart" seems to do the trick.

