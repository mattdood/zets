---
path: '/2022/6/aws-dynamodb-time-to-live-ttl-20220614133041'
title: 'aws dynamodb time to live TTL'
date: '20220614133041'
category: 'aws'
tags: ['developer associate', 'certification', 'dynamodb', 'time to live']
---

# aws dynamodb time to live TTL
DynamoDB TTL (time-to-live) is a set expiry time for your data. Expired items are
marked for deletion (deleted within the next 48 hours).

Great for removing irrelevant or old data (session data, event logs, temporary data).

Reduces the cost of your table by automatically removing data that is no longer
relevant.

**Note:** TTL is stored in **epoch** time. This is known as unix time or posix time.
A numerical value (in seconds) that has elapsed since 12:00am on 1/1/1970.

The creation time is compared to the expiration time, which sets the TTL as the
delta of the two.

## Exam tips
* Time to live (TTL) - defines expiry time for your data
* Use cases - great for removing irrelevant or old data (session data, event logs, temp data)
* Helps save money - reduces the cost of the table by removing data that is no longer
relevant

