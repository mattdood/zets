---
path: '/2023/2/fixes-required-for-gitlab-golang-host-url-changes-and-nested-subgroups-20230215115154'
title: 'fixes required for gitlab golang host url changes and nested subgroups'
date: '20230215115154'
category: 'golang'
tags: ['gitlab', 'golang', 'vcs']
---

# fixes required for gitlab golang host url changes and nested subgroups
Working with GitLab subgroups and Golang is particularly difficult. When working
with project dependencies that have nested sub-groups in GitLab our Golang
dependency resolution becomes even trickier to handle.

Example:
* Original host: `gitlab.my.organization.com/my-group/project` - a private GitLab host
* New host: `gitlab.com/my-organization/my-group/project` - An organization on GitLab's own site.
    * Note: that our project path has changed. We now have `my-organization/my-group/project` rather than `my-group/project`.

Changes to the Golang files:
* All host URL changes need to be made for every import need to be modified.
    * I have a note about this, using a complex `sed` replace will work!
* Updating the `go.mod` and `go.sum`

```
# go.mod

# Old
module gitlab.my.organization.com/my-group/project

# New
module gitlab.com/my-organization/my-group/project

# Requirements old
require (

    gitlab.my.organization.com/my-group/project-2 v0.0.0-xyz-abc

)

# Requirements new
require (

    gitlab.com/my-organization/my-group/project-2 v0.0.0-wvu-def # new hash required on dependent project updates too

)

# Retain a copy of the dependency in this location also
replace gitlab.com/my-organization/my-group/project-2 => gitlab.com/my-organization/my-group/project-2.git v0.0.0-wvu-def
```

## Steps to resolve golang issues
1. Remove `go.mod` and `go.sum` completely
    1. Note: Technically we can remove `go.sum` and just remove all dependencies from `go.mod` but keep the module and go version lines.
1. Run `go mod tidy -e`, this will allow us to resolve dependencies but may fail on the `mock` portions, this will be resolved later.
    1. `-e` states that for errors we simply continue without failing.
1. Run `go generate ./...` to generate any mocks now that *most* dependencies are resolved.
1. Re-run `go mod tidy -e` to catch any mock related issues that were found in the previous step.

