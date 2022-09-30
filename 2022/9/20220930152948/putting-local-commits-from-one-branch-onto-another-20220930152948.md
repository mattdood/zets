---
path: '/2022/9/putting-local-commits-from-one-branch-onto-another-20220930152948'
title: 'putting local commits from one branch onto another'
date: '20220930152948'
category: 'git'
tags: ['fixing git issues']
---

# putting local commits from one branch onto another
Sometimes when working locally we run into problems where we accidentally commit
to master locally (sorry!) and we need to replay these commits onto a feature branch.

To do so, we can check out a branch from master, then reset the master branch to the
remote checkpoint:
```bash
# Assuming we're on the master branch
# this feature branch now has our changes
git checkout -b <my feature branch name>

# Reset the master branch
git checkout master
git reset --hard HEAD
```

Alternatively, if we want to mvoe commits to an **existing** branch:
```bash
# Replay git history onto a feature branch
git checkout <my feature branch name>
git merge master

# Fix the master branch git history
git checkout master
git reset --hard HEAD # optionally we can add a ~n
                      # where "n" is the number of commits to back up

# Swap to the feature branch to continue working
git checkout <my feature branch name>
```

