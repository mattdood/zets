---
path: '/2022/2/aws-iam-introduction-20220202141528'
title: 'aws iam introduction'
date: '20220202141528'
category: 'aws'
tags: ['iam', 'developer associate', 'exam', 'certification']
---

# aws iam introduction
IAM is entirely related to setting up users and granting those users access to
the AWS console.

This allows us to manage users and their level of access to the AWS console.

## Basics
* Centralized control of an AWS account
* Shared access to the AWS account
* Granular permissions on a service-by-service Basics
* Identity federation (supports providers like active directory, facebook, linkedin)
    * This is similar to SSO
* Multi-Factor auth support for independent authenticattion mechanisms (ex: token generators)
* Temporary access control for users/devices/services as necessary
    * We could configure temp access to resources for users
* Password rotation policies
* Integrates with most (maybe all) AWS services
* Allows integration with payment some major processors

### Users, groups roles
* Users - end users (people)
* Groups - collection of users under 1 set of permissions (like a department of people)
* Roles - defines a set of permissions that can be assigned to users/applications/services to give access to AWS resources
    * Ex: We could configure access to a specific resource and grant it to 1 part of an app
    * **Note:** Tightly coupled with security

### IAM policies
Policies are a document (json) that defines one or more permissions that can be granted.

These permissions are then *attached* to a user, group, or role and provide granular
control over the permissions granted.

