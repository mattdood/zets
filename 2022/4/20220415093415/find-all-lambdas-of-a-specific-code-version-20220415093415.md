---
path: '/2022/4/find-all-lambdas-of-a-specific-code-version-20220415093415'
title: 'find all lambdas of a specific code version'
date: '20220415093415'
category: 'aws'
tags: ['lambda', 'python', 'bash']
---

# find all lambdas of a specific code version
When deprecating Lambda runtimes it is important to have a bird's eye view over
what Lambda versions you're running.

Using the AWS CLI you can check against all Lambdas that you have in your account,
assuming your role has the appropriate access.

The below will need to be rerun for each region, and if checking multiple runtimes
you'd have to run it again for different versions.

Example query run against all Lambdas in us-west-2:
```bash
aws lambda \
    list-functions \
    --function-version ALL \
    --region us-west-2 \
    --output text
    --query "Functions[?Runtime=='python3.6'].FunctionArn" \
    >> matching_lambdas.txt
```

