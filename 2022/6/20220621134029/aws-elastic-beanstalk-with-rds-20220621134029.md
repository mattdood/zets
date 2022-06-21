---
path: '/2022/6/aws-elastic-beanstalk-with-rds-20220621134029'
title: 'aws elastic beanstalk with rds'
date: '20220621134029'
category: 'aws'
tags: ['developer associate', 'certification', 'elastic beanstalk', 'rds', 'databases']
---

# aws elastic beanstalk with rds
Elastic Beanstalk can integrate with RDS in 2 ways: either inside the EB environment
or outside of it.

## RDS inside Elastic Beanstalk
For RDS instances created inside of the environment the instances will be deleted
upon termination of the environment.
    * This is a good option for dev and test deployments, but bad for production.

The termination of the environment lacks flexibility.

## RDS outside Elastic Beanstalk
* Don't use EB to create your RDS instnace
* Use the RDS console or AWS CLI
* Allows teardown of the application environment without affecting the database instance

## Connecting  to an outside RDS database
1. Add an additional security gorup to your environment's autoscaling group
    * Allows for communication on the relevant port of the database
1. Provide connection string information to your application servers using the
Elastic Beanstalk environment properties
    * This is essentially environment secrets
    * Requires the DB string and login credentials

## Exam tips
* Inside Elastic Beanstalk deployments are quick but terminates the database on deletion
* Outside Elastic Beanstalk deployments requires additional security group and
credentials configuration, but is independent from the application stack

