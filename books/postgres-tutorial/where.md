---
title: "where句で条件を指定する"
---

# 条件を指定する

前回、insert文でデータを追加したところから続けます。

where句は条件を指定して以下のように使います。
  
```sql
where 条件;
```

今回は条件を指定してデータを取り出してみます。

## 文字列のカラムを条件に指定する

```sql
select * from users where name = 'Taro';
```
このようにするとTaroが取り出されます。

ワイルドカードを使って指定することもできます。

名前が`iro`で終わるデータを取り出してみます。
  
```sql
select * from users where name like '%iro';
```

`%`は任意の文字列を表します。`%`の前に文字列を指定すると、その文字列で始まるデータを取り出します。
そのため、この場合はJiroとShiroが取り出されます。

また、`_`は任意の一文字を表します。
例えば以下のようにすると、Jiroのみが取り出されます。
```sql
select * from users where name like '_iro';
```


## 数値のカラムを条件に指定する

数字の場合は、不等号などを使って条件を指定します。

```sql
select * from users where id > 2;
```

sqlの条件を表す演算子の一覧は以下の通りです。
| 演算子 | 意味 |
|:---:|:---|
| = | 等しい |
| <> | 等しくない |
| != | 等しくない |
| < | より小さい |
| <= | 以下 |
| > | より大きい |
| >= | 以上 |
| between A and B | AとBの間（AとBを含む） |

例えば、
```sql
select * from users where id between 2 and 3;
```
とすると、JiroとSaburoが取り出されます。

## 複数の条件を指定する
条件はandやorを使って複数指定することができます。

Andはどちらも満たしているものに限定します。
```sql
select * from users where id > 2 and name like '%iro';
```

このようにすると、Shiroのみが取り出されます。


一方、orはどれか一つでも満たしていれば取り出します。
```sql
select * from users where id <= 2 or name like '%iro';
```

このようにすると、TaroとJiroとShiroが取り出されます。

## 集合で条件を指定する

inを使うと、指定した値のいずれかに一致するものを取り出します。

```sql
select * from users where id in (1, 3);
```

このようにすると、TaroとSaburoが取り出されます。

いろいろな条件を指定できることがわかったところで、今回はここまでにします。