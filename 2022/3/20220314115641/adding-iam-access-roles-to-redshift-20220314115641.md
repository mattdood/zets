---
path: '/2022/3/adding-iam-access-roles-to-redshift-20220314115641'
title: 'adding iam access roles to redshift'
date: '20220314115641'
category: 'redshift'
tags: ['aws', 'redshift', 'iam', 'aws cli', 'terraform', 'dba']
---

# adding iam access roles to redshift
RedShift requires IAM roles to be associated with it for provisioned access to the
database cluster.

This is a great feature; however, for some reason the user interface within the AWS
console won't always update with available IAM roles to associate to the cluster.

### Resources
Here are a few resources about RedShift IAM access, provisioning, and default roles.
* [IAM policies for RedShift](https://docs.aws.amazon.com/redshift/latest/mgmt/redshift-iam-access-control-identity-based.html)
* [Associating an IAM role to RedShift clusters (new/original console)](https://docs.aws.amazon.com/redshift/latest/dg/c-getting-started-using-spectrum-add-role.html)
* [RedShift AWS CLI commands](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/redshift/index.html)
* [Creating a default RedShift IAM role](https://docs.aws.amazon.com/redshift/latest/mgmt/default-iam-role.html)
* [Authorizing RedShift to access AWS services](https://docs.aws.amazon.com/redshift/latest/mgmt/authorizing-redshift-service.html)

## Terraform
One way around this is to utilize a tool like Terraform, wherein your roles are
associated at the module/resource level, but this is effectively the same as using the AWS
CLI tool.

**Note:** [As of Terraform version 4.5.0 it doesn't seem that default IAM roles are assignable
within the resource module.](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/redshift_cluster)

Example Terraform resource:
```terraform

resource "aws_redshift_cluster" "my_example_cluster" {
  # a bunch of config here
  # ...
  iam_roles = [
    "role-1",
    "role-2",
    "role-3",
    "...",
    "role-n"
  ]
}
```

## AWS CLI
The AWS CLI also has a method for getting around this UI issue, so long as you're
certain the role that will be associated has the properly configured access credentials.

[Here's a link to the documentation on the CLI command](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/redshift/modify-cluster-iam-roles.html)

**Note:** This will require your local credentials/config to be set in the place that
you're running this command from.

Example command to add a role to the RedShift cluster:
```bash
aws redshift modify-cluster-iam-roles \
    --cluster-identifier my_example_cluster
    --add-iam-roles arn:aws:iam::123567891012:role/my-role-group/my-role-name
```

