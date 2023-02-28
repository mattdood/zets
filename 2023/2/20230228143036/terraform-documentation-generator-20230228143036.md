---
path: '/2023/2/terraform-documentation-generator-20230228143036'
title: 'terraform documentation generator'
date: '20230228143036'
category: 'terraform'
tags: ['documentation', 'generator']
---

# terraform documentation generator
When using Terraform it's great to have documentation on variables, resources,
and outputs. It makes for a simple `README.md` addition that adds value to the
folder housing your infrastructure - making things easier to understand at a glance.

A great tool that I've been introducted to is [terraform-docs](https://terraform-docs.io/user-guide/introduction/).

## Example command usage
**Note:** the command below is append only so it will duplicate output on multiple executions

Terraform documentation command:
```bash
terraform-docs markdown table --sort-by required . >> README.md)
```

