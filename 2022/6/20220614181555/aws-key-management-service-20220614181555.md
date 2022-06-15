---
path: '/2022/6/aws-key-management-service-20220614181555'
title: 'aws key management service'
date: '20220614181555'
category: 'aws'
tags: ['developer associate', 'certification', 'kms']
---

# aws key management service
A managed service that makes it easy to create and control encryption keys used
to encrypt your data.

The service is seamlessly integrated with many AWS services to make encrypting
data easy (ex: S3, RDS).

By integrating the KMS system with many services it has become very easy to encrypt
data with **encryption keys you manage**.

## When to use KMS?
Whenever you're dealing with sensitive information.

Sensitive data would include:
* Credentials
* Secrets
* Database passwords
* Financial data
* Customer data

## KMS integrates with most other AWS services
* S3
* RDS
* DynamoDB
* Lambda (encrypt/decrypt data)
* Elastic Block Store
* Elastic File System
* CloudTrail (gives an audit trail for all API calls to KMS)
* Developer tools
* Many more

## What is CMK?
* CMK - Customer Master Key - encrypt/decrypt data up to 4KB
* This is used to generate/encrypt/decrypt the "data key"
* The data key - Used to encrypt/decrypt your data

This is known as "envelope encryption".

