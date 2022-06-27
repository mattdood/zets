---
path: '/2022/6/aws-cloudformation-nested-stacks-20220627132534'
title: 'aws cloudformation nested stacks'
date: '20220627132534'
category: 'aws'
tags: ['developer associate', 'certification', 'cloudformation', 'iac']
---

# aws cloudformation nested stacks
nested stacks allow for re-use of CloudFormation code for common use cases. This
could be for sharing standard configurations for things like web servers or application
servers.

Instead of copying the code each time, create a standard template for each common
use case and reference that from another template.

## CloudFormation Template Structure
An example CloudFormation template is below, showing the `TemplateURL` and `Type`
for the nested stack that will be created.

**Note:** The `TemplateURL` is a file that **must** exist in an S3 bucket.

```yml
Resource:
Type: AWS::CloudFormation::Stack
Properties:
  NotificationARNs:
    - String
Parameters:
    AWS CloudFormation Stack Parameters
  Tags:
    - Resource Tag
  TemplateURL: https://s3.amazonaws.com/.../template.yml
  TimeoutInMinutes: Integer
```

## Exam tips
* Code re-use using existing CloudFormation templates
* Useful for frequently used configurations for anything that gets created often

