---
path: '/2023/6/makefiles-as-a-single-source-of-truth-for-project-commands-20230607104629'
title: 'makefiles as a single source of truth for project commands'
date: '20230607104629'
category: 'applications'
tags: ['design', 'mono repo', 'application architecture']
---

# makefiles as a single source of truth for project commands
I have become more and more enthralled by the idea that we can create a "Makefile to rule them all".

While this approach becomes a behemoth over time, I challenge to find a better approach
than what I will lay out below.

## Requirements
1. A centralized place for project commands (library or application repository)
1. Useful way of viewing all project commands quickly
1. Ability to add documentation to the commands and change them in 1 place
1. CICD and local developers should use the exact same commands
    1. Ensures testability of CICD
    1. Developers can debug any part of the stack from their local machines if needed

## Solution
The best solution I've found thus far has been a comprehensive `Makefile` broken
into many targets. While this file will get large, it does give a necessary
abstraction layer over project commands.

### Setting the scene
A project may use many different tools, with many commands and parameters/config files,
to accomplish the following:
1. Linting (with N number of linters, depending on project complexity)
1. Testing (business logic, unit tests, integration tests, models, infrastructure)
1. Packaging/Building (.zip/.pex/.json/etc. need to be **created** in CICD to be deployed)
1. Deployment (Terraform or some equivalent)

### Makefile
A good `Makefile` won't be defined here, but a skeleton of a few targets to get started
can illustrate the usefullness of having a "single source of truth" for the complex
array of project commands above.

Here we can see a few targets to get us started, a `all` for **local** usage,
`lint`, `test`, and `help`.

```make
###################
####  General  ####
###################

.PHONY: all
all: lint test  ## Local "all" to handle linting and testing in one target. REQUIRES: virtual environment + dependencies.

.PHONY: lint
lint:  ## Uses Pre-Commit to run linters from the `.pre-commit-config.yaml`.
	pre-commit run --all-files

.PHONY: test
test:  ## Uses Pytest to execute all tests.
	pytest -vvv -n auto --showlocals

.PHONY: help
help:  ## Shows available Makefile commands in a list
	@grep -E '^[a-zA-Z_-]+([-%:]|[-%])+.*?## .*$$' $(MAKEFILE_LIST) \
		| sort \
		| awk 'BEGIN {FS = ":.*?## "}; {printf "\033[36m%-30s\033[0m %s\n", $$1, $$2}'
```

Showing the output of `make help`:
```
all                            Local "all" to handle linting and testing in one target. REQUIRES: virtual environment + dependencies.
help                           Shows available Makefile commands in a list
lint                           Uses Pre-Commit to run linters from the `.pre-commit-config.yaml`.
test                           Uses Pytest to execute all tests.
```
