---
path: '/2022/6/ubuntu-sda-contains-a-file-system-with-errors-check-forced-20220614102823'
title: 'ubuntu sda contains a file system with errors check forced'
date: '20220614102823'
category: 'linux'
tags: ['ubuntu', 'disk errors']
---

# ubuntu sda contains a file system with errors check forced
During a normal start up on my Ubuntu virtual machine I ran into an error (below)
that indicated I had some disk issues. This was odd because I'd been using this
without issue for a few weeks and always properly shut it down when not working.

The issue indicated that I should run a disk diagnostic and allow it to remedy
the file system issues.

This problem seems to be possible on a normal Ubuntu installation outside of a VM
as well.

**Note:** The disk name in this error may be different depending on the machine.

## Error
```
/dev/sda1 contains a file system with errors, check forced.
Inodes that were part of a corrupted orphan linked list found.

/dev/sda1: UNEXPECTED INCONSISTENCY: RUN fsck MANUALLY.
         (i.e., without -a or -p options)
fsck exited with status code 4
The root filesystem on /dev/sda1 requires a manual fsck

BusyBox v1.22.1 (Ubuntu 1:1.22.0-19ubuntuu2) built-in shell (ash)
Enter 'help' for a list of built-in commands.

(initramfs)_
```

## Solution
Running the following in the `initramfs` prompt solved the inconsistencies on the
disk. Afterwards I was able to safely restart and the VM worked.

`fsck -f /dev/sda1`

