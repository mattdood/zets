---
path: '/2023/1/finding-text-with-line-numbers-using-recursive-grep-20230126131916'
title: 'finding text with line numbers using recursive grep'
date: '20230126131916'
category: 'linux'
tags: ['grep', 'text search']
---

# finding text with line numbers using recursive grep
A helpful command that I put together to find some information using `grep`
when trying to find common lines (to change) across different projects.

```bash
grep -rnI "my search string pattern here" --include="*.<my file extension here>"
```

The below example would find all references to the Terraform module `autotune`
across my projects. This returns the line number and file name.

```bash
grep -rnI "git::https://github.com/mattdood/autotune" --include="*.tf"
```

Additionally, we could apply a sort to this by piping, though this removes the color output.

```bash
grep -rnI "git::https://github.com/mattdood/autotune" --include="*.tf" | sort
```

