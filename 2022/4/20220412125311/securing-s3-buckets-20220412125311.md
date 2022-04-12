---
path: '/2022/4/securing-s3-buckets-20220412125311'
title: 'securing s3 buckets'
date: '20220412125311'
category: 'aws'
tags: ['s3', 'certification', 'developer associate']
---

# securing s3 buckets
By default S3 buckets are relatively quite secure.

## Default settings
1. Private - all newly created buckets are private
1. Bucket owner - only the bucket owner can upload new files, read files, delete, etc.
1. No public access - no public (anonymous) access is allowed

## Opening up default settings
1. Bucket policies
    1. Applied at a bucket level - permissions are applied to all objects in the bucket
    1. Not individual objects - can't attach a bucket policy to an individual object
    1. Groups of files - files tha tneed to be accessed by the same people
        1. Example: All users in a team need access to the same objects
    1. Format of bucket policies are similar to IAM policy documents
1. Bucket access control lists (ACLs)
    1. Access control lists - applied at an object level, with different permissions for different objects
    1. Grant access to objects - defined by account or groups with different access types
    1. Fine grained control - different access types granted to different objects in the same bucket
        1. Example: Set some objects for read access by user or group, account, etc.
    1. Allows s3 access logs to be enabled (disabled by default) - logs information on every object request
        1. Logs can be written to a separate S3 bucket

