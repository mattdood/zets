---
path: '/2022/6/aws-kinesis-consumers-20220621114205'
title: 'aws kinesis consumers'
date: '20220621114205'
category: 'aws'
tags: ['developer associate', 'certification', 'kinesis', 'streams']
---

# aws kinesis consumers
Scaling Kinesis streams requires increasing the number of shards utilized in processing/sending
data to consumers.

Kinesis has client libraries used in record processors. A consumer instance can process
multiple shards, or we can split them (for failover or reducing load).

The Kinesis client library will handle the load balancing between consumers.

## Kinesis client libraries
* For scaling out consumers we want to ensure the number of consumer instances
does not exceed the number of shards (except for failure/standby purposes)
* Never need to have multiple instances to handle the processing load of 1 shard
    * A shard has the following throughput
        * 2 MB of read/s
        * 1 MB of write/s
* One worker can process multiple shards
* CPU utilization should be the driving force of consumer instance quantity, not
the number of shards in your stream

**Note:** It's best to use an autoscaling group to handle consumer scaling.

## Exam tips
* Kinesis shards:
    * Kinesis Client Library is running on consumers to create a record processor
    for each shard being consumed by the instance
    * Re-sharding (increasing # of shards), creates additional record processors
    on your consumers
    * Autoscaling groups are best for scaling decisions on CPU load on your consumers
    * CPU utilization is the driving force on the quantity of consumers instances
    that you have, NOT the number of shards

