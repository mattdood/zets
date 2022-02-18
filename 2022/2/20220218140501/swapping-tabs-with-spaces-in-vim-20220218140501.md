---
path: '/2022/2/swapping-tabs-with-spaces-in-vim-20220218140501'
title: 'swapping tabs with spaces in vim'
date: '20220218140501'
category: 'vim'
tags: ['vim']
---

# swapping tabs with spaces in vim
This is a quick note to reference a helpful StackOverflow post that I read.

## Scenario
I ran a [`flake8`](https://flake8.pycqa.org/) lint and had forgotten that my code
had some conflicting space/tab errors. My editor is set for spaces; however,
it was during some find/replace (`:s/<match>/<replacement>/g`) that I had
inserted tabs to split a list apart.

### SED replace I used
The replace I used was to break a list object from one line into several:
```
:s/, /,\n\t/g
```

```
# before:
list = [
    'some', item', 'here']

# after:
list = [
    'some',
    'item',
    'here']

# final cleanup:
list = [
    'some',
    'item',
    'here'
]
```

### Replacing the tabs
To remedy this, [this StackOverflow post](https://stackoverflow.com/questions/426963/replace-tabs-with-spaces-in-vim)
recommended using `:retab`, as it will redo the tabs based on our
`set tabstop=<your spaces count>` setting.

