---
path: '/2022/7/aws-monitoring-services-20220715131002'
title: 'aws monitoring services'
date: '20220715131002'
category: 'aws'
tags: ['developer associate', 'certification', 'cloudwatch', 'cloudtrail']
---

# aws monitoring services
Monitoring in AWS has a few different flavors for various use cases.

## CloudWatch
* CloudWatch - Default #C2 host-level metrics for CPU, network, disk, and status check
    * Use the CloudWatch agent for operating system-level metrics like memory usage,
    processes, and CPU idle time
    * The CloudWatch agent has to be installed separately on the system
* CloudWatch Logs - Monitor and store logs to help you better understand your systems and apps
* CloudWatch Alarms - You can create an alarm to monitor any AWS CloudWatch metric
in your account, generate an alert, or take an action

### CloudWatch concepts to remember
* CloudWatch metrics - a metric is a variable to monitor (Ex: CPU usage of an EC2)
* CloudWatch namespaces - a namespace is a container for CloudWatch metrics
* CloudWatch dimensions - a dimension is a filter to search for metrics
* Cloudwatch dashboard - a custom homepage to display things like important metrics
* Cloudwatch actions - allow you to public, monitor, and alert on a variety of metrics
    * PutMetricData - publishes metric data points to cloudwatch
    * PutMetricAlarm - creates an alarm associated with a metric when a threshold is reached

## Use cases for CloudWatch vs. CloudTrail

### CloudWatch
* Monitors performance and metrics
* CloudWatch logs
* CloudWatch alarms
* Do you need to monitor the performance of AWS resources?

### CloudTrail
* Records your API calls for your AWS account
* API activity history related to creation, deletion, and modification of AWS resources
* Do I need an audit log of user activity in my AWS account?

