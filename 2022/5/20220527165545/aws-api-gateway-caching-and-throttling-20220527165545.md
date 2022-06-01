---
path: '/2022/5/aws-api-gateway-caching-and-throttling-20220527165545'
title: 'aws api gateway caching and throttling'
date: '20220527165545'
category: 'aws'
tags: ['developer associate', 'certification', 'api gateway', 'caching', 'throttling']
---

# aws api gateway caching and throttling
API Gateway supports caching endpoint responses for requests made to your API.
Throttling enables you to control API throughput while ensuring you're not
overwhelming your application.

## Benefits of caching
* Reduces the number of calls made to your endpoint
* Can improve latency for requests to your API

## Defaults
* TTL (time-to-live) for caching is in seconds - defaulting to 300 seconds.

## API Gateway returns the cached calls
* When called, the API Gateway will check the cache to determine if the response
already exists
* To improve the performance of the API not all calls will have to hit the backend (server)

## Account level throttling
The purpose of API Gateway throttling is to prevent your API from being overwhelmed
by too many requests.
* Default limits - limits steady-state request rate to 10,000 requests per second, per region
* Concurrent requests - the maximum concurrent requests is 5,000 requests across all APIs per region
    * The limit can be increased on request.
* 429 error - If you exceed the 10k requests/s or 5k concurrent requests you receive
a `429 Too Many Requests` error message

## Exam tips
* Caching:
    * Improve performance of your APIs by caching the output of calls to avoid calling backend every time
    * TTL - time to live for cached responses is 300 seconds by default
    * Reduces the number of API calls, latency
* Throttling:
    * Default of 10,000 requests per second
    * Default of 5,000 concurrent requests
    * `429` errors are thrown for too many requests
    * This exists to keep you from being overwhelmed by too many requests

