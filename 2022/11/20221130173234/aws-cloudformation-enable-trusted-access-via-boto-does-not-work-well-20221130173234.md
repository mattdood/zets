---
path: '/2022/11/aws-cloudformation-enable-trusted-access-via-boto-does-not-work-well-20221130173234'
title: 'aws cloudformation enable trusted access via boto does not work well'
date: '20221130173234'
category: 'aws'
tags: ['cloudformation', 'organization']
---

# aws cloudformation enable trusted access via boto does not work well
When working with [CloudFormation StackSets](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/stacksets-orgs-enable-trusted-access.html)
we need to "Enable Trusted Access" to allow the AWS service to manage our resources on our behalf.

While this is a great organization requirement to impose, the unfortunate reality
is that the Boto3 library (and other SDKs) don't **fully** enable the service.

To do so, a user must instead enable this access manually from the service page
(in this case CloudFormation's) which forces a manual step. When working with Boto
to employ some automated setups (of say, a StackSet) we're [unable to fully deploy
due to the improper handling of the Boto call](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/organizations.html#Organizations.Client.enable_aws_service_access).

While we can **technically** use the self-managed permissions model to ensure we
have the permissions to do this on our own, this is even more resources to juggle
when wanting to automate the setup of cross-account stacks.

### References:
* [CloudFormation StackSet permissions](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/stacksets-concepts.html#stacksets-concepts-stackset-permission-models)
* [Setup of self-managed permissions](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/stacksets-prereqs-self-managed.html)
* [CloudFormation pre-requisites to stack set operations](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/stacksets-prereqs.html)

