---
path: '/2022/7/linux-net-tools-for-diagnosing-errors-in-port-bindings-20220722140300'
title: 'linux net tools for diagnosing errors in port bindings'
date: '20220722140300'
category: 'linux'
tags: ['networks', 'localhost', 'ports']
---

# linux net tools for diagnosing errors in port bindings
When checking for the currently used ports to check for any blockers we can use a
tool called `net-tools`.

The tool returns a list of currently used port mappings to help diagnose the port that
is currently being consumed.

I encountered the need for this when working with a Docker application that required
a common port, I was able to find an Apache2 server running on that port mapping
that I terminated.

[StackOverflow reference](https://stackoverflow.com/questions/37971961/docker-error-bind-address-already-in-use)

## Example usage and installation
```
sudo apt install net-tools

# returns non-privileged user processes
sudo netstat -pna | grep <your port number>

# returns all processes
sudo netstat -pna | grep <your port number>
```

