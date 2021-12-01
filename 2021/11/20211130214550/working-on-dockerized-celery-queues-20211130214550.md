---
path: '/2021/11/working-on-dockerized-celery-queues-20211130214550'
title: 'working on dockerized celery queues'
date: '20211130214550'
category: 'celery'
tags: ['celery', 'redis', 'docker']
---

# working on dockerized celery queues
We had an interesting production issue that we had crop up where our celery
containers were dumping tasks repetitively on each shutdown, then re-queueing them.

The strange thing is that they weren't blocking the other tasks and we were getting
some insane duplicates, to the tune of 1,000's of emails coming through the
pipeline.

There was some deep diving into the Redis queues that we had to check up on,
though this was in production so it was an interesting exploration.

Some useful commands I learned are below.

Execute this from inside your celery worker:
```
celery purge # does what it says
```

Checking on the # of tasks in the queue with Redis:
```
docker exec -it <redis container name> bash

# list keys to the queues
redis-cli -h 127.0.0.1 -p 6379 -n 1 keys \*

# gets length of queue as integer
redis-cli -h 127.0.0.1 -p 6379 -n 1 llen <number from first command>
```

**Note:** I filled in the default host and port numbers, along with a default
database number. These are likely different in your environment.

