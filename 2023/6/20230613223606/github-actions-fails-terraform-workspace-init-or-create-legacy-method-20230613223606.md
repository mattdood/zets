---
path: '/2023/6/github-actions-fails-terraform-workspace-init-or-create-legacy-method-20230613223606'
title: 'github actions fails terraform workspace init or create legacy method'
date: '20230613223606'
category: 'terraform'
tags: ['github actions', 'makefile', 'bash', 'terraform', 'iac']
---

# github actions fails terraform workspace init or create legacy method
When working on a pipeline using GitHub Actions I was deploying some code with a Terraform
command that creates a Terraform workspace.

The command used was this:
```bash
terraform workspace new dev || terraform workspace select dev
```

Which produced an unfortunate exit status inside GitHub actions:
```
Workspace "dev" already exists
Error: Terraform exited with code 1.
```

This lead the worker to begin cancelation of the job and proceed with failing, even though
the second end of the command succeeded.

To avoid this, I swapped to using the new (in [Terraform version 1.4.0](https://github.com/hashicorp/terraform/releases/tag/v1.4.0))
`-or-create` flag.

Newly minted command for the CICD pipeline is:
```bash
terraform workspace select -or-create dev
```
