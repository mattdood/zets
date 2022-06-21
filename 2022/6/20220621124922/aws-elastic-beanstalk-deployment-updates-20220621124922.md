---
path: '/2022/6/aws-elastic-beanstalk-deployment-updates-20220621124922'
title: 'aws elastic beanstalk deployment updates'
date: '20220621124922'
category: 'aws'
tags: ['developer associate', 'certification', 'elastic beanstalk']
---

# aws elastic beanstalk deployment updates
There are several options for deployment updates in elastic beanstalk.

**Types of deployment updates:**
* All at once - deploys to all hosts concurrently
* Rolling - deploys the new version in batches
* Rolling with additional batch - launches an additional batch of instances, then
deploys the new version in batches
* Immutable - deploys the new version to a fresh group of instances before deleting
the old instances
* Traffic splitting - Installs the new version of the application on a new set of instances,
like an immutable deployment, then forwards a percentage of incoming traffic to the new
application
    * This allows for testing new versions before fully committing

## All at once deployment
* All application instances are deployed simultatneously, incurring a "total outage"
    * Not ideal for mission-critical production systems
    * If the update fails then you have to rollback changes by redeploying the original
    version to all instances, creating a secondary outage
* The only real time you'd use this would be a development or test environment because
it is quick to execute

## Rolling deployment
* Deploys the new version in batches, each batch is taken out of service while
the deployment takes place
* No outages for this deployment
* The capacity will be reduced by the number of instances in a batch while the
deployment takes place
* Not ideal for performance sensitive systems

## Rolling with additional batch
* Launches a new instance batch, then deploys the new version to each batch one at a time
* This ensures capacity is maintained because there is no degraded performance
* If the update fails, you need to perform an additional rolling update to roll
back changes to the app
* When a system is highly available and requires lots of traffic capacity, the time
for rollbacks is likely not suitable

## Immutable deployments
* Deploys the new version as a completely new batch
* Only when the new instances pass their health checks, should the old instances be
terminated and removed
* Deployments are completely separate from the live environment, so if an update
fails your rollback is basically immediate
* This is the preferred approach for mission cirtical systems

## Traffic splitting
* An extension of an immutable deployment, enabling "canary testing"
* It's the ability to test deployments during the update setup by directing parts
of the traffic to the new deployment version
* Creates a new set of instances like an immutable deployment, then forwards that
percentage of client traffic to the new version for a specified evaluation period
    * Version 1 may get 90% of the traffic
    * Version 2 may get 10% of the traffic
    * If the instances stay healthy, then forward 100% of the traffic and terminate
    the old ones
    * Provides early indication of any issues

## Exam tips
* Remember each of the deployment types
    * All at once - service interruption with rolling back requiring another downtime
    * Rolling - reduced capacity during deployment, requires further rolling update for rollback
    * Rolling with additional batch - no reduced capacity during deployment, requires
    further rolling update for rollbacks
    * Immutable deployments - creates a new set of instances then swaps over, good
    for mission critical systems
    * Traffic splitting - similar to immutable deployments, provides time to test the
    new version to get indication of issues by using real client traffic on new instances

