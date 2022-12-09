---
path: '/2022/12/terraform-planning-a-portion-of-your-resources-20221209133201'
title: 'terraform planning a portion of your resources'
date: '20221209133201'
category: 'terraform'
tags: ['aws', 'terraform', 'cicd', 'devops']
---

# terraform planning a portion of your resources
When running around with Terraform it's pretty annoying to wait for a full plan
if you're only working on a few independent resources. For larger projects this
can eat up several minutes of time.

A quick way to get around this "only in extreme circumstances" (according to Hashicorp)
would be to specify a target in the command. This will focus solely on that resource
and its given dependency graph.

## Example scenario
We have 2 files (`config.tf`, `templates/config.yml.tpl`) with 2 resources
(`data`, `local_file`).

### Structure

Tree:
```
terraform/
    config.tf
    templates/
        config.yml.tpl
```

```hcl
# config.tf
data "template_file" "config_yml" {
    template = "${file("${path.module}/templates/config.yml.tpl")}"
    vars = {
        region = provider.region
        stage = terraform.workspace
    }
}

resource "local_file" "local_config" {
    content = data.template_file.config_yml.rendered
    filename = "../my-config.yml"
}
```

```hcl
# templates/config.yml.tpl

config:
    region: ${region}
    stage: ${stage}
```

### Running a TF plan on this
Terraform plan typically takes everything in your directory, instead we can
take just the `config.tf` by specifying the resource block.

```bash
terraform plan -target local_file.local_config
```

