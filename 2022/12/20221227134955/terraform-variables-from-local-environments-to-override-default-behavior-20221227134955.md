---
path: '/2022/12/terraform-variables-from-local-environments-to-override-default-behavior-20221227134955'
title: 'terraform variables from local environments to override default behavior'
date: '20221227134955'
category: 'terraform'
tags: ['iac', 'aws', 'bash']
---

# terraform variables from local environments to override default behavior
Working with Terraform sometimes requires different behaviors across environment
stages (dev/prod/local lower environments).

To accomplish this we can use environment variables that force different
behaviors depending on the local bash variable.

The syntax here to pay attention to is that the `TF_VAR_<your variable name here>`
passes any environment variables to the underlying variable in Terraform.

## Using an environment variable
We can set environment variables in a few different ways. To start, we'll need
a variable to match it to. Either in our normal TF file or a `variables.tf`
depending on code organization.

```hcl
# variables.tf
variable "my_test_variable" {
  type        = string
  description = "My test variable"
}
```

Then we pass the variable value either with a local env variable or as part of
our Terraform execution:
```bash
export TF_VAR_my_test_variable="something"
```

```bash
TF_VAR_my_test_variable="something" terraform plan
```

## Complex examples with overrides
If we have a variable that has no default value we can check for its existence
then provide a default value.

This checks for the `TF_VAR_my_test_variable` or the existence of a `var.my_test_variable`
value passed in.

```hcl
# main.tf
variable "my_test_variable" {
  type        = string
  description = "My test variable"
}

locals {
  my_var_or_default = (
    try(var.my_test_variable, false)
    ? var.my_test_variable
    : "default value"
  )
}
```

With a more complex variable we could check for the existence of other defaults, then
coalesce them together:

```hcl
# main.tf
locals {
  my_var_or_default = (
    try(var.my_test_variable, false) || var.my_other_test_variable != null
    ? coalesce(var.my_test_variable, var.my_other_test_variable)
    : "default value"
  )
}
```

