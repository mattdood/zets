---
path: '/2023/1/auto-committing-to-git-repos-and-the-things-we-do-for-love-20230115231025'
title: 'auto committing to git repos and the things we do for love'
date: '20230115231025'
category: 'golang'
tags: ['linux', 'git', 'automation']
---

# auto committing to git repos and the things we do for love
Recently my partner lost some files, to avoid having this happen in the future
I decided to write a tool. Most of our important personal notes are stored
in Git repositories, we like to keep them accessible on each of our machines easily.

To ensure these notes are synced with the Git remote host, I wrote [push-me](https://github.com/mattdood/push-me.git).

**This tool does a few cool things:**
* Creates a configuration file to hold relative paths to git repos that should be pushed to the remote host
* Adds a `crontab` task that executes the `push-me` binary hourly

Now, my partner only needs to edit a single configuration file to ensure that her
own personal "auto save" is enabled.

Example `.push-me-config.yml`:

```yml
repos:
    - "my-repo/path/here"
    - "my-other-repo/path/here"
```

