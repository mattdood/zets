---
path: '/2021/06/raspberri-pi-led-pomodoro-20210616224115'
title: 'Raspberry Pi LED Pomodoro'
date: '20210616224115'
category: 'project'
tags: ['raspberry pi', 'pomodoro', 'project']
---

# raspberry pi LED pomodoro
I had an idea to make a Raspberry Pi project that would control lights in my office
using a Raspberry Pi Zero.

## Structure
* Have a Raspberry Pi tied to an LED light strip
* Run a custom `socketserver` that accepts commands from a remote local server
* Have an LED control program that would handle a pomodoro configuration

## Pomodoro setup
* Red - working period
* Yellow - break period
* Green - Free time

