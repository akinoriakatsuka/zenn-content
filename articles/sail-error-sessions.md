---
title: "sail upしたときにsessionsテーブルがないというエラーが出たときの対処法"
emoji: "🕌"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["laravel", "docker", "sail"]
published: true
---

# バージョン

```
$ sail artisan --version
Laravel Framework 11.1.1
```

# エラー内容

`SQLSTATE[42P01]: Undefined table: 7 ERROR: relation "sessions" does not exist LINE 1: select * from "sessions" where "id" = $1 limit 1 ^`

# 原因

`SESSION_DRIVER` が `database` になっているが、`sessions` テーブルがないため。

# 対処法

以下の方法のいずれかを実施する。http://localhost:80 にアクセスして、laravelの画面が表示されることを確認する。

## その1

`.env`の`SESSION_DRIVER`を`file`に変更する。

## その2

以下のコマンドを実行する。

```
$ sail artisan migrate
```

マイグレーションが実行されて、`sessions` テーブルが作成される。