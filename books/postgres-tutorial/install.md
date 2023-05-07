---
title: "インストール"
---

# インストール

今回はHomebrewを使ってMacにPostgreSQLをインストールします。

## Homebrewのインストール
インストールしていない場合は、インストールしてください。

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

https://brew.sh/index_ja

## PostgreSQLのインストール

```bash
brew install postgresql
```

## PostgreSQLがインストールされたか確認
PostgreSQLの本体とコマンドがインストールされます。
  
```bash
postgres --version # postgres (PostgreSQL) 14.7 (Homebrew)
psql --version # psql (PostgreSQL) 14.7 (Homebrew)
```

## PostgreSQLが起動しているか確認

```bash
pg_isready # /tmp:5432 - accepting connections
```

起動していない場合は以下のようにして起動します。

```bash
brew services start postgresql
```

## PostgreSQLに接続

```bash
psql postgres
```

## PostgreSQLから抜ける

```bash
postgres=# \q
```

インストールができたところで、今回はここまでにします。