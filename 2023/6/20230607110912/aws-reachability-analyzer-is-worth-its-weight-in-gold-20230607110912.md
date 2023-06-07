---
path: '/2023/6/aws-reachability-analyzer-is-worth-its-weight-in-gold-20230607110912'
title: 'aws reachability analyzer is worth its weight in gold'
date: '20230607110912'
category: 'aws'
tags: ['aws network management', 'vpc', 'networking']
---

# aws reachability analyzer is worth its weight in gold
This is a shoutout to the Reachability Analyzer developers, y'all rock.

I have been using the AWS Network Manager tool "Reachability Analyzer" to handle
going from `Elastic Network Interface (ENI) <-> Some Destination (security group/route/IP/etc.)`
successfully for troubleshooting.

The great part is that it shows you within a minute or two whether or not the network
route you're trying is "reachable". Additionally, the *cost basis* appears to only
be about $0.10/run!
