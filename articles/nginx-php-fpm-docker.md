---
title: "Dockerでnginx+php-fpmをとりあえず動かしてみるハンズオン"
emoji: "🖐️"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["php", "nginx", "docker"]
published: true
---

## 検証環境

```
Docker version 20.10.13, build a224086
MacOS Sonoma
```

## ゴール

- nginxとphp-fpmを使って、`phpinfo()` を表示する。

## ディレクトリ構成

```
.
├── docker
│   ├── nginx
│   │   └── default.conf
│   └── php
│       └── Dockerfile
├── docker-compose.yml
└── src
    └── index.php
```

## docker-compose.yml

docker-compose.ymlに以下の内容を記載します。

```yml
version: '3.9'

services:
  nginx:
    image: nginx:latest
    container_name: nginx
    ports:
      - "8080:80"
    volumes:
      - ./docker/nginx/default.conf:/etc/nginx/conf.d/default.conf
    depends_on:
      - php
  php:
    build:
      context: ./docker/php
    container_name: php-fpm
    volumes:
      - ./src:/var/www/html
```

### 設定内容

servicesに2つのコンテナの設定を書いていきます。

#### nginx
nginxは `nginx:latest` のイメージをそのまま使います。

`ports` の設定で、ホストマシンのポート 8080 に、コンテナ内のポート 80 をマッピングします。

`volume` の設定で、ホストマシンの `docker/nginx/default.conf` をコンテナ内の `/etc/nginx/conf.d/default.conf` にマウントします。

`depends_on` の設定で、phpコンテナが起動してからnginxコンテナを起動するようにします。

#### php
phpは `./docker/php/Dockerfile` を使ってイメージをビルドします。

`volume` の設定で、ホストマシンの `src` ディレクトリをコンテナ内の `/var/www/html` にマウントします。

## docker/php/Dockerfile

```Dockerfile
FROM php:8.4-fpm
```

拡張モジュールを追加する場合は、以下のように記述します。（ここを変えた場合は、イメージをビルドし直してください。）

```Dockerfile
FROM php:8.4-fpm

RUN docker-php-ext-install pdo_mysql
```

## docker/nginx/default.conf

```
server {
    listen 80;
    server_name localhost;

    root /var/www/html;

    index index.php index.html;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        include fastcgi_params;
        fastcgi_pass php-fpm:9000;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    }
}
```

nginxの設定ファイルです。

`server` ブロックで、リクエストを受け付けるポートやドキュメントルートを設定します。

`location /` の設定で、リクエストが来たらindex.phpを返すようにします。

`location ~ \.php$` の設定で、phpファイルへのリクエストを受け付けます。

## src/index.php

```php
<?php
phpinfo();

```

## 操作

docker-compose.ymlがあるディレクトリで、以下のコマンドを実行
（ホストマシンの8080が埋まっていないか確認してください）

```
docker compose up -d
```

イメージをビルドし直す時は

```
docker compose up -d --build
```

## 動作確認

http://localhost:8080/
にアクセスする

![](/images/phpinfo.png)

## サンプルリポジトリ
ここまでの内容をまとめたリポジトリを作成しました。

https://github.com/akinoriakatsuka/nginx-php-fpm-sample

