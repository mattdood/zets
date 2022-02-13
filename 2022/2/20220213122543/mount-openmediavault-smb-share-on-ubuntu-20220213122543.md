---
path: '/2022/2/mount-openmediavault-smb-share-on-ubuntu-20220213122543'
title: 'mount openmediavault smb share on ubuntu'
date: '20220213122543'
category: 'homelab'
tags: ['ubuntu', 'smb share', 'openmediavault']
---

# mount openmediavault smb share on ubuntu
Mounting NFS shares is quite different from the Windows friendly SMB share variant.

I found it quite difficult to mount this on my Ubuntu laptop, as it was having
difficulties validating my credentials even though it was set to "guest". While
there were a few StackOverflow and Reddit posts regarding the issue, I didn't have
anything that was usable for guests.

[This StackOverflow post was super helpful](https://askubuntu.com/questions/1092278/mount-windows-share-as-guest-from-command-line)

## Mounting a guest SMB share
Guest mounting is much easier, here's a command to run. Additionally, we can
put this in our `/etc/fstab` too.

```
sudo mount -t cifs -o rw,guest,vers=1.0 //my.ip.address.here/<fileshare-path> /my/local/path
```

Edit our `etc/fstab`:
```
# your other fstab stuff up here
//my.ip.address.here/<fileshare-path> /my/local/path cifs vers1.0 rw guest
```

## Mounting an SMB share with credentials
To mount with credentials we should use a file that will log us in every time we
hit the mount:

Create a `.credentials` file:
```
sudo vim /etc/.credentials
```

Fill it with our information:
```
# credentials file
username=<my username>
password=<my password>
```

Mount the share:
```
sudo mount -t cifs -o credentials=/etc/.credentials,rw,vers=1.0 //my.ip.address.here/<fileshare-path> /my/local/path
```

Add it to the `etc/fstab`:
```
# your other fstab stuff up here
//my.ip.address.here/<fileshare-path> /my/local/path cifs vers1.0 rw guest /etc/.credentials
```

