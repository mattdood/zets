---
path: '/2021/06/execute-simple-scripts-from-vim-20210608234758'
title: 'Execute Simple Scripts from Vim'
date: '20210608234758'
category: 'vim'
tags: ['vim', 'scripts', 'terminal']
---

# execute simple scripts from vim
I've been running into a few scenarios where I want to be able to execute the
script I'm working on without having to change to another tmux pane.

It looks like this is a solved problem with:
```vim
:w !bash
:w | !bash % " this does the same, writing the entire file to the buffer
:w !sh
:w !python
" etc.
```

[Stackoverflow question](https://vi.stackexchange.com/questions/10209/execute-current-buffer-as-bash-script-from-vim)

