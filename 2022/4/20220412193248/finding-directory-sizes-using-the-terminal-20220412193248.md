---
path: '/2022/4/finding-directory-sizes-using-the-terminal-20220412193248'
title: 'finding directory sizes using the terminal'
date: '20220412193248'
category: 'ubuntu'
tags: ['devops']
---

# finding directory sizes using the terminal
Finding directory sizes is important when needing to gather information about
filesystems.

Resources:
[`du` command](https://www.geeksforgeeks.org/du-command-linux-examples/)

Example with `-h` for human readability:
```
du -h /path/to/directory
du -hs . # current directory, summarized
```

Output:
![Example output of a du -hs .](./20220412193455-img-1.png)

**Note:** The `-s` flag summarizes.

Example with `-hs` to sort:
```
du -hs . | sort -h
```

This will yield information sorted largest -> smallest in a human readable format.

Output:
![Example output of du -hs . | sort -h](./20220412193633-img-2.png)

Another useful trick would be to add exclusions (like `.git/`):
```
# greps can be chained together
du -hs . | sort -h | grep -v <exclusion> | grep -v <exclusion> | ...
```

Output:
![Example output of du -hs . | sort -h | grep -v .git](./20220412193633-img-2.png)

