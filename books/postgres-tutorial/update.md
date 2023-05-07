---
title: "update文でデータを更新する"
---

# update文でデータを更新する

データベースのデータを更新するにはupdate文を使います。

update文では以下のように記述します。

```sql
update テーブル名 set カラム名 = 値 where 条件;
```

## データを更新する

```sql
update users set name = 'Ichiro' where id = '1';
```

select文で確認してみます。

```sql
select * from users;
```

idが1のレコードだけが更新されていることが確認できます。

```
 id |  name  
----+--------
  2 | Jiro
  3 | Saburo
  4 | Shiro
  1 | Ichiro
(4 rows)
```

データの更新の方法がわかったところで、今回はここまでにします。