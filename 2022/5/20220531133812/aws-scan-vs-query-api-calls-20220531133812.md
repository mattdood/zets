---
path: '/2022/5/aws-scan-vs-query-api-calls-20220531133812'
title: 'aws scan vs query api calls'
date: '20220531133812'
category: 'aws'
tags: ['developer associate', 'certification', 'dynamodb', 'api calls']
---

# aws scan vs query api calls
DynamoDB offers 2 ways to get data out of the database: scan and API calls.

## What is a query?
Queries find items in a table based on a **primary key** attribute and a distinct
**value** to search for.

Example:
Selecting an item where the user ID is equal to 212, you would select all the attributes
for that item and use the user ID as the key to search on.

#### Query results
* Sort key - results are always sorted by the sort key
* Numeric order - in ascending numeric order by default
* ASCII - ASCII character code values
* Reverse the order - You can reverse the order by setting the `ScanIndexForward`
parameter to false. **Note:** This is only for the query, not for scans.
* Eventually consistent - This is the default for querying.
* Strongly consistent - This parameter can be set to ensure results are strongly consistent.

### Refining the query
You can use an optional sort key name and value to further refine results.

This would be useful for things like timestamps, where you can only select items
that match a date range of a few timestamps.

### Returning specific attributes
By default a query returns all attributes for the items you search for. If you use
`ProjectionExpression` as a parameter you can choose to only return the specific attributes
that you want (i.e., only the email address rather than all attributes).

## What is a scan?
A scan operation examins every item in the table. By default it returns all the data
attributes.

Use the `ProjectionExpression` as a parameter if you want to only return specific attributes
that you want (same as with a query).

## Choosing between queries or scans
1. Querying is more efficient than a scan
    * The scan dumps the entire table and filters the values to provide a desired
    result, removing the unwanted data.
1. Extra steps with scans
    * Scans add an extra step of removing the data you don't want. As the table
    grows, the scan operation takes longer.
1. Provisioned throughput
    * A scan operation on a large table can use up the provisioned throughput for a large
    table in just a single operation.

## Improving query and scan performance
There are a few configurations that can be used to improve both query and scan performance.

### Improving query performance
* Set a smaller page size - this will return X number of items
* Running a larger number of **smaller operations** that will allow other requests to succeed
without throttling.
* In general, avoid using scan operations by using `Query`, `Get`, or `BatchGet` APIs

### Improving scan performance
* Sequential by default - a scan operation processes data sequentially by returning 1MB increments
before moving on to the next 1 MB of data. Scans one parititon at a time.
* Parallel scanning - You can configure DyanamoDB to use parallel scans instead by logically
dividing a table or index into segments and scanning each segment in parallel.
* Parallel scans should be avoided if we're incurring heavy read/write activity from
other applications. This can have impact on performance for downstream apps.
* Isolating scan operations to specific tables and segregating them from mission-critical
traffic is a best-case, even when writing to 2 tables and only scanning one of them.

## Exam tips
* A scan operation examines every item in the table and by default returns all the data
* Both queries and scans can have the # of attributes trimmed down with `ProjectionExpression`
* Queries find items in a table using the primary key and a distinct value to search for
* Queries can have default return value orders changed
* Queries are more efficient than scans, avoid scans by designing tables that don't need them

