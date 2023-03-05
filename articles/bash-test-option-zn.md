---
title: "bashのif文における -z -n オプション"
emoji: "💻"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["bash","シェル"]
published: true
---

# オプション

|  オプション  |  説明  |
| ---- | ---- |
|  -n  |  文字列が空でなければtrue  |
|  -z  |  文字列が空であればtrue  |


## 例

```bash
string=""
if [ -z ${string} ] ; then
  echo "empty";
fi
```
${string}は空文字列なので、emptyが表示される。

```bash
string="hoge"
if [ -n ${string} ] ; then
  echo "not empty";
fi
```
${string}は空文字列ではないのでnot emptyが表示される。

## 補足
[ ] の記法は`test`コマンドの書き換えです。

testコマンドについては[こちら](https://zenn.dev/aki_artisan/articles/bash-test-options)の記事で解説しています。

```
if [ -n "hoge" ] ; then
```
は
```
if test -n "hoge"; then
```
と同じ意味になります。