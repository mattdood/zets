---
path: '/2021/12/mounting-nfs-shares-in-ubuntu-server-20211208175826'
title: 'mounting nfs shares in ubuntu server'
date: '20211208175826'
category: 'linux'
tags: ['ubuntu server', 'nfs', 'homelab', 'nas']
---

# mounting nfs shares in ubuntu server
During setup of our home NAS my household (mostly me) decided to separate our media
services and our media files into two separate servers. This would help to keep
our file storage server's resources separate from our application server's resources.

I'd never mounted a network file share before, so I thought I'd document the procedure.

[Reading about a Network File System](https://www.datto.com/blog/what-is-nfs-file-share)
[File permissions number calculator](https://chmod-calculator.com/)

## Steps + commands
1. ssh to your server, mine was internal.

```
ssh you@192.168.1.123
```

1. Determine your mount point from the NAS, I did this by running the following on the NAS server.
    * Note: We use an OpenMediaVault server, so our NFS mounts are under `/export/`

```
ls -l /export/

# output sample
root@your-nas:~# ls -l /export/
total 4
drwxrws--- 2 root users 4096 Dec  8 17:25 MediaShare
```

1. Create your mount point

```
mkdir -p /mnt/your-mount-here
```

1. Use the above information to mount to your destination server.

```
sudo mount -t nfs4 192.168.1.234:/export/MediaShare /mnt/your-mount-here
```

1. Set the permissions that you need, I did a `chown` for my user and set the files to `755`

```
sudo chown -R ${USER:GROUP} /mnt/your-mount-here/

sudo chmod -R 755 /mnt/your-mount-here/
```

1. Test and check the permissions to ensure you don't have errors

    1. I first ran a `stat` to check permissions
    ```
    stat /mnt/your-mount-here/

    you@your-server:/$ stat /mnt/your-mount-here/
      File: /mnt/your-mount-here/
      Size: 4096            Blocks: 8          IO Block: 4096   directory
    Device: fd00h/64768d    Inode: 3145730     Links: 2
    Access: (0755/drwxr-xr-x)  Uid: ( 1000/ you)   Gid: (    0/    root)
    Access: 2021-12-09 01:51:14.485360884 +0000
    Modify: 2021-12-09 01:43:15.653176950 +0000
    Change: 2021-12-09 01:51:14.485360884 +0000
     Birth: -
    ```

    1. I also created a test file to check for errors

    ```
    touch /mnt/your-mount-here/test.py
    ```
