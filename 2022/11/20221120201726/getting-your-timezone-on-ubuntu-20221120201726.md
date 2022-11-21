---
path: '/2022/11/getting-your-timezone-on-ubuntu-20221120201726'
title: 'getting your timezone on ubuntu'
date: '20221120201726'
category: 'linux'
tags: ['ubuntu', 'bash']
---

# getting your timezone on ubuntu
Just a factoid for myself to remember whenever I need a timezone for my systems.
This came into handy with docker compose files, I needed to set my environment
variable but didn't know what format it accepted.

```
cat /etc/timezone

>>> America/Los_Angeles
```

