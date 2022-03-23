---
path: '/2022/3/aws-route-53-domain-name-service-20220323154313'
title: 'aws route 53 domain name service'
date: '20220323154313'
category: 'aws'
tags: ['developer associate', 'certification', 'elb', 'ec2', 'route 53', 'DNS', 'aws', 'networks']
---

# aws route 53 domain name service
The [AWS Route 53](https://aws.amazon.com/route53/) service allows users to create
a domain name service that routes traffic from your domain to web servers.

Example setup for a Route 53 domain -> load balancer -> EC2 instance:

![Sample architecture diagram for a route 53 service to load balancer that routes to ec2](./20220323155143-img-1.png)

**Note:** The AWS domain name registration is roughly $10/year. This will then
be added to the hosted zones area of the AWS console.

**Tip:** If you have issues connecting to an elastic load balancer for the service, always start
by checking the security groups.

