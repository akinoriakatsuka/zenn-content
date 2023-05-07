---
title: "テーブルの作成"
---

# テーブルの作成

今回は、データの入れ物であるテーブルを作成してみます。

## データベースに入る

前回、作成したデータベースに入ります。

```bash
psql postgres-tutorial
```

## テーブルの作成

今回は、ユーザーを管理するテーブルを作成します。

```bash
CREATE TABLE users (id INT, name VARCHAR(255));
```
CREATE TABLEと表示されれば、テーブルが作成されています。

## テーブルの一覧を確認する

データベース内のテーブルの一覧を確認するには、`\dt`コマンドを使います。

```bash
\dt
```

表示例
```
         List of relations
 Schema | Name  | Type  |  Owner   
--------+-------+-------+----------
 public | users | table | postgres
(1 row)
```

うまくいっていればusersというテーブルが表示されます。Ownerは環境によって異なるので、表示が異なっていても問題ありません。Homebrewでインストールしている場合、マシンのログイン名になります。

## テーブルの内容を確認する
テーブルの内容を確認するには、`\d`コマンドを使います。コマンドの後にテーブル名を指定します。

```bash
\d users
```

表示例
```
                       Table "public.users"
 Column |          Type          | Collation | Nullable | Default 
--------+------------------------+-----------+----------+---------
 id     | integer                |           |          | 
 name   | character varying(255) |           |          |         
```

テーブルが作成できたところで、今回はここまでにします。
