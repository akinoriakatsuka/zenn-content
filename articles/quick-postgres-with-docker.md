---
title: "Dockerで手早くPostgresを試してみる"
emoji: "🐘"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["postgres", "docker"]
published: true
---

# dockerコンテナを立ち上げる

```
docker run --rm --name some-postgres -e POSTGRES_PASSWORD=mysecretpassword -it postgres
```

参考：https://hub.docker.com/_/postgres#:~:text=start%20a%20postgres%20instance

# postgresユーザーでコンテナを実行する

`docker container ps`でコンテナIDを確認する。

```
CONTAINER ID   IMAGE             COMMAND                  CREATED        STATUS       PORTS                  NAMES
064a5688bd28   postgres          "docker-entrypoint.s…"   2 hours ago    Up 2 hours   5432/tcp               some-postgres
```

以下では、CONTAINER IDが`064a5688bd28`であるとします。ここの結果で適宜読み替えてください。

`-u`でユーザーを指定しないと、psqlコマンドが実行できないので、`-u postgres`をつける。

```
docker container exec -u postgres -it 064a5688bd28 psql
```

あるいは、rootユーザーでコンテナに入ってから、`su - postgres`でpostgresユーザーに切り替える。

```
docker container exec -it 064a5688bd28 psql
```

コンテナ内で
```
su - postgres
```



