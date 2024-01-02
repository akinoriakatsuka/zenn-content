---
title: "phpのautoloadを理解する"
emoji: "💡"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["php"]
published: true
---

# オートロードとは何か

phpのオートロードとは、未定義のクラスを呼び出した時に、クラスの定義を読み込む仕組みのことです。

オブジェクト指向プログラミングではクラスを定義するときにファイルを分割することが一般的です。例えば、`User`クラスを定義するときに、`User.php`というファイルを作成し、その中に`User`クラスを定義します。

このとき、他のファイルで`User`クラスを使いたい場合には、通常`User.php`を読み込む必要があります。phpでは、`require_once`などといった関数を使ってファイルを読み込むことができます。

しかし、読み込むクラスが多くなると、ファイルの先頭にたくさんの`require_once`を書く必要があり、コードが読みにくくなります。

そこで、phpでは、未定義のクラスを呼び出した時に、クラスの定義を読み込む用途で指定した処理をさせることができる仕組みが用意されています。これがオートロードです。

# オードロードの仕組み

## spl_autoload_register
オートロードの時の挙動は、`spl_autoload_register`関数を使って定義します。

spl_autoload_register関数は、引数にコールバック関数を取ります。ここで指定したコールバック関数が、未定義のクラスを呼び出した時に実行されます。

コールバック関数の引数には、呼び出されたクラス名（string/文字列型）が入ります。コールバック関数の中で、クラス名に対応するファイルを読み込む処理を書きます。

```php
spl_autoload_register(function ($class) { // $classには呼び出されたクラス名が入る
    // クラスを定義するファイルを読み込む処理
});
```

## コード例

コード例を用いて、autoloadの挙動を確認します。
ファイルを分けない場合、autoloadを使わない場合、autoloadを使う場合の3つの例を示します。

以下の例では全てのファイルを同じディレクトリに配置してください。

### ファイルを分けない場合

```php:index.php
<?php

class User
{
    public function __construct()
    {
        echo 'Userクラスのインスタンスが生成されました。' . PHP_EOL;
    }
}

$user = new User();

```

#### 実行結果

```terminal:</>terminal
$ php index.php
Userクラスのインスタンスが生成されました。
```

### autoloadを使わない場合

```php:index.php
<?php
require_once 'user.php';

$user = new User();

```

```php:User.php
<?php
class User
{
    public function __construct()
    {
        echo 'Userクラスのインスタンスが生成されました。' . PHP_EOL;
    }
}

```

#### 実行結果

```terminal:</>terminal
$ php index.php
Userクラスのインスタンスが生成されました。
```

### autoloadを使う場合

以下は、autoloadを使った場合の例です。autoload.phpというファイルで、autoloadの挙動を定義して、index.phpでautoload.phpを読み込んでいます。

```php:autoload.php
<?php
spl_autoload_register(function ($class) {
    echo '1. ' . $class . 'クラスを読み込みます。' . PHP_EOL;
    require_once $class . '.php';
    echo '2. ' . $class . 'クラスを読み込みました。' . PHP_EOL;
});

```

```php:User.php
<?php
class User
{
    public function __construct()
    {
        echo 'Userクラスのインスタンスが生成されました。' . PHP_EOL;
    }
}

```

```php:index.php
<?php
require_once 'autoload.php';
// require_once 'user.php';

$user = new User(); // 明示的にuser.phpを読み込む必要がなくなった

```
#### 実行結果

```terminal:</>terminal
$ php index.php
1. Userクラスを読み込みます。
2. Userクラスを読み込みました。
Userクラスのインスタンスが生成されました。
```

:::message
例では、クラスを読み込む以外の処理も書いていますが、実際には予期せぬ挙動につながるため、クラスを読み込むための処理以外を書くべきではありません。
:::

# オートロードの規約

オートロードを使う時のルールとしては、PHP-FIGが作成したPSR-4という規約がデファクトスタンダードとなっています。

https://www.php-fig.org/psr/psr-4/

## PSR-4

以下の記事でPSR-4の内容を翻訳しています。
https://zenn.dev/aki_artisan/articles/psr4-translation-ja

