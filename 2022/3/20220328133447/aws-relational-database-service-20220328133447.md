---
path: '/2022/3/aws-relational-database-service-20220328133447'
title: 'aws relational database service'
date: '20220328133447'
category: 'aws'
tags: ['developer associate', 'certification', 'rds', 'databases']
---

# aws relational database service
The AWS RDS service is a core concept in nearly all applications, providing cloud
hosted storage for anything we'd need.

## Usage
Typically, the RDS database instances are utilized for **Online Transaction Processing**
workloads (OLTP). These are for transactions from applications.

## RDS database engine options
* Microsoft SQL Server
* Oracle
* MySQL
* PostgreSQL
* MariaDB
* Amazon Aurora - An Amazon offering that is compatible with PostgreSQL and MySQL while
being significantly more performant and auto-scaling

## Launching an RDS
RDS provisioning is extremely easy, can be provisioned in minutes, and have the following
features:
* Multi-AZ
* Failover capability
* Automated backups

**Note:** A manual install in your own datacenter (with testing) using the features above
would take upwards of a week to accomplish.

## Differences in workloads
* Online Transaction Processing (OLTP) - processes data from transactions in real-time
    * About data processing and completing large numbers of small transactions in real-time
    * Examples: Customer orders, banking transactions, payments, booking systems
* Online Analytics Processing (OLAP) - processes complex queries of historical data
    * About data analysis using large amounts of data, complex queries, and long running processes
    * Examples: analyzing net profit figures from the past several years, sales forecasting

