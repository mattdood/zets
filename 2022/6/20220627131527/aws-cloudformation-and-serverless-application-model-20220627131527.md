---
path: '/2022/6/aws-cloudformation-and-serverless-application-model-20220627131527'
title: 'aws cloudformation and serverless application model'
date: '20220627131527'
category: 'aws'
tags: ['developer associate', 'certification', 'cloudformation', 'iac', 'serverless', 'sam']
---

# aws cloudformation and serverless application model
The Serverless Application Model is an extension to CloudFormation used to define
serverless applications.

## Features
* Simplified syntax - SAM uses a simplified syntax for defining serverless resources:
    * APIs, Lambda functions, DynamoDB tables, etc.
* SAM CLI - use the SAM CLI to package your deployment code, upload to S3, then
deploy your serverless application

## Packaging and deploying with SAM CLI
The SAM CLI has a few commands for generating cloud resources using CloudFormation.
We use a SAM compatible template that will generate our resources by converting it
to be a SAM template.

We can then deploy that template from S3.

Example:
```bash
sam package \
    --template-file ./mytemplate.yml \
    --output-template-file sam-template.yml \
    --s3-bucket s3-bucket-name

sam deploy \
    --template-file sam-template.yml \
    --stack-name mystack \
    --capabilities CAPABILITY_IAM
```

## Exam tips
* Serverless Application Model (SAM) - Define and provision serverless applications
using CloudFormation
* `sam package` - packages applications and uploads to S3 bucket
* `sam deploy` - deploys a serverless app using CloudFormation

