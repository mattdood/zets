---
path: '/2023/1/finding-an-object-in-s3-using-boto3-without-using-a-list-objects-method-20230124101436'
title: 'finding an object in s3 using boto3 without using a list objects method'
date: '20230124101436'
category: 'aws'
tags: ['python', 'boto', 's3']
---

# finding an object in s3 using boto3 without using a list objects method
I've seen quite a few implementations of a "does this object exist?" method
that use Boto3 as a pagination tool to sift through a list of objects in a bucket.

This is objectively (hehe) fine; however it should only be implemented for a list
of validations rather than a single item.

The issue with this approach is in a few places:
* `O(n)` time to resolve the match via pagination, given `n` is the # of objects in the bucket
* Repetitive calls to S3 that incur charges
* Slower roundabout returns due to repetitive API calls, they even have potential for throttling

A great solution to this is to use the `head_object()` method of the Boto3 library.
This returns the metadata for a given object if it exists, a `botocore.errorfactory.ClientError` if it does not.

**Reference:**
* [StackOverflow post discussing a few different S3 obj. checking methods](https://stackoverflow.com/questions/33842944/check-if-a-key-exists-in-a-bucket-in-s3-using-boto3)

## Example implementation

```python
import boto3
from botocore.client import BaseClient
from botocore.errorfactory import ClientError

s3_client = boto3.client('s3')


def s3_obj_exists(s3_client: BaseClient, s3_key: str) -> bool:
    try:
        s3_client.head_object(
            Bucket='my-s3-bucket',
            Key=s3_key,
        )
        return True

    except ClientError:
        # obj not found
        pass

    return False
```

