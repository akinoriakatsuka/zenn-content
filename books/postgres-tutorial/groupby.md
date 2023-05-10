---
title: "グループ化と集計"
---

# グループ化と集計

SQLでは合計や平均値などの集計値を返す関数が用意されています。集計地を取り出すにはselect文を使います。

## 集計値を取り出す

合計を取り出すには、sum関数を使います。

```sql
select sum(score) from users;
```

うまくいくと以下のように出力されます。

```
  sum  
-------
 300.7
(1 row)
```

複数の集計値を取り出すこともできます。

```sql
select sum(score), avg(score), count(*) from users;
```

```
  sum  |        avg        | count 
-------+-------------------+-------
 300.7 | 75.17499923706055 |     4
(1 row)
```

## グループ化

集計を行うためのグループ化を行うには、group by句を使います。

例えば、年齢ごとにscoreの平均値を取り出すには、以下のようにします。

```sql
select age, avg(score) from users group by age order by age;
```

```
 age |        avg        
-----+-------------------
  21 | 90.19999694824219
  22 |             65.25
  24 |                80
(3 rows)
```


## having句

集計結果に対して条件を指定するには、having句を使います。

2人以上いる年齢に対してscoreの平均値を取り出すには、以下のようにします。

```sql
select age, avg(score) from users group by age having count(age) >= 2;
```

```
 age |  avg  
-----+-------
  22 | 65.25
(1 row)
```

havingの代わりにwhere句を使うことはできません。where句は集計前のレコードに対して条件を指定することができます。

```sql
select age, avg(score) from users where id <> 3 group by age order by age;
```

こうすることで、idが3でないレコードのみを集計の対象とすることができます。

```
 age |        avg        
-----+-------------------
  21 | 90.19999694824219
  22 |                60
  24 |                80
(3 rows)
```

ageが22であるレコードはJiroとSaburoのものでしたが、Saburoのidは3であったので、集計の対象から外れ、結果としてJiroの値のみが平均の計算に使われています。

## 注意点 - 集計値と集計値でない値を同時にselectすることはできない
集計値と集計値でない値を同時にselectすることはできません。集計に使っていないカラムをselectするとエラーになります。

```sql
select sum(score), name from users;
```

```
ERROR:  column "users.name" must appear in the GROUP BY clause or be used in an aggregate function
LINE 1: select sum(score), name from users;
                           ^
```

これは、集計値を取り出す場合、何らかのグループ化を行う必要があるためです。`select sum(score) from users;`のように`order by`句がない場合は、すべてのレコードが1つのグループとして扱われます。

例外として、集計の対象となったカラムは取り出すことができます。これは上の例でも確認してきた通りです。

```sql
select age, avg(score) from users group by age order by age;
```

```sql
-- 出力は省略
```