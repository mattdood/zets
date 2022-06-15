---
path: '/2022/6/aws-kms-customer-master-keys-20220614183049'
title: 'aws kms customer master keys'
date: '20220614183049'
category: 'aws'
tags: ['developer associate', 'certification', 'kms', 'customer master key']
---

# aws kms customer master keys
The customer master key is a managed key in the KMS service that the customer
manages.

## Features
* Alias - your application can refer to the alias when using the CMK
* Creation date - the date and time when the CMK was created
* Description - You can ad a description to describe the CMK
* Key state - enabled, disabled, pending, deletion, unavailable
    * Note that there is a 7 day grace period to reverse a deletion when removing
    a CMK
* Stays inside KMS - can never be exported outside of the service

## Exam tips
* The general features of the KMS CMK with an alias, date, description
* The key administrative permissions:
    * IAM users and roles that can administer (but not use) the key through
    the KMS API
* Key usage permissions - the IAM users/roles that can use the key to encrypt/decrypt data
* AWS-managed CMK - the keys used on your behalf for services integrated with KMS.
    * These are managed keys used in the background when encryption is selected
    on creation.

