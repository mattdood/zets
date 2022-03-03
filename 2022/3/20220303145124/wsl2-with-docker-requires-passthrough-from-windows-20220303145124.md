---
path: '/2022/3/wsl2-with-docker-requires-passthrough-from-windows-20220303145124'
title: 'wsl2 with docker requires passthrough from windows'
date: '20220303145124'
category: 'docker'
tags: ['wsl2', 'windows', 'docker', 'ubuntu']
---

# wsl2 with docker requires passthrough from windows
Installing Docker within the WSL2 environment (mine runs Ubuntu) requires a passthrough
due to some unsupported things running on a Windows host (from what I can understand in the docs).

To remedy this, I followed [this tutorial on the Docker website](https://docs.docker.com/desktop/windows/wsl/)
then was able to boot into my WSL instance and run Docker myself.

