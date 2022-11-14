---
path: '/2022/11/truenas-doesnt-allow-existing-raid-arrays-to-be-overwritten-20221113183035'
title: 'truenas doesnt allow existing raid arrays to be overwritten'
date: '20221113183035'
category: 'homelab'
tags: ['homelab', 'truenas']
---

# truenas doesnt allow existing raid arrays to be overwritten
Just a note for anyone that stumbles onto this post - if you're creating storage
pools in TrueNAS the drives cannot be in a pre-existing RAID array due to the
safety protocols that are built into their software.

You will have to **remove** this RAID configuration before you're able to
move forward with creating storage pools.

