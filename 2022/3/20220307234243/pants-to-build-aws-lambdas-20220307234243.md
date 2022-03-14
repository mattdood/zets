---
path: '/2022/3/pants-to-build-aws-lambdas-20220307234243'
title: 'pants to build aws lambdas'
date: '20220307234243'
category: 'cicd'
tags: ['aws', 'lambda', 'python', 'pants']
---

# pants to build aws lambdas
Working in a CI/CD pipeline requires the ability to create our build structures
on the fly without a significant amount of hassle. While tooling is great, sometimes
it becomes cumbersome if it does "too many things" or if you're trying to glue
too many tools together.

With [Pants](https://www.pantsbuild.org/v2.10/docs/welcome-to-pants) I've found quite
the opposite, a fantastic use case for building deployment dependencies and keeping them
squared away the way we want.

### Requirements
* [Set up your Pants installation](https://www.pantsbuild.org/v2.10/docs/welcome-to-pants)
* [Read up about lambda functions](https://aws.amazon.com/lambda/)
* [Create a lambda execution role](https://docs.aws.amazon.com/lambda/latest/dg/lambda-intro-execution-role.html)

## Use case
I'm going to demo a quick [AWS Lambda](https://aws.amazon.com/lambda/) build that
will have a few non-traditional components to the build process.

### Setup
Our lambda will be set up in its own folder, with a lambda handler declared inside a file.

```
# aws/test_lambda/lambda_handler.py

def lambda_handler(event, context):
    print("hello world")
    return
```

Additionally, we'll keep our requirements in a separate area that will have a specific
file for our lambda. I like to keep dependencies separate between services as best
we can.

```
# requirements/lambda.txt
# these are python libraries
requests
beautifulsoup4
```

### The BUILD process setup
When working with Pants we'll need to specify `BUILD` files throughout our project.
This is easily done with the builtin setup command that Pants has, then with some
minor tweaking afterward we can configure our lambda environment.

[Pants has some great docs on the AWS lambda support](https://www.pantsbuild.org/v2.10/docs/reference-python_awslambda)

To generate `BUILD` files:
```
# from root of directory
./pants tailor
```

Editing our lambda `BUILD` file:
```
# aws/test_lambda/BUILD

# The default `sources` field will include our handler file.
python_sources(name="test_lambda0")

python_awslambda(
    name="lambda",
    runtime="python3.8",
    handler="lambda_handler.py:lambda_handler",
)

python_requirements(
    source="../../requirements/lambda.txt"
)
```

This will allow our requirements to be specifically called out for 3rd party
packages. [The documentation on this is pretty spot on, if we want to get more specific
in the future.](https://www.pantsbuild.org/docs/python-third-party-dependencies)

To inspect our dependencies, we can run:
```
./pants peek <your file path>
```

### Building the lambda
To build the lambda, we'll utilize our Pants installation to create a .zip of the
project space. This will then be deployed using the AWS CLI to be used in the creation
of our lambda function.

[I'm working off this set of docs for building lambdas](https://www.pantsbuild.org/docs/awslambda-python)

Building our .zip file:
```
# from project root
./pants package aws/test_lambda/lambda_handler.py
```

Deploying our lambda to AWS:
```
cd dist/aws.test_lambda/

aws create-function \
    --function-name test_lambda \
    --runetime python3.8 \
    --zip-file fileb://test_lambda.zip \
    --handler lambdex_handler.handler \
    --role arn:aws:iam:123456789012:role/service-role/MyTestFunction-role-asdf
```

To update our lambda after a separate build:
```
cd dist/aws.test_lambda/

aws update-function-code \
    --function-name test_lambda \
    --zip-file fileb://test_lambda.zip
```

