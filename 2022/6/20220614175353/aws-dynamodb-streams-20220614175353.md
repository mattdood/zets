---
path: '/2022/6/aws-dynamodb-streams-20220614175353'
title: 'aws dynamodb streams'
date: '20220614175353'
category: 'aws'
tags: ['developer associate', 'certification', 'dynamodb', 'streams']
---

# aws dynamodb streams
A time ordered sequence of item level modifications (insert, update, delete).

## Features
* These are stored in an encrypted log for 24 hours. This is good for ordering,
archiving, and replaying events in a table.
* Typically the stream systems are used for event triggering (like a lambda function).
* The streams are accessed with their own dedicated endpoint separate from the table.
* By default the minimum amount of data that can be recorded is the primary key.
* Before and after images can also be captured, showing changes.

Events are logged in near real-time, which is great for serverless architectures.
The content of the stream (data) can be used for application development.

Example:
Lambda polls the DynamoDB stream for changes, then triggers different functions
based on the data.

## Use cases
* Audit or archive transactions
* Replicate data across multiple tables
* Trigger an event driven application

## Exam tips
1. Sequence of modifications - the steram is a time-ordered sequence of item level
modifications in your DynamoDB tables
1. Encrypted and stored - data is stored for 24 hours
1. Lambda event source - can be used as an event source for Lambda

