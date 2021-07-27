---
path: '/2021/7/remove-cached-gitignore-files-20210726220807'
title: 'remove cached gitignore files'
date: '20210726220807'
category: 'git'
tags: ['gitignore', 'git']
---

# remove cached gitignore files
Sometimes I'll add things to my `.gitignore` after the fact as my needs change.

Removing these files from the git cache will allow the `.gitignore` to ignore them
going forward when you make commits.

I found this StackOverflow answer when struggling to remember the caching that
git uses. Code below, [answer is here](https://stackoverflow.com/a/34435207/12387496)

```bash
# do the cache removal on folders if you have submodules
# I found the submodule updates were annoying to re-add
# so just do it one by one for big submodule repos

git rm -r --cached .
git add .
git commit -m "Drop files from .gitignore"
```

