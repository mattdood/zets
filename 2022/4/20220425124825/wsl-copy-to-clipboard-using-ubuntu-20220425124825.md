---
path: '/2022/4/wsl-copy-to-clipboard-using-ubuntu-20220425124825'
title: 'wsl copy to clipboard using ubuntu'
date: '20220425124825'
category: 'wsl'
tags: ['ubuntu']
---

# wsl copy to clipboard using ubuntu
It took a little while for me to copy + paste from my WSL instance into the Windows
side of my computer today. I thought it would be best to write down the command to
avoid losing track of it down the road.

When trying this, I was attempting to utilize `xclip` to accomplish copying, then
later tried using Vim to copy straight to the clipboard (apparently this uses
xclip as the underlying copy strategy).

**Attempts:**
```
xclip -sel clipboard <filename>
```

**Solution:**
```
cat <filename> | clip.exe
```

