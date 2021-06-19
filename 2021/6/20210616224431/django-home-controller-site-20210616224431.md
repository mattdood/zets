---
path: '/2021/06/django-home-controller-site-20210616224431'
title: 'Django Home Controller Site'
date: '20210616224431'
category: 'project'
tags: ['home automation', 'project']
---

# django home controller site
When thinking about my Raspberry Pi LED controller idea I realized that a simple
Django site deployed on a Linux desktop using Kubernetes might be perfect to
handle a web interface for it.

## Concepts
* Deploy on home server and serve locally
* Allow local login for us at home
* Send requests to Raspberry Pi devices to control lighting
* Potentially have a reminders app that utilizes SMS to send reminders
    * Accept texts back that would set reminders for that number or both

