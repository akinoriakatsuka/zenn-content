---
title: "insert文でデータを追加する"
---

# データを追加する

データを追加するにはinsert文を使います。

usersテーブルにデータを追加してみます。
```sql
insert into users (id, name) values (2, 'Jiro');
```

複数のデータを一度に追加することもできます。
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

データが挿入できることを確認したところで今回はここまでにします。