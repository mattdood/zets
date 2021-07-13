---
path: '/2021/7/asyncresult-returns-from-celery-tasks-20210712193345'
title: 'AsyncResult returns from celery tasks'
date: '20210712193345'
category: 'python'
tags: ['celery', 'django']
---

# AsyncResult returns from celery tasks
When working through a set of asynchronous tasks I have been finding it useful
to have a controller -> sub-task structure.

This leverages the ability for Celery to resolve task outcomes and pass results
using `chain()`.

Today I was reminded (hence the note) that results from `.delay()` calls are
not going to be resolved to the return of the function you are running. These
instead resolve to a `celery.result.AsyncResult` class that states some additional
information about the execution.

We should instead use the `.get()` after the task which would return the result.
The documentation states that we should avoid the use of `.get()` too much for
interlocked tasks, as this is inefficient and should instead rely on `chain()`.

[Documentation on the `AsyncResult`](https://docs.celeryproject.org/en/stable/reference/celery.result.html#celery-result)

Example:
```python

@shared_task
def some_task()
    return True

result = some_task.delay.get()

if result:
    # do something
else:
    # do something else
```



