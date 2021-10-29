---
path: '/2021/9/vim-and-nvim-indenting-by-filetype-20210907145200'
title: 'vim and nvim indenting by filetype'
date: '20210907145200'
category: 'vim'
tags: ['vimrc', 'init.vim']
---

# vim and nvim indenting by filetype
One of the issues I had recently when working in a full stack application was
having different indentation settings for different files. Having spent most of
my time in a Python setting I didn't need anything other than 4 spaces, which
I would carry over to the other files like `.html` or `.js`.

This became annoying when working in a JS-only application so I decided to hunt
down a solution.

[Source from Reddit, the question actually had what I needed](https://www.reddit.com/r/neovim/comments/991kmv/annoying_auto_indentation_in_tex_files/)

## Settings changes
Below are my settings for HTML, Django's HTML templating language, and JavaScript.

This will change on-load depending on the buffer's filetype.

```lua
" Example Settings"
autocmd BufNewFile,BufRead *.js
        \ set filetype=javascript  |
        \ set shiftwidth=2         |
        \ set tabstop=2

autocmd BufNewFile,BufRead *.html,*htmldjango
        \ set filetype=html  |
        \ set shiftwidth=2   |
        \ set tabstop=2
```

