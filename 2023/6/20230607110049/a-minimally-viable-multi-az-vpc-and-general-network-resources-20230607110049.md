---
path: '/2023/6/a-minimally-viable-multi-az-vpc-and-general-network-resources-20230607110049'
title: 'a minimally viable multi az vpc and general network resources'
date: '20230607110049'
category: 'aws'
tags: ['networking', 'vpc', 'aws network management']
---

# a minimally viable multi az vpc and general network resources
Learning about AWS network resources gave some challenges to wrap my head around
when tasked with creating a Multi-AZ deployment.

This is something that takes quite a while to grok, and even longer to one-line-change-deploy
my way to victory.

I find that these resources are often a bit small in Terraform (only a few lines),
but it's the sheer **number** of them that makes it a little challenging to wrap
my head around the architecture.

To avoid that, this is a list of the "minimally viable" requirements for a good
network.

## Resources
This resource list is non-exhaustive, and does not include application specific
resources but instead is strictly related to bare bones VPC requirements.

I have attempted an "order" of what the dependency Graph Terraform creates **kind of looks like**:
1. VPC
    1. Main route table (empty)
1. Route tables
    1. Private route table
    1. Public route table
1. Subnets
    1. Private subnets (a, b, c) for your region
        1. Assign to Private Route table
    1. Public subnets (a, b, c) for your region
        1. Assign to Public Route table
1. Internet Gateway (a, b, c)
    1. Assign to all Public subnets
1. NAT Gateway (a, b, c) with Elastic IP
    1. Assign to all Private subnets
1. Security groups
    1. Private general egress (outbound `0.0.0.0/0`) to allow private resources to download things
        1. Assign to Private resources
    1. Private general ingress (from known endpoints)
        1. Assign to Private resources that need ingress from known endpoints (like S3 or ECR)
1. VPC Endpoints
    1. S3 for 1 region is good, requires security group rules
        1. Would be assigned to Public/Private Route tables
