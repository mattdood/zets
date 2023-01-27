---
path: '/2023/1/github-reusable-workflows-and-actions-are-great-20230126182036'
title: 'github reusable workflows and actions are great'
date: '20230126182036'
category: 'cicd'
tags: ['github', 'git', 'cicd']
---

# github reusable workflows and actions are great
Lately I've been working on creating as close to a "single source of truth" as
possible for my projects. This has been something I've suffered from for a little
while as the number of projects I start and work on increases.

My goal with centralizing my workflows and actions is to simplify the way that
I manage the business logic while keeping the output the same (or as close to it as I can
for standard projects).

### References
* [reusing workflows](https://docs.github.com/en/actions/using-workflows/reusing-workflows)
* [accessing workflow_run completion status](https://github.com/orgs/community/discussions/26238)
* [waiting for workflow_run to complete](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows#workflow_run)
* [creating composite actions](https://docs.github.com/en/actions/creating-actions/creating-a-composite-action)

## Approach
The intent with this endeavor is to have a single source for templates, then
have reference to these from outside projects.

### Project structure
The `common-ci` project I created uses the below format.

```
common-ci/
    .github/
        actions/
            sample-action-name/
                action.yml
        workflows/
            languagename-ci.yml
            languagename-release.yml
```

### Example workflow
Below is an example workflow, this illustrates that the workflow happens `on: workflow_call:`.
Similar to how we'd define the job structure in a project repo, we can generalize
enough that we can create this generic template.

```
# common-ci/.github/workflows/languagename-ci.yml
name: Golang-CI

on:

  workflow_call:

jobs:

  makefile-check:
    name: makefile
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code Repository
        uses: actions/checkout@v3

      - name: Makefile exists?
        uses: mattdood/common-ci/.github/actions/makefile-check@v0.0.3

  fmt:
    name: fmt
    needs: [makefile-check]
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code Repository
        uses: actions/checkout@v3

      - name: Setup Go
        uses: actions/setup-go@v3

      - name: Fmt
        run: make fmt
```

### Reference structure in a project
Assume that we have a project (`sample-project/`) with a workflows folder for
GitHub. In the below example we're able to have 2 pipelines (`CI`, `Golang-Release`)
that execute with different triggers while invoking the `common-ci` pipeline.

As an added bonus, the `release.yml` is also waiting for the workflow execution
of the `CI` pipeline ***prior*** to executng itself.

```yml
# sample-project/.github/workflows/ci.yml
name: CI

on:

  pull_request:

  push:
    branches: ["master", "main"]
    paths-ignore: ["docs/**"]

jobs:

  ci:
    uses: mattdood/common-ci/.github/workflows/golang-ci.yml@v0.0.4

# sample-project/.github/workflows/release.yml
name: Golang-Release

on:

  workflow_run:
    workflows: [CI]
    types: [completed]
    branches: ["master", "main"]

  push:
    branches: ["master", "main"]
    tags:
      - v*

jobs:

  release:
    uses: mattdood/workflows.github/workflows/golang-release.yml@v0.0.4
    secrets:
      GH_TOKEN: ${{ secrets.GITHUB_TOKEN }}
    if: ${{ github.event.workflow_run.conclusion == 'success' }}
```

