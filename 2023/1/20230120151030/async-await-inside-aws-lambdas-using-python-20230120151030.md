---
path: '/2023/1/async-await-inside-aws-lambdas-using-python-20230120151030'
title: 'async await inside aws lambdas using python'
date: '20230120151030'
category: 'aws'
tags: ['python', 'lambda', 'asyncio', 'asynchronous programming', 'async await']
---

# async await inside aws lambdas using python
When working with AWS Lambda and `asyncio` in a Python environment we can sometimes
get some odd behavior with the lambda itself running the asynchronous code but not
returning the results.

This is expected because we're not necessarily telling the Lambda to `await` the
asynchronous invocation's results.

## Pitfalls with asyncio in AWS Lambdas
A few gotcha's exist when working with `asyncio`, below are the pitfalls:
1. ***Do not*** install `asyncio` using `pip` - The `asyncio` library is included inside
the Python standard library, `pip install`-ing it will cause errors
1. Ensure that the runtime for Python in the lambda is `>= 3.7`
1. Use an `asyncio` handler that will force the functionality to return results in a
*synchronous* manner

## Forcing synchronous behavior
An example of the implementation below utilizes a run loop that `asyncio` provides
to ensure we're gathering synchronous results.

```python
import asyncio

loop = asyncio.get_event_loop()


# Some sample async function
async def my_async_func(event):
    await print(f"{event}")
    return 0


# Entrypoint for our lambda
def lambda_handler(event, context):

    # Call our async function
    coroutine = my_async_func(event)

    # Tell asyncio to run the function and gather the
    # results synchronously
    results = loop.run_until_complete(*[coroutine])

    return results
```

Another example that I haven't personally tested, but have seen in StackOverflow
posts and whatnot:

```python
import asyncio


# Some sample async function
async def my_async_func(event):
    await print(f"{event}")
    return 0


# Entrypoint for our lambda
def lambda_handler(event, context):

    # Call our async function
    results = asyncio.run(my_async_func(event))

    return results
```

