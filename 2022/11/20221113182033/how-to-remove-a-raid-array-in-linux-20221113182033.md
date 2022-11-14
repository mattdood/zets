---
path: '/2022/11/how-to-remove-a-raid-array-in-linux-20221113182033'
title: 'how to remove a raid array in linux'
date: '20221113182033'
category: 'linux'
tags: ['storage', 'raid', 'nas', 'homelab', 'truenas']
---

# how to remove a raid array in linux
While working on my homelab today I ran into an issue when swapping to a new
operating system (NAS provider) wherein my drives couldn't be overwritten
by TrueNAS due to them existing in a RAID array already.

To remedy the issue I removed the RAID array manually using the console, which
allowed me to provision my drives into a "storage pool" inside TrueNAS.

## Steps
1. Checking the raid configuration
    1. `cat /proc/mdstat` - Shows the active RAID arrays
1. Checking the details of which drives are included
    1. `mdadm --detail /dev/<your raid array name>`
1. Removing the RAID itself first requires the drives to not be mounted (if they are)
    1. `umount /<your raid array disk>`
    1. `sed -i '/<your raid array>/d' /etc/fstab`
1. Now we can stop the RAID array. For the TrueNAS distribution the RAID array
is already deleted which saves some effort for us
    1. `mdadm --stop /dev/<your raid array here>`
    1. `mdadm --remove /dev/<your raid array here>`

