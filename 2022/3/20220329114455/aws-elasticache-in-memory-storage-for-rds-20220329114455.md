---
path: '/2022/3/aws-elasticache-in-memory-storage-for-rds-20220329114455'
title: 'aws elasticache in memory storage for rds'
date: '20220329114455'
category: 'aws'
tags: ['developer associate', 'certification', 'databases', 'elasticache', 'caching']
---

# aws elasticache in memory storage for rds
Memory is faster than disk. Elasticache is a way to speed database queries by
storing frequently accessed data in an in-memory cache.

* In-memory cache (key value) - easy to deploy, operate, and scale in-memory cache in the cloud
* Improves DB performance - retrieving information in faster caches than disk-based storage
* Good for read-heavy DB workloads (caching results of I/O intensive queries)
* Useful for session data on distributed applications

An Elasticache cluster can store the frequently accessed data, then the application
would query the cache instead of the database.

## Memcached
Great for basic object caching, scaling horizontally, with no persistence.

This has no multi AZ or failover options. However, it is a good choice if you want
basic caching and it to be as simple as possible.

## Redis
A more sophisticated solution with enterprise features like persistence, replication,
multi AZ, failover.

This also supports sorting and ranking data (like gaming leaderboards), lists, and
other complex data types.

## Typical exam scenario
1. Database under stress
1. Find a solution
    * What service would alleviate this
1. Know when to use Elasticache
    * This is a good if your database is read-heavy and not prone to frequent changes

## When not to use elasticache
* Heavy write loads
    * Caching doesn't alleviate heavy writes, you'd need to scale up the DB instead
* OLAP queries with analytical loads
    * This is basically any complex, long running query. Use RedShift instead.

