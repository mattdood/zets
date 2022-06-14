---
path: '/2022/6/aws-dynamodb-provisioned-throughput-20220614130500'
title: 'aws dynamodb provisioned throughput'
date: '20220614130500'
category: 'aws'
tags: ['developer associate', 'certification', 'dynamodb', 'metering']
---

# aws dynamodb provisioned throughput
DynamoDB provisioned throughput is measured in "capacity units".

During table creation you can specify requirements in terms of "read" and "write"
capacity units.

## Write capacity units
1x write capacity unit = 1x 1KB write per second

## Read capacity units
1x read capacity unit = 1x strongly consistent read of 4KB per second
    OR 2x eventually consistent reads of 4KB per second (default)

Example:
Your app needs strongly consistent reads at a rate of 80 reads/s and it has a
payload of 3KB per read.

You'll provision:
* size of each payload / 4KB
    * 3KB/4KB = 0.75
* Rounded-up to the nearest whole number, each read operation needs 1x read capacity unit
* Multiply the number of reads per second = 80 read capacity units required
for strongly consistent reads

## Exam tips
* Write capacity units - 1x 1KB write per second
* Read capacity units (strongly consistent) - 1x 4KB write per second
* Read capacity units (eventually consistent) - 2x 4KB write per second

