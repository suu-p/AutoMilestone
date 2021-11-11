# AutoMilestone

## Milestone 생성 스크립트 추가

```yaml
name: Create Milestone

on:
  pull_request:
    branches:
      - main

jobs:
  set-milestone:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v2
      - name: 'Create new milestone'
        id: createmilestone
        uses: "WyriHaximus/github-action-create-milestone@v1"
        with:
          title: "test"
        env:
          GITHUB_TOKEN: "${{ secrets.GITHUB_TOKEN }}"

```

## Tag 조회 script

```yaml
name: Echo Tag

on:
  push:
    tags:
      - 'v*.*.*'

jobs:
  echo-tag:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v2

      - name: Set output
        id: vars
        run: echo ::set-output name=tag::${GITHUB_REF#refs/*/}
      - name: Check output
        env:
          RELEASE_VERSION: ${{ steps.vars.outputs.tag }}
        run: |
          echo $RELEASE_VERSION
          echo ${{ steps.vars.outputs.tag }}
```