---
title: "Dockerfileからコンテナを作成する"
emoji: "🐳"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: []
published: true
---

# 概要
Dockerfileからコンテナを作成する方法を説明します。
Dockerfileからイメージを作り、イメージからコンテナを作成します。

## Dockerfileを作成

Dockerfileを作成します。

```Dockerfile
FROM rockylinux:8

RUN dnf update -y
```

## イメージを作成

```bash
docker image build -t myrockylinux:v1 .  
```

-tオプションでイメージ名を指定します。

その後ろの引数でDockerfileのパスを指定します。今回はカレントディレクトリにDockerfileを配置して、`.`を指定しています。

docker imagesコマンドでイメージが作成されていることを確認します。

```bash
docker images
```

このように表示されます

```
REPOSITORY                       TAG              IMAGE ID       CREATED          SIZE
myrockylinux                     v1               85d86d48fd48   46 minutes ago   228MB
```


## イメージからコンテナを起動

```bash
 docker run --rm --name myrockylinux -it myrockylinux:v1 /bin/bash
```

--rmオプションをつけると、コンテナを終了したときにコンテナが自動的に削除されます。

コンテナを起動すると、以下のようになります。

```bash
[root@f0e2e3e3f0e2 /]# 
```

別のターミナルを開いて、docker container ls コマンドでコンテナが起動していることを確認します。

```bash
docker container ls
```

このように表示されます。

```
CONTAINER ID   IMAGE            COMMAND       CREATED          STATUS          PORTS     NAMES
f0e2e3e3f0e2   myrockylinux:v1  "/bin/bash"   10 seconds ago   Up 9 seconds              myrockylinux
```

## コンテナを終了

```bash
exit
```

docker container ls コマンドでコンテナがなくなっていることを確認します。

```bash
docker container ls
```