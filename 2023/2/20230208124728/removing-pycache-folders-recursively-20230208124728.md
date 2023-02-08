---
path: '/2023/2/removing-pycache-folders-recursively-20230208124728'
title: 'removing pycache folders recursively'
date: '20230208124728'
category: 'python'
tags: ['linux', 'bash', 'python', 'pycache']
---

# removing pycache folders recursively
It gets annoying sometimes dealing with `__pycache__/` and it's associated
output files.

I found this great command on StackOverflow that I'd like to remember. This is
for removing `__pycache__/`, `.pyc`, and `.pyo` files.

**Checking for files that will be removed:**
```bash
find . | grep -E "(/__pycache__$|\.pyc$|\.pyo$)"
```

**Removing the files:**

```bash
find . | grep -E "(/__pycache__$|\.pyc$|\.pyo$)" | xargs rm -rf
```