短く説明すると、PSR-4では、名前空間とディレクトリを対応させておき、それ以下のサブ名前空間をディレクトリで、クラス名をファイル名でそれぞれ対応させるという仕様です。

例えば、`App\SomeModule\SomeUnit`というクラスを`src/`から読み込ませたい場合、`App`という名前空間を`src`ディレクトリに対応させれば、`App\SomeModule\SomeUnit`は`src/SomeModule/SomeUnit.php`から読み込まれるようになります。

| 名前空間付きクラス名          | 名前空間接頭辞     | ベースディレクトリ       | ファイルパス                               |
| :---------------------------- |:-------------------|:-------------------------|:------------------------------------------ |
| \App\SomeModule\SomeUnit      | App                | ./src/                   | ./src/SomeModule/SomeUnit.php              |

# Composerを使って実際のプロジェクトでautoloadを使う方法

簡単にautoloadを使うための方法の一つはComposerを使うことです。

Composerは、パッケージの依存関係を管理するためのツールで、標準でautoloadの実装を持っています。Composerのインストール方法は他の記事を参照してください。

https://getcomposer.org/

以下では、カレントディレクトリでComposerを使えることを前提としています。（検証環境はComposer version 2.5.8を使っています）

ディレクトリ構成は以下のようになっているものとします。/srcディレクトリと/publicディレクトリがあり、publicディレクトリの中にindex.phpがあります。

```
.
├── public
│   └── index.php
└── src
```

## composer.jsonの作成

Composerを使うために、ディレクトリ直下にcomposer.jsonというファイルを作成します。

```json:composer.json
{}
```

```terminal:</>terminal
$ composer install
```

空のcomposer.jsonを作成した後、`composer install`コマンドを実行します。

すると、vendorディレクトリとcomposer.lockファイルが作成されます。autoload.phpはvendorディレクトリの中にあります。

```
.
├── composer.json
├── composer.lock
├── public
│   └── index.php
├── src
└── vendor
    ├── autoload.php
    └── composer
```

以下の例では、`App`という名前空間を`src`ディレクトリに対応させます。

## index.phpでautoload.phpを読み込む

index.phpでautoload.phpを読み込みます。

```php:index.php
<?php
require_once __DIR__ . '/../vendor/autoload.php';

$app = new App\MyApp();
$app->run();

```

## クラスを定義する

読み込むためのクラスを定義します。

```php:src/MyApp.php
<?php
namespace App;

class MyApp
{
    public function run()
    {
        echo 'Hello, world!' . PHP_EOL;
    }
}

```

## composer.jsonにautoloadの設定を記述する

composer.jsonにautoloadの設定を記述します。

```json:composer.json
{
    "autoload": {
        "psr-4": {
            "App\\": "src/"
        }
    }
}
```

## composer dump-autoloadを実行する

composer.jsonを変更した場合は、`composer dump-autoload`コマンドを実行する必要があります。

```terminal:</>terminal
$ composer dump-autoload
```

## 実行結果

実行してみると、正常にsrc/MyApp.phpが読み込まれていることがわかります。（クラスのrunメソッドが実行されている）

```terminal:</>terminal
$ php public/index.php
Hello, world!
```

このようにして、PSR-4の規約に従ってクラスを読み込むことができました。

## Composerのautoloadの仕様

### PSR-4で複数のディレクトリに対応させる場合

```json:composer.json
{
    "autoload": {
        "psr-4": {
            "App\\": ["src/", "app/"]
        }
    }
}
```

上記のように、複数のディレクトリに対応づけることができます。
そうした場合、左側にあるディレクトリから順に探索されます。そのため、両方のディレクトリに呼び出すクラスのファイルがある場合は、左側のディレクトリのファイルが読み込まれます。

# まとめ

- オートロードとは、未定義のクラスを呼び出した時に、ファイルからクラスの定義を読み込む仕組みのことです。
- オートロードのための規約として、PSR-4がデファクトスタンダードとなっています。
- Composerを用いてPSR-4にしたがったautoloadを使うことができます。

# 参考文献

https://www.php.net/manual/ja/language.oop5.autoload.php
https://www.php-fig.org/psr/psr-4/
https://getcomposer.org/doc/04-schema.md#autoload
