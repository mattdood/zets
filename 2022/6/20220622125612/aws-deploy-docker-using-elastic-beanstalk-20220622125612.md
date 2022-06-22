---
path: '/2022/6/aws-deploy-docker-using-elastic-beanstalk-20220622125612'
title: 'aws deploy docker using elastic beanstalk'
date: '20220622125612'
category: 'aws'
tags: ['developer associate', 'certification', 'containers', 'elastic beanstalk']
---

# aws deploy docker using elastic beanstalk
Elastic Beanstalk supports a number of Docker containers while handling capacity
provisioning, load balancing, scaling, and application health monitoring.

* Single Docker container - you can run a single Docker container on an EC2
instance provisioned by Elastic Beanstalk
* Multiple Docker containers - Use EB to build an ECS cluster and deploy multiple
Docker containers on each instance
* Deploy your code - upload a zip file containing your code bundle and EB will do
the rest
* Upgrade your code - if you want to upgrade your app to a new version, upload
and deploy a revised zip file

**Note:** This can be handled with Terraform as well, then handled with CICD
to upload application zips

