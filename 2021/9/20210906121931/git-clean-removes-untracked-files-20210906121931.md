---
path: '/2021/9/git-clean-removes-untracked-files-20210906121931'
title: 'git clean removes untracked files'
date: '20210906121931'
category: 'git'
tags: ['git', 'workflow']
---

# git clean removes untracked files
Having lots of untracked files when a `git pull` fails is very annoying to clean
up before diagnosing the failure. While working with a few dozen files it can
be frustrating to do an `rm` and string together all of them.

This ended up being a silly solution, when I looked into a faster way to do
this it looks like git will handle it for you.

[More in-depth information on this is available from this tutorial.](https://linuxize.com/post/how-to-remove-untracked-files-in-git/)

Check what git wants to remove:

```bash
git clean -d -n
```

Remove interactively:

```bash
git clean -d -n -i
```

Remove from directories:

```bash
git clean -d -n some-dir/ some-other-dir/
```

Actually remove them, rather than dry-run:

```bash
git clean -d -f <anything else here>
```

Another option for untracked files:
```bash
git add .
git reset --hard HEAD
```

