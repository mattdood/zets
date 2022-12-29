---
path: '/2022/12/git-cli-usage-with-different-working-directory-20221228191911'
title: 'git CLI usage with different working directory'
date: '20221228191911'
category: 'git'
tags: ['git', 'version control']
---

# git CLI usage with different working directory
Just learned that you can call Git from the CLI with different working directory
context. This was helpful when making my typical "git wrapper" commands on
one of my CLIs.

```bash
git -C <path> <subcommmand>
```

An example of this would be:
```bash
git -C /home/matthew/zets/ add
```

Which would run `git add` on my `/home/matthew/zets/.git` (or `~/zets/.git`).

