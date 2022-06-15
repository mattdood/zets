---
path: '/2022/6/aws-dynamodb-throughput-exceeded-20220614175918'
title: 'aws dynamodb throughput exceeded'
date: '20220614175918'
category: 'aws'
tags: ['developer associate', 'certification', 'dynamodb', 'metering']
---

# aws dynamodb throughput exceeded
The DynamoDB service will meter request throughput if the DynamoDB has a provisioned
throughput.

## Provisioned Throughput Exceeded
1. `ProvisionedThroughputExceededException` - Your request rate is too high for the
read/write capacity provisioned on your DynamoDB table
1. Using the AWS SDK? - The SDK will automatically retry requests until they are successful
1. Not using the AWS SDK? - Reduce the request frequency. Use an exponential backoff

## Exponential backoff
Overloaded components can generate errors based on having too many requests.
Typically you would implement retries by sending requests from the client side to
keep sending requests until it succeeds.

In addition to using simple retries, all AWS SDKs use exponential backoffs. This
means that it will wait an increasing amount of time between failed requests.

By increasing the duration of time that the requests wait to retry to help improve
the throughput.

**Note:** If after 1 minute this doesn't wor, your request sie may be exceeding the throughput
for your read/write capacity.
    * If this is for read requests then the accelerator (DAX) may be a good fit
    * If this is for writes then the provisioned throughput for the writes should be adjusted

