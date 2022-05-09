---
path: '/2022/5/aws-lambda-versions-20220509153618'
title: 'aws lambda versions'
date: '20220509153618'
category: 'aws'
tags: ['developer associate', 'certification', 'lambda']
---

# aws lambda versions
Lambda versioning allows us to control what lambdas are run, to allow backward
compatibility, testing, staging, etc.

## Versioning
* When you create a lambda function, there is only 1 version: $LATEST
* When you upload a new version of the code to Lambda, the new version becomes $LATEST
* You can create multiple versions of your function and use aliases to reference them
as part of the ARN of the function
    * Example: Development environment may maintain multiple versions of the same function
    to develop and test code
* An alias is like a pointer to a specific version of the function

Example Lambda versioning:
![2 lambda versions with their ARNs](./20220509153926-img-1.png)

* Versions of the lambda can be sent between different versions of functions based
on weighted percentages (%)

