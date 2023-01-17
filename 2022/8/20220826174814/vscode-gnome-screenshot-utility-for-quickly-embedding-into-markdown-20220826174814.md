---
path: '/2022/8/vscode-gnome-screenshot-utility-for-quickly-embedding-into-markdown-20220826174814'
title: 'vscode gnome screenshot utility for quickly embedding into markdown'
date: '20220826174814'
category: 'editors'
tags: ['vscode', 'gnome', 'markdown', 'utility']
---

# vscode gnome screenshot utility for quickly embedding into markdown
My partner recently started utilizing my [zet-cli](https://github.com/mattdood/zet-cli)
utility to take notes; however, there is a disconnect between VSCode
and the ability to quickly add screenshots into markdown files.

I have a Vim utility to quickly take a screenshot and embed a file into
my working directory that I adapted to fit this use case.

The solution was to adapt the `keybinds`, `tasks`, and `settings` files of VSCode
to allow this script to run, embed some boilerplate text, and terminate easily.
The keybind for the finished solution is `ctrl+'` to take a screenshot.

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

# Execute `gnome-screenshot` within a current working directory.
# Iterates the image filename based on the # of additional
# images already in the directory.
# Used in conjunction with Vim for quick Markdown images.

working_dir=$(pwd)

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

## VSCode setup
Using the above script, I found a few things that were needed to execute
the script and provide some boilerplate.
1. A task needs to be created in the `tasks.json` file for the **user** (not the project)
1. An extension [macros](https://github.com/geddski/macros) needs to be installed
to allow multiple commands to be run in succession
1. The `gnome-ss-vscode` macro needs to be created
1.

The user's `settings.json` file:
```json
{
    "macros": {
        "gnomeSS": [
            "editor.action.insertLineAfter", // go to new line below
            // execute screenshot task
            {
                "command": "workbench.action.tasks.runTask",
                "args": "gnome-ss-vscode"
            },
            // move to a new line
            {
                "command": "cursorMove",
                "args": {
                    "to": "wrappedLineStart",
                    "by": "wrappedLine",
                    "value": 1
                }
            },
            // output boilerplate for
            // the image to be embedded
            {
                "command": "type",
                "args": {
                    "text": "![]()"
                }
            }
        ]
    }
}
```

The user's `keybinds.json` file:
```json
[
    // Registers the macro to a keybind
    {
        "key":  "ctrl+'",
        "command": "macros.gnomeSS",
        "when": "editorTextFocus && !editorReadonly"
    }
]
```

The user's `tasks.json` file:
```json
{
    "version": "2.0.0",
    "tasks": [
        // Registers the gnome-ss-vscode task
        // and points it to the script in our local path
        {
            "label": "gnome-ss-vscode",
            "type": "shell",
            "command": "gnome-ss-vscode.sh"
        }
    ]
}
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
```markdown

My notes here

Embedded image script output:

![]()
```

