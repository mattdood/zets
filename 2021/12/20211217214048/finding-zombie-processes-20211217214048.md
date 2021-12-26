---
path: '/2021/12/finding-zombie-processes-20211217214048'
title: 'finding zombie processes'
date: '20211217214048'
category: 'linux'
tags: ['bash', 'ubuntu']
---

# finding zombie processes
Sometimes when Docker containers are stopped and started in quick succession for
testing I've noticed that my Docker daemon isn't giving a proper call back to
systemctl to release the process.

Zombie processes can be difficult to get rid of, and sometimes the symptoms don't
necessarily look like they are "zombies".

## Example
In one particular instance I had a zombie Docker container process that wasn't
releasing an active port.

On startup, this container was throwing a `cannot bind to port 9000:9000, it is in use`.

## Diagnosing zombie processes
When working on this problem, I did the standard `docker ps` and equivalent checks
in [Portainer](https://www.portainer.io/). This returned odd results, as I noticed
that the port itself wasn't in use.

I found that zombie processes are a potential issue when shutting down a program,
and [used this comment from Stackoverflow](https://askubuntu.com/a/290012).

```bash
ps aux | grep 'Z'
```

This returned a process that had not successfully closed, and I then inspected
the parent of this process so I could remove the failed process.

```bash
pstree -p -s <pid of parent>
```

After this it was as simple as issueing a `kill <parent pid>`.

