---
path: '/2022/6/aws-sqs-queue-types-20220615095939'
title: 'aws sqs queue types'
date: '20220615095939'
category: 'aws'
tags: ['developer associate', 'certification', 'sqs', 'queues']
---

# aws sqs queue types
The primary difference between queue types is how they handle the ordering of
messages.

## Two types of queue
1. Standard queues are the default - which provide "best-effort" ordering
1. FIFO (first-in-first-out) - ordering of messages is strictly preserved

## Standard queues
* Nearly unlimited number of transactions per second
* Guarantees that a message is delivered at least once
* Best-effort ordering - provides a "generally delivered" in the same order as they're sent
    * Due to the highly distributed system, some may be delivered multiple times or
    in the wrong order

## FIFO queues
* First-in-first-out delivery - order messages are received is strictly preserved
* Exactly-once processing - a message is delivered once and remains available
until a consumer processes and deletes it. Duplicates are not introduced.
* 300 transactions per second limit
    * FIFO queues are limited to 300 TPS, but have all the capabilities of a standard queue

## Exam tips
* Standard queue:
    * Best-effort ordering
    * Message delivered at least once
    * Occasional duplicates
    * Default queue type
* FIFO queue:
    * First-in-first-out message order is strictly preserved
    * Messages are delivered once
    * No duplicates

