---
path: '/2021/8/github-actions-workflow-and-scheduling-20210819172353'
title: 'github actions workflow and scheduling'
date: '20210819172353'
category: 'git'
tags: ['github', 'github actions', 'git']
---

# github actions workflow and scheduling
Working with GitHub actions more seriously recently had lead me to a few conclusions:
1. Not all repos need to have an "on push" or "on pull" action.
1. Scheduling for submodules is a great way to keep parent repos updated.
    1. Useful dependent upon whether or not the submodules have breaking dependencies.
1. All workflows should have a manual execution option.
    1. This is good outside solely testing.

Example GitHub Action snippet:
```yaml

name: Example Action
on:
  schedule:
  # Run daily at midnight
  - cron: '0 0 * * *'

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

```

