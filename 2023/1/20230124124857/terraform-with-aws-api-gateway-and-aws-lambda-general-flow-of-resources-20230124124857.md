---
path: '/2023/1/terraform-with-aws-api-gateway-and-aws-lambda-general-flow-of-resources-20230124124857'
title: 'terraform with aws api gateway and aws lambda general flow of resources'
date: '20230124124857'
category: 'terraform'
tags: ['iac', 'aws', 'lambda', 'api gateway']
---

# terraform with aws api gateway and aws lambda general flow of resources
Terraform is a bit unwieldy looking when working with API Gateway, this is due to the
shear number of resources required to stand up a simple API Gateway that talks to a
few lambdas.

The general flow of resources:
1. API Gateway itself
1. API Gateway Resource for each path portion
    1. Example: `/test` has a resource for `test`
    1. Example: `/test/other` has 2 resources for `test` and `other`, where `other` references `test` as a parent
1. API Gateway Method for each path portion that requires a method (GET/POST/etc.)
    1. Note: These are registered to the paths that have a method, not each resource
1. API Gateway Integration for each method that was created
1. API Gateway Deployment once all resources are created

**Note:** The below is an example, but utilizes some older Terraform versions for modules
and whatnot. This is likely not the most up-to-date representation of the individual
attributes, but the general workflow of resources is the same.

* [Good StackOverflow reference](https://stackoverflow.com/questions/39040739/in-terraform-how-do-you-specify-an-api-gateway-endpoint-with-a-variable-in-the)

## Example implementation
Below are stubbed examples of a barebones API Gateway deployment in Terraform.
I'm creating a few paths and one that accepts an argument, then passes this
to a registered AWS Lambda.

```hcl
################
# API Gateway  #
################
resource "aws_api_gateway_rest_api" "example_rest_api" {
    name = "example-name"
    description = "example API Gateway"
}

################
# Path proxies #
################
# Path: test/
resource "aws_api_gateway_resource" "proxy_test" {
    rest_api_id = aws_api_gateway_rest_api.example_rest_api.id
    parent_id = aws_api_gateway_rest_api.example_rest_api.root_resource_id
    path_part = "test"
}

# Path: test/endpoint_one
resource "aws_api_gateway_resource" "proxy_endpoint_one" {
    rest_api_id = aws_api_gateway_rest_api.example_rest_api.id
    parent_id = aws_api_gateway_rest_api.proxy_test.id
    path_part = "endpoint_one"
}

# Path: test/endpoint_one/{userId}
resource "aws_api_gateway_resource" "proxy_userid" {
    rest_api_id = aws_api_gateway_rest_api.example_rest_api.id
    parent_id = aws_api_gateway_rest_api.proxy_endpoint_one.id
    path_part = "{userId}"
}

#######################
# Method registration #
#######################
# Path: test/endpoint_one/{userId}
resource "aws_api_gateway_method" "lambda_method_userid_endpoint" {
    rest_api_id = aws_api_gateway_rest_api.example_rest_api.id
    resource_id = aws_api_gateway_resource.proxy_endpoint_one.id
    http_method = "GET"
    authorization = "AWS_IAM"
}

#######################
# Integrate lambdas   #
#######################
resource "aws_api_gateway_integration" "lambda_userid_integration" {
    depends_on = [
        module.userid_lambda,
    ]
    rest_api_id = aws_api_gateway_rest_api.example_rest_api.id
    resource_id = aws_api_gateway_resource.proxy_userid.id

    # Required method for lambda
    integration_http_method = "POST"
    type = "AWS_PROXY"
    uri  = "arn:aws:apigateway:${local.region}:lambda:path/2015-03-31/functions/${module.userid_lambda.lambda_function_arn}/invocations"
}

############################
# API Gateway deployment   #
############################
resource "aws_api_gateway_deployment" "example_deployment" {
    depends_on = [
        module.userid_lambda,
    ]
    rest_api_id = aws_api_gateway_rest_api.example_rest_api.id
    stage_name  = local.env
}

###################
# Create lambdas  #
###################
module "userid_lambda" {
    # Something here to create a lambda!
}
```

