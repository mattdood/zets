---
path: '/2022/6/aws-dynamodb-on-demand-capacity-20220614131248'
title: 'aws dynamodb on-demand capacity'
date: '20220614131248'
category: 'aws'
tags: ['developer associate', 'certification', 'dynamodb', 'on-demand']
---

# aws dynamodb on-demand capacity
Charges apply for reading, writing, and storing data in DynamoDB with instant
scaling based on the activity (both up/down).

This is based on the reads/writes on the table, rather than specifying the read/write
units during table creation.

**Great for:**
* Unpredictable workloads
* New applications you don't have workload plans for
* When you want to "pay for what you use"

## On-demand capacity
* Unknown workloads
* Unpredictable application traffic
* Spiky, short-lived peaks
* Pay-per-use model is desired
* It may be more difficult to predict the cost

## Provisioned capacity
* Read/write capacity can be easily forecasted
* Predictable application traffic
* Application traffic is consistent or increases gradually
* Gives much clearer ideas of cost

