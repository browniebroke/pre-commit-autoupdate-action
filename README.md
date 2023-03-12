# Pre-commit autoupdate action

A Github action to run `pre-commit autoupdate` and send pull request if any updates is required.

> **Note**
>
> This action can be replaced by [a reusable workflow](https://github.com/browniebroke/github-actions#pre-commit-auto-update), which reduces the boilerplate needed.
> 
> If your project is open source, you might want to consider [pre-commit.ci](https://pre-commit.ci/), which runs auto-update weekly on Monday.

Example of workflow:

```
name: Pre-commit auto-update

on:
  # every day at midnight
  schedule:
    - cron: "0 0 * * *"
  # on demand  
  workflow_dispatch:

jobs:
  auto-update:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      
      - uses: actions/setup-python@v2
      
      - uses: browniebroke/pre-commit-autoupdate-action@main
      
      - uses: peter-evans/create-pull-request@v3
        with:
          token: ${{ secrets.GITHUB_TOKEN }}
          branch: update/pre-commit-hooks
          title: Update pre-commit hooks
          commit-message: "chore: update pre-commit hooks"
          body: Update versions of pre-commit hooks to latest version.
```
