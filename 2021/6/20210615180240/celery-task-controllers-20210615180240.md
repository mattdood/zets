---
path: '/2021/06/celery-task-controllers-20210615180240'
title: 'Celery Task Controllers'
date: '20210615180240'
category: 'celery'
tags: ['celery', 'django', 'scraping']
---

# celery task controllers
During a revamp of a previous project I found myself needing to chain together
several Celery tasks into one place.

I used `chain()` rather than trying to pass results back and forth between
tasks. A sample implementation is below.

[Documentation on `chain()`](https://docs.celeryproject.org/en/stable/userguide/canvas.html#chains)

## Idea
I needed a single task to execute a simple workflow once per minute:
* Scrape data from a feed
* Optionally pass that data to be screened
* Save the data

## Issues
These issues are broken into sub-categories.

### `.delay()` -> `.get()`
I found several issues when working through how to handle the returns of the
tasks in a reasonable fashion.

```python
results = task_name.delay()

# Returns an error
other_task = other_task.delay(results.get())
```

### Tasks need serialized data
* Data must be serialized and cannot easily be Python objects
    * For Django I used `serialize('json', [obj, obj, ...])` with `deserialize('json', [obj, obj, ...])`

While it is not ideal to serialize and deserialize between each task, it
did allow access to the object's class which I found more valuable than
using solely JSON.

```python

serialize('json', some_list)

deserialize('json', some_serialized_list)

```

## Solution: `chain()`
I found the `chain()` to be the best method to pass data back and forth.
This has a few constraints regarding how data is passed between tasks; however,
it does pass the return value of functions down the chain sequentially.

### Constraints

### Sample implementation
This sample uses [Django's serialization tools](https://docs.djangoproject.com/en/3.2/topics/serialization/)
to pass JSON objects that can then be converted to Django objects.

```python
from django.core.serializers import deserialize, serialize

@shared_task
def task_one():
    # implementation
    serialized_data = serialize('json', some_list)
    return serialized_data

@shared_task
def task_two(some_data):
    deserialized_data = deserialize('json', some_data)

    for data.object in deserialized_data:
        # implementation

    serialized_data = serialize('json', some_list)
    return serialized_data

... etc.

@shared_task
def task_controller():
    # implementation
    chain(task_one.s(), task_two.s())
```

