---
title: "Google Chromeで歌詞サイトのソースを表示する"
emoji: "📜"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["chrome","chromium"]
published: true
---

# 概要
chromeなどのブラウザでは、右クリックでコンテキストメニューを開いてページのソースを表示することができます。しかし、歌詞などのサイトではコピペを防止するためか、画面のクリックが無効になっています。そういう場合でもソースを表示する方法を紹介します。

※悪用しないようにお願いします。

# 手順
アドレスバーのurlの前に`view-source:`を追加する。

[歌詞サイト](https://www.uta-net.com/song/326156/)
ソース `view-source:https://www.uta-net.com/song/326156/`

## 補足
同じように、Safariでアドレスバーに入力したのですが、無効なurlですと表示されてしまいました。chrome以外では未検証ですがchromiumで同じようにできたので、chromium製のブラウザなら同じようにできるかと思われます。