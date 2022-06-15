---
path: '/2022/6/aws-sqs-parameters-20220615101508'
title: 'aws sqs parameters'
date: '20220615101508'
category: 'aws'
tags: ['developer associate', 'certification', 'sqs', 'queues']
---

# aws sqs parameters
There are a few settings with the SQS system that allow additional configuration
of the queues.

## Visibility timeout
Visibility timeout is the amount of time that the message is invisible in the SQS
queue after a reader picks up that message.
    * By default the timeout is 30 seconds
    * Max timeout is 12 hours

If the job is not processed in the timeframe it was made invisible, then it will
be visible again and will be available for pickup by another consumer.

## Short polling vs. long polling
* Short polling:
    * Returns a response immediately even if the message queue being polled is
    empty
    * This can result in a lot of empty responses if nothing is in the queue
    * You will still pay for these responses
* Long polling:
    * Periodically polls the queue
    * Doesn't return a response until a message arrives int he message queue or
    until the long poll times out
    * Can save money
    * Long polling is generally preferable to short polling

## Exam tips
* Visibility timeout defaults to 30 seconds and max is 12 hours
* Short polling - returns responses immediately, even if it is empty. Costs per response.
* Long polling - returns responses when there is content or a timeout. Saves costs.

