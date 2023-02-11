---
path: '/2023/2/terraform-pattern-for-service-based-resource-grouping-20230210205406'
title: 'terraform pattern for service based resource grouping'
date: '20230210205406'
category: 'terraform'
tags: ['iac', 'services']
---

# terraform pattern for service based resource grouping
When working on large projects it gets a little difficult to fully understand
each of the resources and their purpose. As projects grow they tend to have
lots of intermingled components that are difficult to decipher.

I find this to be a little overwhelming when looking at projects with more than
just a few components.

## Breaking things into componenets
To combat this, I've been using a little bit of code repetition to make it
easier to *logically* group the resources.

Exmaple:

```
terraform/
    my_service
        backend.tf
        sqs.tf
        fifo-sqs.tf
        lambdas.tf
        outputs.tf
        variables.tf
        version.tf
```

In the above we can clearly see that we have a set of `.tf` files for our
various resources, a specific "backend", and the associated variables/etc.

The great part about this pattern is that we can group the application's sub-components
into suitable "logical blocks".

## Backend notes
The S3 backend (or whatever remote backend) should use a key that organizes
at enough granularity to separate into workspaces.

Example folder structure:
```
<backend bucket name>/
    <account id>/
        <region>/
            <env stage name>/
                <service name>/
                    terraform.state
```

Example with placeholder names:
```
matthews-s3-bucket/
    0123456789012/
        us-east-1/
            dev/
                test_lambda_service/
                    terraform.state
                test_queue_service/
                    terraform.state
            stage/
                test_lambda_service/
                    terraform.state
                test_queue_service/
                    terraform.state
            prod/
                test_lambda_service/
                    terraform.state
                test_queue_service/
                    terraform.state
```

## Difficulties
This is a little tedious to maintain due to the repetition with the `backend.tf`
and the commands you have to run when actually deploying infrastructure.

One might think that another area for pain points might be the introduction
of interdependent resources. This is likely not going to be an issue if the
application is separated into properly discreet blocks.

## Example Makefile targets
I think that the `Makefile` targets make this a lot easier to work with day-to-day.

```makefile
# Makefile
TF_DIR := ./terraform

.PHONY: tf-init-%
tf-init-%:
    cd ${TF_DIR}/$1 && terraform init -upgrade
    cd ${TF_DIR}/$1 && terraform workspace select $* || terraform workspace new $*

.PHONY: tf-plan-%
tf-plan-%:
    cd ${TF_DIR}/$1 && terraform workspace select $*
    cd ${TF_DIR}/$1 && terraform plan -out=plan -input=false

.PHONY: tf-apply-%
tf-apply-%:
    cd ${TF_DIR}/$1 && terraform workspace select $*
    cd ${TF_DIR}/$1 && terraform apply "plan"

.PHONY: tf-destroy-%
tf-destroy-%:
    cd ${TF_DIR}/$1 && terraform workspace select $*
    cd ${TF_DIR}/$1 && terraform destroy
```

