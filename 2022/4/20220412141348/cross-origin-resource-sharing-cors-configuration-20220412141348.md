---
path: '/2022/4/cross-origin-resource-sharing-cors-configuration-20220412141348'
title: 'cross origin resource sharing CORS configuration'
date: '20220412141348'
category: 'aws'
tags: ['CORS', 'aws', 's3', 'developer associate', 'certification']
---

# cross origin resource sharing CORS configuration
Cross origin resource sharing allows things like S3 bucket objects to be accessed from
another bucket.

Example architecture for CORS setup:
![Two S3 buckets with files referencing each other](./20220412141413-img-1.png)

## Enabling CORS
Open the `Cross-Origin resource sharing configuration` in S3.

Paste the URL for the bucket you'd like to access. Ensure that the headers settings
are also pasted in.

