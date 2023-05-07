---
title: "insert文でデータを追加する"
---

# データを追加する

データを追加するにはinsert文を使います。

```sql
insert into テーブル名 (カラム名1, カラム名2, ...) values (値1, 値2, ...);
```

## usersテーブルにデータを追加する

usersテーブルにデータを追加してみます。
```sql
insert into users (id, name) values (2, 'Jiro');
```

テーブルに保存されている一行のデータのことをレコードと呼びます。例えば、usersテーブルの一つのレコードで一人のユーザーを表すといった使われ方をします。
本書ではこれ以降、一行のデータを表す時にはレコードという用語を使います。

複数のレコードを一度に追加することもできます。
```sql
insert into users (id, name) values (3, 'Saburo'), (4, 'Shiro');
```

データが追加されたか確認してみます。
```sql
select * from users;
```

うまくいっていれば、以下のように表示されます。
```
 id | name
----+-------
  1 | Taro
  2 | Jiro
  3 | Saburo
  4 | Shiro
(4 rows)
```

データが挿入できることを確認したところで、今回はここまでにします。