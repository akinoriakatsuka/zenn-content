---
title: "sailで作ったpostgresのデータベースに接続する"
emoji: "✨"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["laravel", "docker", "postgres", "sail"]
published: true
---

# sailで作ったpostgresのデータベースに接続する

## sailでのlaravelのインストール

終わっている方は飛ばしてください。

```
curl -s "https://laravel.build/example-app?with=pgsql" | bash
```

最後にパスワードを聞かれるので入力する

```
sail='[ -f sail ] && bash sail || bash vendor/bin/sail'
sail up -d
```

これでlaravelのプロジェクトが立ち上がる。localhost:80にアクセスするとlaravelの画面が表示されることを確認。

sessionsテーブルがないというエラーが出る場合は、`.env`の`SESSION_DRIVER`を`file`に変更するか、以下のコマンドを実行する。

```
sail artisan migrate
```

`.env`ファイルのDBに関わる初期値は以下の通り。

```
DB_CONNECTION=pgsql
DB_HOST=pgsql
DB_PORT=5432
DB_DATABASE=laravel
DB_USERNAME=sail
DB_PASSWORD=password
```

## postgresのデータベースに接続する

### phpのコンテナから接続する

```
$ docker ps
```

```
CONTAINER ID   IMAGE          COMMAND                  CREATED       STATUS                 PORTS                                                  NAMES
a093c9bac631   sail-8.3/app   "start-container"        2 hours ago   Up 2 hours             0.0.0.0:80->80/tcp, 0.0.0.0:5173->5173/tcp, 8000/tcp   example-app-laravel.test-1
a24686a8d565   postgres:15    "docker-entrypoint.s…"   2 hours ago   Up 2 hours (healthy)   0.0.0.0:5432->5432/tcp                                 example-app-pgsql-1
```


```
$ docker container exec -it a093c9bac631 bash
```

```
root@a093c9bac631:/var/www/html# psql -U sail -h pgsql laravel
Password for user sail:
```

パスワードは.envファイルの通り、`password`を入力する。

ポイントは、`-h pgsql`の部分で、dockerで立ち上げたdbコンテナは同じくdockerで立ち上げたappコンテナから見ると、`pgsql`というホスト名でアクセスできる。

### postgresのコンテナに入って接続する

```
$ docker ps
```

```
CONTAINER ID   IMAGE          COMMAND                  CREATED       STATUS                 PORTS                                                  NAMES
a093c9bac631   sail-8.3/app   "start-container"        2 hours ago   Up 2 hours             0.0.0.0:80->80/tcp, 0.0.0.0:5173->5173/tcp, 8000/tcp   example-app-laravel.test-1
a24686a8d565   postgres:15    "docker-entrypoint.s…"   2 hours ago   Up 2 hours (healthy)   0.0.0.0:5432->5432/tcp                                 example-app-pgsql-1
```

```
$ docker container exec -it a24686a8d565 bash
```

コンテナ内で以下を実行すると、データベースに接続できる。

```
root@a24686a8d565:/# psql -U sail laravel
```

### データベースの中身を見る

```
                                             List of databases
   Name    | Owner | Encoding |  Collate   |   Ctype    | ICU Locale | Locale Provider | Access privileges 
-----------+-------+----------+------------+------------+------------+-----------------+-------------------
 laravel   | sail  | UTF8     | en_US.utf8 | en_US.utf8 |            | libc            | 
 postgres  | sail  | UTF8     | en_US.utf8 | en_US.utf8 |            | libc            | 
 template0 | sail  | UTF8     | en_US.utf8 | en_US.utf8 |            | libc            | =c/sail          +
           |       |          |            |            |            |                 | sail=CTc/sail
 template1 | sail  | UTF8     | en_US.utf8 | en_US.utf8 |            | libc            | =c/sail          +
           |       |          |            |            |            |                 | sail=CTc/sail
 testing   | sail  | UTF8     | en_US.utf8 | en_US.utf8 |            | libc            | 
(5 rows)
```

あとは、select文などを実行してデータベースの中身を見ることができる。