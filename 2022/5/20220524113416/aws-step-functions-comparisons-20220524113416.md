---
path: '/2022/5/aws-step-functions-comparisons-20220524113416'
title: 'aws step functions comparisons'
date: '20220524113416'
category: 'aws'
tags: ['step functions', 'state machines', 'developer associate', 'certification']
---

# aws step functions comparisons
Step functions provide various types of state machines that have different
workflows to cater to a variety of tasks that can be orchestrated.

The kind of task that is being orchestrated determines the type of workflow to use.

## Standard workflows
* Long-running - durable, long-running, and auditable workflows that may run for
up to a year. Full execution history is available for 90 days.
* At-most-once - Tasks are never executed more than once unless specifying retry actions
* Non-idempotent actions - when processing payments, we only want it to execute once
* Change in state? - A request is non-idempotent if it **always causes a change in state**
    * Ex: Charging a credit card or sending an email

## Express workflows
* Short-lived - up to 5 minute execution
* Great for high-volume, event-processing-type workloads
* At-least-once - ideal if there is possibility an execution will be run more than once
    * Or if there are multiple concurrent executions
* Idempotent - example - transforming input data and storing the result in DynamoDB
* Identical request - has no side effect
    * A result is idempotent if the results will always be the same

### Synchronous express workflow
Great for operations that are performed one at a time. The workflow must complete
before the next step begins.
1. Begins a workflow
1. Waits until it completes
1. Returns the result

### Asynchronous express workflow
Great for services that don't depend on the completion of the workflow.
1. Begins a workflow
1. Confirms the workflow has started
1. The result of the workflow is available in CloudWatch Logs
    1. Does **not** wait on the results of a workflow before accomplishing another task

