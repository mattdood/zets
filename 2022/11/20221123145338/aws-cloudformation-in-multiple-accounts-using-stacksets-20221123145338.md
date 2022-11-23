---
path: '/2022/11/aws-cloudformation-in-multiple-accounts-using-stacksets-20221123145338'
title: 'aws cloudformation in multiple accounts using stacksets'
date: '20221123145338'
category: 'aws'
tags: ['cloudformation', 'multi account', 'stackset']
---

# aws cloudformation in multiple accounts using stacksets
When working with CloudFormation it can be a bit annoying when you have a single
entrypoint into an account but need to deploy things into multiple regions/accounts.

The idea that a single CloudFormation Template (CFT) can also deploy
to multiple regions/accounts is a *somewhat* new concept (circa 2019), but useful.

A great use case for this is when you have a master organization-level payer account
that needs resources deployed, but also require connected resources in a
sub-account.

Example organization:

```
my-payer-account
    | my-sub-account
```

Example CFT that can deploy to both:

```yml
AWSTemplateFormatVersion: '2010-09-09'
Description: >-
    Cross account deployment
Parameters:
    SubAccount:
        Type: String
        Description: Sub-account to deploy to

Resources:

    ExampleCrossAccountIAMRole:
        Type: AWS::CloudFormation::StackSet
        Properties:
            StackSetName: "example-stackset"
            Permissionmode: SELF_MANAGED
            StackInstancesGroup:
                - DeploymentTargets:
                    Accounts:
                    - !Sub "${SubAccount}"
            TemplateBody: |
              Resources:
                IAMRole:
                  Type: AWS::IAM::Role
                   Properties:
                     RoleName: "ExampleRole"
                     Description: >-
                       Cross account role
                     AssumeRolePolicyDocument:
                       Version: "2012-10-17"
                       Statement:
                         - Effect: Allow
                           Principal:
                             AWS:
                               - "arn:aws:iam::<my account here>:root"
                           Action:
                             - "sts:AssumeRole"
                           Policies:
                             - PolicyName: "ExamplePolicy"
                               PolicyDocument:
                                 Version: "2012-10-17"
                                 Statement:
                                   - Effect: Allow
                                     Action:
                                       - "<some actions here>"
                                     Resource: "*"
```

