---
path: '/2022/1/bulk-renaming-files-with-the-rename-utility-in-linux-20220131221630'
title: 'bulk renaming files with the rename utility in linux'
date: '20220131221630'
category: 'linux'
tags: ['ubuntu', 'bash', 'homelab']
---

# bulk renaming files with the rename utility in linux
I've found that working with file renaming utilities has become quite tedious with my
Plex server at home.

Often times when things are **acquired** they'll have non-standardized naming
formats that our [Radarr](https://radarr.video/) and [Sonarr](https://sonarr.tv/)
don't know how to handle.

For example:
```
'(Provider name) Show Name - 001 (1080p)(Some other junk here).mkv'
```

## The issue
Plex doesn't know how to handle edge cases when renaming, neither do the renaming
utilities that Sonarr and Radarr have equipped.

This leads to a significant amount of manual intervention when working in larger
repos of files that we need to scan.

## The solution
The `rename` utility that comes in our linux distro gives us the ability to use
[Sed replace](https://www.usessionbuddy.com/post/sed-replace-examples/).

When working with rename, we're able to use regular expressions and general
find/replace functionality to rename files in bulk.

Example:
```
# see the options
rename --help

# use rename with no operations, just showing what it will do
# also use verbose to show extra detail
rename <your pattern> <your filename pattern to do this on> -n --verbose

# taking this result, let's add a season number and the episode qualifier:
# '(Provider name) Show Name - 001 (1080p)(Some other junk here).mkv'
rename 's/- /- s01e/' -n --verbose

>>> '(Provider name) Show Name - 001 (1080p)(Some other junk here).mkv', '(Provider name) Show Name - s01e001 (1080p)(Some other junk here).mkv'

# now we run the command on a file without the no operation flag
rename 's/- /- s01e/' --verbose
```

We can actually do the same as the above but with regex, this allows us to do things
like matching specific numbers or sets of characters (i.e., `[0-9]` for numbers).

I recommend using a regex builder to create and test, I use [Regexr](https://regexr.com/).

