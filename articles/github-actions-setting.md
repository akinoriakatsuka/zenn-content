---
title: "Github Actionsã®è¨­å®"
emoji: "ð·"
type: "tech" # tech: æè¡è¨äº / idea: ã¢ã¤ãã¢
topics: ["github"]
published: true
---

# æ¦è¦

GitHub Actions ã®ãµã³ãã«ã³ã¼ããã¾ã¨ãã¾ãã

# GitHub Actionsã®è¨­å®

## ã¨ããããè©¦ã

https://docs.github.com/en/actions/quickstart

ãªãã¸ããªãä½æãã¦ã`.github/workflows/`ä»¥ä¸ã«YAMLãè¿½å ããã

```yaml:.github/workflows/actions.yml
name: GitHub Actions Demo
on: [push]
jobs:
  Explore-GitHub-Actions:
    runs-on: ubuntu-latest
    steps:
      - run: echo "ð The job was automatically triggered by a ${{ github.event_name }} event."
      - run: echo "ð§ This job is now running on a ${{ runner.os }} server hosted by GitHub!"
      - run: echo "ð The name of your branch is ${{ github.ref }} and your repository is ${{ github.repository }}."
      - name: Check out repository code
        uses: actions/checkout@v3
      - run: echo "ð¡ The ${{ github.repository }} repository has been cloned to the runner."
      - run: echo "ð¥ï¸ The workflow is now ready to test your code on the runner."
      - name: List files in the repository
        run: |
          ls ${{ github.workspace }}
      - run: echo "ð This job's status is ${{ job.status }}."
```

https://github.com/<ã¦ã¼ã¶ã¼å>/<ãªãã¸ããªå>/actions ã«ã¢ã¯ã»ã¹ããã¨çµæãé²è¦§ã§ãã¾ãã

## ä½¿ç¨éã®ææ¡

https://github.com/settings/billing ã® Usage this month ããè¦ããã¾ãã

## ä¸¦åå¦ç
jobsã¯åºæ¬çã«ä¸¦åã§å¦çããã¾ããä¸ã¤ã²ã¨ã¤ã®jobã®stepã¯é£ç¶çã«å¦çããã¾ãã
jobåå£«ã§é çªãè¨­å®ãããå ´åä»¥ä¸ã®ããã«è¨­å®ãã¾ãã

### ä¸¦åå¦çã®é çªã®è¨­å®

needsã«jobã®ååã¾ãã¯jobã®ååã®éåãæå®ãã¦ãé çªãè¨­å®ãã¾ãã
![](/images/github-actions-setting/image1.png)

```yaml:.github/workflows/actions_parallel.yml
name: Parallel
on: [push]
jobs:
  setup:
    runs-on: ubuntu-latest
    steps:
      - run: echo "setup"
  job1:
    needs: setup
    runs-on: ubuntu-latest
    steps:
      - run: echo "job1"
  job2:
    needs: setup
    runs-on: ubuntu-latest
    steps:
      - run: echo "job2"
  job3:
    needs: setup
    runs-on: ubuntu-latest
    steps:
      - run: echo "job3"
  end:
    needs: ["job1", "job2", "job3"]
    runs-on: ubuntu-latest
    steps:
      - run: echo "end"
```