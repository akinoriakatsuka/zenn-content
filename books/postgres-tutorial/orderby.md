---
title: "レコードの並び順を指定する"
---

# レコードの並び順を指定する

select文で取り出したデータの並び順を指定するには、`order by`句を使います。

## 準備

今後の説明のために、userテーブルにscoreというカラムを追加します。今回は一度テーブルを削除して再度作り直します。

```sql
drop table users; -- DROP TABLE
create table users (id int, name varchar(255), age int, score real);
insert 
  into users (id, name, age, score) 
  values 
    (1, 'Taro', 24, 80.0),
    (2, 'Jiro', 22, 60.0),
    (3, 'Saburo', 22, 70.5),
    (4, 'shiro', 21, 90.2);
```

## order by で並び順を指定する

```sql
select * from users order by id;
```

以下のように出力されます。

```
 id |  name  | age | score 
----+--------+-----+-------
  1 | Taro   |  24 |    80
  2 | Jiro   |  22 |    60
  3 | Saburo |  22 |  70.5
  4 | shiro  |  21 |  90.2
(4 rows)
```

また、scoreが大きい順に並べる時には以下のようにします。
```sql
select * from users order by score desc;
```

```
 id |  name  | age | score 
----+--------+-----+-------
  4 | shiro  |  21 |  90.2
  1 | Taro   |  24 |    80
  3 | Saburo |  22 |  70.5
  2 | Jiro   |  22 |    60
(4 rows)
```

### 複数の条件で並べ替える

ageで並べ替えた後に、scoreで並べ替えたい時は順番にコンマ区切りで条件を書き並べます。

```sql
select * from users order by age, score desc;
```

order byを指定しない場合、select文で取り出されるレコードの並び順に決まったルールはありません。実際、update文を扱った時にidが1のレコードが一番最後に表示されていました。
特定の並び順でデータを取得したい場合は必ずorder byで並び順を指定する必要があります。