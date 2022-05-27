---
path: '/2022/5/aws-x-ray-configuration-20220527164356'
title: 'aws x-ray configuration'
date: '20220527164356'
category: 'aws'
tags: ['developer associate', 'certification', 'x-ray']
---

# aws x-ray configuration
The AWS X-Ray SDK sends data to the X-Ray daemon which buffers segments in a queue and
uploads them to X-Ray in batches.

**Note:** You need both the X-Ray SDK and the X-Ray daemon on your systems

## High-level configuration steps
Remember to have the:
* X-Ray SDK
* X-Ray daemon

* On premises & EC2 instances:
    * Install the X-Ray daemon on your EC2 instance or on-premises server
* Elastic Beanstalk
    * Install the X-Ray daemon on the EC2 instances inside your Beanstalk
* Docker on ECS:
    * Install the X-Ray daemon in its own Docker container

## Annotations and indexing
* Annotations
    * When instrumenting your application you can record additional information
    about requests using annotations
* Key-value pairs
    * Annotations are key-value pairs that are indexed for use with filtering
    expressions
    * Filters enable searching and grouping of data

