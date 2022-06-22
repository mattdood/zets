---
path: '/2022/6/github-repo-tagging-20220622155711'
title: 'github repo tagging'
date: '20220622155711'
category: 'git'
tags: ['github', 'versioning', 'cicd']
---

# github repo tagging
For personal projects I use a tagging system to trigger CICD pipelines that release
to either test/dev/prod stages.

To create these tags I use a manual Git tagging operation, then push that tag to
GitHub.

For rollbacks I can also delete the tag, essentially removing the release.

```bash
# Creating
git tag <your tag here, I use vX.X.X>
git push origin <your tag>

# Deleting
git tag -d <your tag here>
git push origin :<your tag here> # the colon is required
```

