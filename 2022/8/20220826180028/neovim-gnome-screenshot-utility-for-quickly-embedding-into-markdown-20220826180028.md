---
path: '/2022/8/neovim-gnome-screenshot-utility-for-quickly-embedding-into-markdown-20220826180028'
title: 'neovim gnome screenshot utility for quickly embedding into markdown'
date: '20220826180028'
category: 'editors'
tags: ['neovim', 'gnome', 'markdown', 'utility']
---

# neovim gnome screenshot utility for quickly embedding into markdown
I have been using my own note taking tool ([zet-cli](https://github.com/mattdood/zet-cli))
since June 2021. The general concept is to use markdown files as notes
and to embed any images that I require in the notes using my screenshot utility.

My primary editor is [Neovim](https://neovim.io) and requires some customization
to accomplish the task of embedding screenshots seamlessly into my notes.

## Bash script
I use a bash script that executes the `gnome-screenshot` tool with a few
parameters for the output.

The script uses the current working directory to create a screenshot,
count the number of images already in the directory, then iterate 1 more
in the filename before outputting it to the current working directory.

This file should be created then saved to the `/usr/local/bin` directory
with the name `gnome-ss-vscode.sh`.

To make it executable, run `chmod +x gnome-ss-vscode.sh`.

You will likely need to run `sudo` with the above commands.

```bash
#!/usr/bin/env bash

# Matthew Wimberly - 6-9-2021

# Execute `gnome-screenshot` within a copied directory.
# Iterates the image filename based on the # of additional
# images already in the directory.
# Used in conjunction with Vim for quick Markdown images.

working_dir=$(xclip -o -sel clip)
if [[ $working_dir != *"zets"* ]]; then
    working_dir=$HOME/Pictures
fi

# find the number of `.png`s and iterate it
img_count=$(find $working_dir -name "*.png" -type f | wc -l)
img_count_iter=$(($img_count + 1))
filename="$(date +%Y%m%d%H%M%S)-img-$img_count_iter.png"
echo $filename
full_filepath="$working_dir/$filename"

gnome-screenshot -a --border-effect=shadow -f $full_filepath

# uses xclip to pipe the full filename back
echo -n $filename | xclip -sel clip
```

## Neovim setup
The following is placed in my `init.vim` (I'm not using an `init.lua` yet).

To utilize the utility, I use `<leader>ss` to call my function, which gets my
current working directory, executes the screenshot utility with it, then
pastes some embed output.

```vimscript
" Screenshot utility with Gnome-Screenshot
function! Get_clipboard()
    let @+ = system('xclip -o -sel clip', @r)
endfunction
function! Gnome_ss()
    let @+ = expand("%:p:h")
    execute '! gnome-ss.sh'
    let clipboard = Get_clipboard()
    let home_path = $HOME
    let cleaned_path = split(@+, home_path)[0]
    let img_append = '![](./' . cleaned_path . ')'
    execute append('.', img_append)
endfunction
nnoremap <leader>ss :call Gnome_ss()<CR>
```

## Sample output
If a note is being taken in the following directory structure and the command is run
it will output a file similar to the below. The sample output is provided as
an indication of the text it inserts into the note that is currently being
edited.

Sample directory after being run:
```
2022/
    08/
        20220826174814/
            my-note-20220826174814.md
            20220826184814-img-1.png
```

Sample note contents (final line is output):
```
My notes here

Embedded image script output:

![](20220826184814-img-1.png)
```
