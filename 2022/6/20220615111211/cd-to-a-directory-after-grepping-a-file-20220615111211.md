---
path: '/2022/6/cd-to-a-directory-after-grepping-a-file-20220615111211'
title: 'cd to a directory after grepping a file'
date: '20220615111211'
category: 'bash'
tags: ['grep', 'find', 'dirname', 'cd', 'scripts']
---

# cd to a directory after grepping a file
I have quite a few notes generated from my [Zet-CLI](https://github.com/mattdood/zet-cli).
These notes are stored in a [time-series format](https://github.com/mattdood/zets)
which gets annoying when I need to find a specific one, then maybe change a filename
or delete a file.

To avoid going back and forth grepping, `cd`-ing into directories, then grepping again
I've discovered a little trick.

## Finding a file then cd-ing to it
To find a file and `cd` to the containing directory, I'm using this:

```bash
cd $(dirname $(find . | grep <my search string>))
```

This script does the following:
1. `find` to find all files in my current directory recursively
1. Pipe the results to `grep` to compare the filenames to my search string
1. Return the results (should be 1 thing, hopefully) to `dirname`
1. `dirname` then finds the containing directory of that file
1. Return the containing directory to `cd` to take me there

