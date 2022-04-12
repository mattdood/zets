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
This is cost optimized for data archival.
* Storage is very, very inexpensive
* Optimized for data that is very infrequently accessed
* Users pay for each time you access data
* 99.9% availability
* 11 9's of durability

### Glacier
* Retrieval time ranges from 1 minute to 12 hours
* 90 day minimum storage commitment

### Glacier Deep Archive
* Archives rarely accessed data with a default retrieval time of 12 hours
* Good for things that are very, very rarely accessed (or not, ex: Auditable records)
* Retrieval time starts at minimum of 12 hours
* 180 day minimum storage commitment

## S3 intelligent tiering
2 tiers exist for object access:
* frequent and infrequent access
* Automatically moves your data to the most cost-effective tier based on how frequently
objects are being accessed
* Adds a monthly fee of $0.0025 per 1,000 objects
* 99.9% availability
* 11 9's of durability

## S3 exam tips

* s3 standard:
    * 99.99% avail, 11 9's durability
    * >=3 AZs
    * Suitable for most workloads
* s3 standard infrequent access:
    * 99.9% avail, 11 9's durability
    * >=3 AZs
    * Long term infrequently accessed critical data
    * Minimum storage duration 30 days
* s3 one zone infrequent access:
    * 99.5% avail, 11 9's durability
    * 1 AZ
    * Long term infrequently accessed non-critical data
    * Minimum storage duration 30 days
* s3 glacier:
    * 99.99% avail, 11 9's durability
    * >=3 AZs
    * Long term data archival with occasional access (within hours or minutes)
    * Minimum storage duration 90 days
* s3 glacier deep archive:
    * 99.99% avail, 11 9's durability
    * >=3 AZs
    * Rarely accessed data archival with occasional access, 12 hours retrieval
    * Minimum storage duration 180 days
* s3 intelligent tiering:
    * 99.9% avail, 11 9's durability
    * >=3 AZs
    * Unknown or unpredictable access pattern
    * Minimum storage duration 90 days

