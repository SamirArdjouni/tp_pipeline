
NF7-DO-03

```yml
name: Conventional Commits

on:
  push:
    branches: [feature/**, hotfix/**]

jobs:
  build:
    name: Conventional Commits
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: webiny/action-conventional-commits@v1.0.5
```


NF8-DO-01
test1

```yml

name: Validate test

on:
  pull_request:
    types: opened

jobs:
  test:
    strategy:
      matrix:
        version: [14.x, 16.x]
    name: Validate test unitaire
    runs-on: ubuntu-latest
    if: startsWith(github.head_ref, 'feature/')
         
    steps:
      - uses: actions/checkout@v2
      - name: Use Node.js Version ${{ matrix.version }}
          uses: actions/setup-node@v3
          with:
            node-version: ${{ matrix.version }}
            cache: 'npm'

```



NF4-DO-01
```yml
name: Creation des branches

on:
  issues:
    types: [assigned]
  issue_comment:
    types: [created]
  pull_request:
    types: [closed]

jobs:
  create_issue_branch_job:
    runs-on: ubuntu-latest
    steps:
      - name: Creation branche
        uses: robvanderleek/create-issue-branch@main
        with:
          branchName: "feature/${issue.number}-${issue.title}"
          defaultBranch: "develop"
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}


```




NF8-DO-04

```yml
name: suppresion de branches
on:
  pull_request:
    types:
      - opened
      - closed
      - edited
      - reopened
jobs:
  automerge:
    runs-on: ubuntu-latest
    steps:
      - name: suppresion de branches
        uses: koj-co/delete-merged-action@master
        with:
          branches: "!main, !develop, *"
        env:
          GITHUB_TOKEN: "${{ secrets.GITHUB_TOKEN }}"


```