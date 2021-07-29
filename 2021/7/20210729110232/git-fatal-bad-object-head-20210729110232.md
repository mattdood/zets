---
path: '/2021/7/git-fatal-bad-object-head-20210729110232'
title: 'git fatal bad object HEAD'
date: '20210729110232'
category: 'git'
tags: ['corrupt repo', 'repo']
---

# git fatal bad object HEAD
Sometimes when doing a `git status` I'll run into some fatal object errors and
have to run a few troubleshooting techniques.

## Typical error
This will show some object issues and keep you from seeing your status and files.

```
error: object file .git/objects/31/65329bb680e30595f242b7c4d8406ca63eeab0 is empty
fatal: loose object 3165329bb680e30595f242b7c4d8406ca63eeab0 (stored in .git/objects/31/65329bb680e30595f242b7c4d8406ca63eeab0) is corrupt
```

### The alias I use to resolve this
When troubleshooting this I found some more manual ways to do this in the link below.
I use this alias because it solves things 99% of the time.

[Source for this](https://stackoverflow.com/a/31110176/12387496)

```bash
alias git-corrupt='find .git/objects/ -type f -empty | xargs rm && \
    git fetch -p && \
    git fsck --full'
```

## Today I ran into this error
I should've read closer; however, I "autopiloted" my way to running this - not recommended.
When using my alias on the incorrect error I created a separate issue.

```
fatal: loose object 7b36029a951eacd979d24e993e020c4d018ca265 (stored in .git/objects/7b/36029a951eacd979d24e993e020c4d018ca265) is corrupt
fatal: unpack-objects failed
```

### After running my alias
I then received a new fatal issue with the `HEAD` of my branch.

```
fatal: bad object HEAD
```

### Resolution
The resolution that I discovered (after some Googling) is below.
Fortunately I didn't have to troubleshoot for long and this resolution worked first
try.

* Note: There is further effort after the initial `git reset` that I haven't done.

[Source for the resolution is after "git status"](https://stackoverflow.com/a/30871926/12387496)

```bash
git reset master
git status

# showed all good
```


