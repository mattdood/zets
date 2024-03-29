---
path: '/2022/3/github-actions-conditional-environment-variables-20220325012837'
title: 'github actions conditional environment variables'
date: '20220325012837'
category: 'cicd'
tags: ['github', 'bash']
---

# github actions conditional environment variables
**Update 1/4/2023:** The original psot contained an error that did not have
proper variable scope in mind when working with the builtin GitHub actions
variables. The code has since been fixed, though the solution that I recommend
to avoid the verbosity of this setup is still recommended.

Working with GitHub actions is often nicer than GitLab's CI pipelines because it offers
readability (with less verbose includes), simpler stage dependencies, and less reliance on
the `rules` flag.

However, when creating an environment variable for stages, I found that I couldn't follow
the documentation on the site. This was related to using the `$GITHUB_ENV` to do
environment changes from within a job step, oddly enough it would fail stating that it
was an invalid name.

Example configuration:
```yml
  env_vars:
    runs-on: ubuntu-latest
    steps:
      - name: Set Stage
        run: |
          echo "Discovering the environment stage:"
          if [[ ${{ github.ref == 'refs/heads/master' }} ]]; then
            echo "STAGE=prod" >> $GITHUB_ENV
          else
            echo "STAGE=dev" >> $GITHUB_ENV
          fi
          echo "Environment stage is set:"
          echo "${{ GITHUB_ENV }}"
```

**Note:** I break this down below as well, but we essentially check the head reference
for our `master` branch, then return the value as either `prod` if it matches, or `dev` otherwise.

[Documentation regarding the environment variable creation](https://docs.github.com/en/actions/using-workflows/workflow-commands-for-github-actions#environment-files)

## Working around GITHUB_ENV in a cleaner way
My workaround for this environment variable setup was to utilize a ternary operator styled
approach within the `env` stage at a global level.

Example for a dev/prod configuration:
```yml
env:
  STAGE: ${{ github.ref == 'refs/heads/master' && 'prod' || 'dev' }}
```

Breaking down what's written above, we have:
1. A `STAGE` variable being set
1. The `github.ref` head is checked against our `master` branch
1. If the branch matches `master`, then use `prod`
1. If the branch doesn't match `master`, then use `dev`

## Bonus, echoing our vars after setting them
I think it's important to have some verbosity when running CI/CD pipelines, especially when
extending functionality. Often times when we're setting up environments for deployment,
if we don't know "what we have" then we won't be able to determine missing configurations.

As such, I like to include a job to echo our vars (not our secrets) to keep things transparent.

```yml
jobs:

  env_vars:
    runs-on: ubuntu-latest
    steps:
    - name: Echo Env Vars through Context
      run: |
        echo "$GITHUB_CONTEXT"
```

