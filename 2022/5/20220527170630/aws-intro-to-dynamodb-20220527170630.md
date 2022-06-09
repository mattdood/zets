---
path: '/2022/5/aws-intro-to-dynamodb-20220527170630'
title: 'aws intro to dynamodb'
date: '20220527170630'
category: 'aws'
tags: ['developer associate', 'certification', 'dynamodb']
---

# aws intro to dynamodb
DynamoDB is a NoSQL database that stores and retrieves data without having to
define its structure/schema upfront. This is an alternative to relational databases
that are rigid in structure.

## General information
* Fast and flexible
    * Great for applications that need consistent, single-digit millisecond
    latency at any scale
* Fully managed
    * Supports key-value data models.
    * Supported document formats are JSON, HTML, XML
* Use cases
    * Great fit for mobile, web, gaming, IOT, and ad-tech.

## Serverless
DynamoDB is a serverless database that can be configured to automatically scale.
This is a popular choice for developers and architects that are already designing
serverless applications.

Out of the box the DynamoDB offering integrates well with Lambda functions.

## DynamoDB Features
* Performance - SSD storage
* Resilience - Data is spread across 3 geographically distinct data centers
* Consistency - Eventually consistent reads (default), strongly consistent reads, and ACID transactions

## Consistency models
DynamoDB offers different data consistency models for different use cases.

### Eventually consistent reads
Consistency across all copies of data is usually reached within a second.

If you read data that you changed 1 second ago, then the DB should return your
recently changed data. This is **best for read performance**.

### Strongly consistent reads
A strongly consistent read always reflects all successful writes. Writes are
reflected across all 3 locations at once. This is **best for read consistency**.

### ACID transactions
These are called `DynamoDB Transactions` and provide the ability to perform
ACID transactions (Atomic, Consistent, Isolated, Durable). This enables the ability
to read or write across multiple tables, in multiple transactions, in an all-or-nothing
fashion.

Essentially meaning that you can perform the transaction and if it fails then the outcome
will not occur.

## Primary keys
* Primary keys are used to store and retrieve data
* Two types of keys:
    * Partition key
        * A unique attribute to the table (customer ID)
        * Partition keys input to an internal hash function that determines the partition
        (or physical location) of the data on the disk
        * This is why no 2 items have the same partition key, they can't have the same
        location in physical space on the disk
    * Composite key (partition key + sort key)
        * Combination of a partition key and a sort key
        * The unique combination required for a primary key means that we could
        have the same partition key used but by having different sort keys we have uniqueness

## Restricting user access with IAM
User access can be restricted with a condition to an IAM policy to allow access
to items only if the partition key value matches some unique ID.

Example configuration for user access control:
```JSON
"Condition": {
    "ForAllValues:StringEquals": {
        "dynamodb:LeadingKeys": [
            "${www.mygame.com:user_id}" -> parition key must match user_id to restrict access
        ]
    }
}
```

## Exam tips
* DynamoDB is a low latency NoSQL database
* Data models are either key-value or document formats (JSON, HTML, XML)
* Consistency models are eventually, strongly, or DynamoDB (ACID) transactions
* Features - consists of tables, items, and attributes
* 2 types of primary key - partition key, composite key (partition key + sort key)
    * Partition keys should be unique identifiers
    * Sort keys would be things like time stamps or dates to have a uniquely identifying
    primary key

