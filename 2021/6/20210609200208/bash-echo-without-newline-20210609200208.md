---
path: '/2021/06/bash-echo-without-newline-20210609200208'
title: 'Bash Echo without Newline'
date: '20210609200208'
category: 'bash'
tags: ['bash', 'scripting']
---

# bash echo without newline
Today I ran into an issue with Bash scripting where I had a carriage return
piped back from the end of a utility script.

The issue:
```bash
# Pipes to the clipboard
echo $some_var | xclip -o -sel clip
```

This would return a `^@` at the end of my line in Vim. Apparently a carriage
return is appended to the end of bash `echo` commands, using `-n` removes this.

```bash
# Corrected clipboard
echo -n $some_var | xclip -o -sel clip
```
