---
title: "Github Actionsの設定"
emoji: "🐷"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["github"]
published: true
---

# GitHub Actionsの設定

## クイックスタート

https://docs.github.com/en/actions/quickstart


`.github/workflows/`以下にYAMLを追加する。
YAMLファイルに以下のように設定

```yaml:.github/workflows/actions.yml
name: GitHub Actions Demo
on: [push]
jobs:
  Explore-GitHub-Actions:
    runs-on: ubuntu-latest
    steps:
      - run: echo "🎉 The job was automatically triggered by a ${{ github.event_name }} event."
      - run: echo "🐧 This job is now running on a ${{ runner.os }} server hosted by GitHub!"
      - run: echo "🔎 The name of your branch is ${{ github.ref }} and your repository is ${{ github.repository }}."
      - name: Check out repository code
        uses: actions/checkout@v3
      - run: echo "💡 The ${{ github.repository }} repository has been cloned to the runner."
      - run: echo "🖥️ The workflow is now ready to test your code on the runner."
      - name: List files in the repository
        run: |
          ls ${{ github.workspace }}
      - run: echo "🍏 This job's status is ${{ job.status }}."
```

https://github.com/akinoriakatsuka/github-actions-sample
