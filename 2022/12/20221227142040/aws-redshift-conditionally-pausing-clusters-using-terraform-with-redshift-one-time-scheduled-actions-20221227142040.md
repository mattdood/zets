---
path: '/2022/12/aws-redshift-conditionally-pausing-clusters-using-terraform-with-redshift-one-time-scheduled-actions-20221227142040'
title: 'aws redshift conditionally pausing clusters using Terraform with redshift one time scheduled actions'
date: '20221227142040'
category: 'databases'
tags: ['terraform', 'iac', 'aws', 'redshift']
---

# aws redshift conditionally pausing clusters using Terraform with redshift one time scheduled actions
Working with Terraform and Redshift together gives us some great behaviors for
provisioning lower environments.

For lower development environments that don't require the cluster to be in an "Available"
state we can set a "time to live" (TTL) to pause the cluster, avoiding costs.

Using Terraform this is pretty easy, we're able to set a "one time" scheduled
action that can pause the cluster at a given time.

### References
* [Redshift scheduled actions](https://docs.aws.amazon.com/redshift/latest/APIReference/API_ScheduledAction.html)
* [Pausing and resuming Redshift clusters](https://docs.aws.amazon.com/redshift/latest/mgmt/managing-cluster-operations.html#rs-mgmt-pause-resume-cluster)
* [Terraform workspaces](https://developer.hashicorp.com/terraform/language/state/workspaces)
* [Terraform time functions](https://developer.hashicorp.com/terraform/language/functions/timeadd)
* [Terraform aws_redshift_scheduled_action](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/redshift_scheduled_action)

## Example of pausing the cluster
Say we use a terraform workspace that checks our "stage" to determine if we're
in a lower environment. Then we also have a default value for our TTL that can
be overridden.

We can override the below by passing a `TF_VAR_redshift_ttl` value at execution
time or by setting it in our environment variables on our machine.

Ex: `TF_VAR_redshift_ttl="1h" terraform plan`

Below is an example of some minimally viable code that conditionally deploys
a "pause" scheduled action 1 time for 15 minutes after cluster provisioning (by default).
This would only deploy to environments that are not `dev` or `prod` as the `terraform.workspace`
name.

```hcl
# main.tf
variable "redshift_ttl" {
  type = string
  description = "Time for the Redshift cluster to be `Available` before pausing. Can be overridden."
}

locals {
  is_dev_or_prod = terraform.workspace == "dev" || terraform.workspace == "prod"

  # Check for TTL override or use the default
  redshift_shutoff_ttl = (
    !local.is_dev_or_prod && (try(var.redshift_ttl, false) || var.my_other_ttl != null)
    ? coalesce(var.redshift_ttl, var.my_other_ttl)
    : "15m" # 15 minute default
  )
}

# Conditional action
resource "aws_redshift_scheduled_action" "conditional_cluster_pause" {
  count = !is_dev_or_prod ? 1 : 0

  name = "my-db-pausing-action"
  schedule = "at(${formatdate("YYYY-MM-DD'T'hh:mm:ss", timeadd(timestamp(), local.redshift_shutoff_ttl))})"
  iam_role = aws_iam_role.conditional_cluster_pause_role.arn
  target_action {
    pause_cluster {
      cluster_identifier = aws_redshift_cluster.my_cluster.cluster_identifier
    }
  }
}

# Example IAM role
resource "aws_iam_role" "conditional_cluster_pause_role" {
  name = "redshift-scheduled-action-role"
  assume_role_policy = jsonencode({
    "Version" : "2008-10-17",
    "Statement" : [
      {
        "Effect" : "Allow",
        "Principal" : {
          "Service" : [
            "redshift.amazonaws.com",
            "scheduler.redshift.amazonaws.com"
          ]
        },
        "Action" : "sts:AssumeRole"
      }
    ]
  })
  inline_policy {
    name = "redshift-scheduled-action-policy"
    policy = jsonencode({
      "Version" : "2012-10-17",
      "Statement" : [
        {
          "Sid" : "",
          "Effect" : "Allow",
          "Action" : [
            "redshift:PauseCluster",
            "redshift:ResumeCluster",
          ],
          "Resource" : "arn:aws:redshift:${local.region}:${local.account}:cluster:my-redshift-cluster"
      }]
    })
  }
}
```

