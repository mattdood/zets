---
path: '/2022/5/aws-dynamodb-indexes-20220531133127'
title: 'aws dynamodb indexes'
date: '20220531133127'
category: 'aws'
tags: ['developer associate', 'certification', 'dynamodb', 'indexing']
---

# aws dynamodb indexes
DynamoDB indexes exist to allow querying on non-primary key attributes stored within
the table.

## Flexible querying
Query based on an attribute that is not the primary key. This uses **global secondary
indexes** and **local secondary indexes** to accomplish query execution.

* Secondary index - allows you to perform fast queries on specific columns in a table.
    * You select the columns that you want included in said index, then run the searches
    on the index itself rather than the whole dataset. These run on a subset of the data.

## Local secondary index
* Primary key - These have the same partition key as the original table, but a different sort key.
This changes the organization of the data, but still uses the original table partition.
* Different view - gives a different view of the data due to the alternate sort key
* Faster queries - Any queries fbased on this sort key are much faster using the index
rather than the maint able.
    * Example: Partition key of user ID, sort key of account creation date
* Added at creation time - The local secondary index can only be added when you are
creating your table. These cannot be added, removed, or modified later.

## Global secondary index
* A completely different primary key - different partition and sort keys
* View data differently - also gives a different view of the data (similar to local secondary index)
* Speeds up queries - the speed is related to the alternative partition and sort key
    * Example: Parititon key of email address, sort key of last login date
* Flexible - You can create these when you create or table, or add them in later.

## Exam tips
* Enable fast queries on specific data columns
* Give a different view of the data based on an alternative parition/sort key combination
* Each index type offers different benefits, these should be considered on table creation

