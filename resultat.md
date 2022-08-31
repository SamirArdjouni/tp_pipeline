
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
