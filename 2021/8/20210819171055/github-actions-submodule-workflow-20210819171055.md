---
path: '/2021/8/github-actions-submodule-workflow-20210819171055'
title: 'github actions submodule workflow'
date: '20210819171055'
category: 'git'
tags: ['github', 'github actions', 'git']
---

# github actions submodule workflow
My personal website utilizes my `zets/` repository from GitHub to generate content.

In order to create a clean continuous deployment process I leveraged GitHub Actions
to update a submodule of the `zets/` repo. This helped to keep my notes repo
entirely separate from the actual site, something that I wanted to be sure I could
maintain.

## Adding the submodule
The submodule is added and updated using the below commands. This requires a
`.gitmodules` file as well.

```bash
# add the repo
git submodule add https://github.com/username/repo

# initialize from the `.gitmodules`
git submodule update --init --recursive
git submodule udpate --recursive --remote
```

## Drafting the GitHub Action
The action itself is set to run nightly at midnight. The scheduling was chosen for
two reasons:
1. I often don't know when I'll be writing in my notes folder.
1. If it was scheduled on push to the `zets/` child repo the action would be in 2 parts:
    1. Child -> parent updating
    1. Parent committing

By having a schedule I was able to mitigate this and keep things separate, which
was my goal from the start.

Sources for the build:
1. [A portion of this StackOverflow comment](https://stackoverflow.com/a/68213855/12387496)
1. [The same StackOverflow thread, different portion](https://stackoverflow.com/a/67583133/12387496)
1. [This site for Cron job scheduling](https://cron.help/every-day-at-midnight)

This is my actual `submodules.yml` file for the workflow. I used a "private access token"
on GitHub specific to this repo only, use these at your discretion.

GitHub links to set this up:
1. [Personal Access Tokens](https://github.com/settings/tokens)
1. Secrets: https://github.com/username/repo/settings/secrets/actions

```yaml

name: Update Submodules
on:
  schedule:
  # run daily at midnight
  - cron: '0 0 * * *'
  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

jobs:
  update:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2

        # Uses the private access token from above link
        with:
          token: ${{ secrets.PRIVATE_TOKEN_GITHUB }}

      # Initialize or update each one recursively
      - name: Pull & update submodules recursively
        run: |
          git submodule update --init --recursive
          git submodule update --recursive --remote

      # Commit to the repo under the GitHub actions user to ensure we have
      # reasonable logging to trace back
      - name: Commit & push changes
        run: |
          git config --global user.email "actions@github.com"
          git config --global user.name "GitHub Actions - update submodules"
          git commit -am "Update submodules" || echo "No changes to commit"
          git push

```

