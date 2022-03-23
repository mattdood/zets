---
path: '/2022/3/aws-elastic-load-balancers-20220323152722'
title: 'aws elastic load balancers'
date: '20220323152722'
category: 'aws'
tags: ['developer associate', 'certification', 'elb', 'aws', 'networks']
---

# aws elastic load balancers
Load balancers distribute network traffic across a group of servers. This routes
traffic to different webservers based on things like, round robin or based on which
server is the least busy.

If a single webserver fails, the load balancer will not send requests to it until it
comes online.

Additionally, we can add more webservers as traffic increases and the load balancer can have
them registered then route traffic to it.

## Types of load balancers
1. Application load balancer - http/https
1. Network load balancer - TCP and high performance
1. Classic load balancer (legacy) - http/https and TCP
1. Gateway load balancer - balances workloads for 3rd party virtual appliances running AWS
    * Virtual applicances on the AWS marketplace
    * Virtual firewals like Fortinet, Palto Alto

### Application load balancer
This balances HTTP/HTTPs traffic. These operate at layer 7 (application) of the
OSI model, which makes it application aware.

* Supports advanced request routing to specific web servers based on the HTTP header

Example of an application-level load balancer to route to web servers:

![Routing traffic between different application web servers](./20220323153609-img-1.png)

### Network load balancer
A high performance option for TCP traffic, where extreme performance is needed. Operates
at the layer 4 transport later.

* Handles millions of requests per second with low latency

### Classic load balancer (legacy)
Supports some layer 7 specific features (`X-Forwarded-For`) headers and sticky sessions.
Handles layer 4 load balancing for TCP protocol.

## X-Forwarded-For header
Allows a service to identify the originating IP address of a client connecting through
a load balancer. This enables the application to keep sessions alive while passing
through the load balancer.

## Common load balancer errors
Most comon is the `Error 504 Gateway timeout`. This means that the target server downstream
has failed to respond.

### General troubleshooting
1. Check that the application is alive
1. Determine if the target connection is having issues
1. Check where the app specifically is failing to determine if there are issues with
the connectivity

## Exam tips
* App load balancers routes to web servers based on request types (http/https)
* Network load balancer for high performance (TCP traffic)
* Classic load balancer (http/https/TCP)
* Gateway load balancer for 3rd party appliances
* X-Forwarded-For header to enable sticky sessions

