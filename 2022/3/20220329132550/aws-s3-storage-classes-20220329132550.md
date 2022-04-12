---
path: '/2022/3/aws-s3-storage-classes-20220329132550'
title: 'aws s3 storage classes'
date: '20220329132550'
category: 'aws'
tags: ['developer associate', 'certification', 's3', 'storage']
---

# aws s3 storage classes
AWS S3 offers a number of different storage classes for various use cases. These have
different associated costs and trade offs between them.

## S3 standard
This is designe dfor high avialability and durability.
* Storage across >= 3 availability zones
    * 99.99% availability
    * 11 9's of durability
* Designed for frequent access
* Suitable for most workloads (default storage class)
    * Usage includes websites, content distribution, gaming apps, etc.

## S3 standard infrequent access (S3-IA)
Designed specifically for infrequently accessed data.
* Provides rapid access - used for data that is accessed less frequently, but
does need rapid access when called upon
* Pay to access data - there is a low per-GB storage price and per-GB retrieval fee
* Use cases are cenered around long-term storage, backups, and disaster recovery files
* 99.99% availability
* 11 9's of durability
* **Note:** Minimum storage duration is 30 days

## S3 one zone infrequent access
This is similar to S3-IA but it is stored redunantly within a single AZ.
* Costs 20% less than the regular S3-IA
* Good for long-lived, infrequently accessed, non-critical data
* 99.5% availability
* 11 9's of durability
* Minimum storage duration is 30 days

## S3 glacier

