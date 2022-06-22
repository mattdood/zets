---
path: '/2022/6/aws-codedeploy-features-20220622101534'
title: 'aws codedeploy features'
date: '20220622101534'
category: 'aws'
tags: ['developer associate', 'certification', 'codedeploy', 'cicd']
---

# aws codedeploy features
CodeDeploy offers CICD in various ways, these were covered in a previous note
that had an overview of the different code hosting solutions that AWS offers.

## More nitty gritty features
* In-place deployment:
    * capacity is reduced during the deployment
    * Lambda is not supported
    * Rolling back involves a re-deploy
    * Great when deploying the first time
* Blue/Green deployment:
    * No capacity reduction (safest option)
    * Green instances can be created ahead of time
    * Easy to switch between old and new
    * You pay for 2 environments until you terminate the old servers

