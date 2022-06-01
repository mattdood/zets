---
path: '/2022/5/aws-lambda-concurrent-executions-limitations-20220524105657'
title: 'aws lambda concurrent executions limitations'
date: '20220524105657'
category: 'aws'
tags: ['lambda', 'developer associate', 'certification']
---

# aws lambda concurrent executions limitations
The AWS Lambda service has concurrency limitations to limit the number of functions
that can be run simultaneously within a given region, per account.

## Concurrent executions
* Default is 1,000 per region
* Error message is `TooManyRequestsException`
* HTTP status code: 429
* Request throughput limit to be increased
    * This can be requested through the AWS Support Center
* **Reserved concurrency** guarantees that a set number of executions which will always
be available for your critical function, however this also acts as a limit

