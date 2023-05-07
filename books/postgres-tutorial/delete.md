---
title: "delete文でデータを削除する"
---

# delete文でデータを削除する

データベースからデータを削除するには、delete文を使います。

delete文では、以下のように書きます。

```sql
delete from テーブル名 where 条件;
```

このようにすることで、条件に合致するレコードが削除されます。

## データを削除する

今回は、usersテーブルからデータを削除してみます。

```sql
delete from users where id = '1';
```

以下のように表示されれば成功しています。
```
DELETE 1
```

削除されたか確認してみます。

```sql
select * from users;
```

idが1のレコードが削除されていれば成功です。
```
 id |  name  
----+--------
  2 | Jiro
  3 | Saburo
  4 | Shiro
(3 rows)
```

where句を省略するとすべてのレコードが削除削除されます。

```sql
delete from users;
```

select文で確認すると、テーブルが空になっていることが確認できます。

```
 id | name 
----+------
(0 rows)
```

削除したデータを再度insertしてデータを戻しておきましょう。

```sql
insert into users (id, name) values (1, 'Taro'), (2, 'Jiro'),(3, 'Saburo'), (4, 'Shiro');
```


