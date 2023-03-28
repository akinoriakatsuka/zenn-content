---
title: "PhpStormを使い始めるためにやったこと（Mac）"
emoji: "🌪️"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["php","PhpStorm","JetBrains"]
published: true
---

これまでVSCodeしか使っていなかったのですが、PHPerKaigi2023で色々な方がおすすめしていたので、入門することにしました。
「これも設定しておくと良いよ！」というものがありましたらコメントでぜひ教えてください。

# PhpStormのインストール

公式サイトからダウンロード
https://www.jetbrains.com/ja-jp/phpstorm/

少し手が出しづらいお値段ですが、無料お試し期間があります。
![](/images/phpstorm-setup/price.png)

# インタプリタの設定

そのままだとPHPを実行するためのインタプリタがないので、インストールしたバイナリファイルのパスを指定する。

今回はHomebrewでインストールしてみます。

```
$ brew install php
```

2023/3/28現在、PHP 8.2.4がインストールされる。

```
$ php --version
PHP 8.2.4 (cli) (built: Mar 16 2023 16:46:52) (NTS)
Copyright (c) The PHP Group
Zend Engine v4.2.4, Copyright (c) Zend Technologies
    with Zend OPcache v8.2.4, Copyright (c), by Zend Technologies
$ which php
/usr/local/bin/php
$ readlink /usr/local/bin/php
../Cellar/php/8.2.4/bin/php
```

`which php`と`readlink /usr/local/bin/php`はインストールされている場所の確認です。場所がうまく見つからない場合は試してみてください。

![](/images/phpstorm-setup/setting.png)

/usr/local/Cellar/というディレクトリにbrewで入れたphpが置かれているので、これを選択して設定。

![](/images/phpstorm-setup/cli_interpreters.png)


# ターミナルから開けるようにする
VSCode では `code .`としてカレントディレクトリでVSCodeをひらけていました。

Macの場合は、以下のコマンドを実行すると、パスが通ったディレクトリにPhpStormを開くスクリプトを作成できます。chmodでパーミッションを設定して、実行可能にしておきます。

```
echo '#!/bin/sh

open -na "PhpStorm.app" --args "$@"' >> /usr/local/bin/pstorm && chmod 755 /usr/local/bin/pstorm
```

うまくいけばこちらで開けるようになっているはずです。
```
$ pstorm .
```

Mac以外の方は以下のurlを参考にして適宜読み替えてください。
https://pleiades.io/help/phpstorm/working-with-the-ide-features-from-command-line.html#standalone