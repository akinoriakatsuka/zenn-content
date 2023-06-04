---
title: "select文でデータを検索する"
---

# データを検索する

データベースからデータを取り出すには、select文を使います。
select文では、以下のように書きます。

```sql
select カラム名1, カラム名2, ... from テーブル名;
```

## 準備

実際にuserテーブルにデータを挿入して確認してみます。insert文については後で扱うので、今回はとりあえずこちらを実行してください。

```sql
insert into users (id, name) values (1, 'Taro');
```

成功すれば、以下のように表示されます。
```
INSERT 0 1
```

## select文

データが挿入されているか確認してみます。
確認するには、select文を使います。

```sql
select id, name from users;
```

うまくいっていれば、以下のように表示されます。
```
 id | name
----+------
  1 | Taro
(1 row)
```

特定のカラムのみを取り出したい場合は、カラム名を指定します。

```sql
select name from users;
```

また、すべてのカラムを取り出す場合は、`*`を指定します。

```sql
select * from users;
```

`*`はすべてのカラムという意味で、今回の場合は`select id, name from users;`と同じ意味になります。