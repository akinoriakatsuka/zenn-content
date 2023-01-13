---
title: "Gitでよく使うコマンド"
emoji: "🦁"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["git"]
published: false
---

## git remote

### リモートリポジトリを見る
```
git remote -v
```

### リモートリポジトリを追加する
```
git remote add <リモート名> <リポジトリURL>
```

### リモートリポジトリを削除する
```
git remote remove <リモート名>
```

### リモートリポジトリをリネームする
```
git remote remove <旧リモート名> <新リモート名>
```