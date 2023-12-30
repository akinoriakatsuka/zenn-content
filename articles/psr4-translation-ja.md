---
title: "PSR-4 オートローダー（日本語訳）"
emoji: "🐘"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["php"]
published: true
---

# オートローダー<!-- Autoloader -->

この文書中のMUST、MUST NOT、REQUIRED、SHALL、SHALL NOT、SHOULD、SHOULD NOT、RECOMMENDED、MAY、OPTIONAL というキーワードは、[RFC 2119](http://tools.ietf.org/html/rfc2119) で定義されているものと同じ意味で解釈されます。<!-- The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC 2119](http://tools.ietf.org/html/rfc2119). -->

## 1. 概要<!-- 1. Overview -->

このPSRは、ファイルパスからクラスを[オートロード](https://www.php.net/manual/ja/language.oop5.autoload.php)するための仕様を記述しています。[PSR-0](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md)を含む、他のオートロード仕様と完全に相互運用可能で、それらに追加して使用することができます。このPSRは、仕様に従ってオートロードされるファイルを配置する場所も記述しています。<!-- This PSR describes a specification for [autoloading][] classes from file paths. It is fully interoperable, and can be used in addition to any other autoloading specification, including [PSR-0][]. This PSR also describes where to place files that will be autoloaded according to the specification. -->


## 2. 仕様<!-- Specification -->


1. 「クラス」という用語は、クラス、インターフェース、トレイト、およびその他の類似の構造を指します。<!-- 1. The term "class" refers to classes, interfaces, traits, and other similar structures. -->

2. 完全修飾クラス名は以下の形式を持ちます。<!-- 2. A fully qualified class name has the following form: -->
    ```
    \<NamespaceName>(\<SubNamespaceNames>)*\<ClassName>
    ```

    1. 完全修飾クラス名は、トップレベルの名前空間名（ベンダー名前空間とも呼ばれる）を持たなければなりません。（MUST）<!-- 1. The fully qualified class name MUST have a top-level namespace name, also known as a "vendor namespace". -->
    2. 完全修飾クラス名は、1つ以上のサブ名前空間名を持つことができます。（MAY）<!-- 2. The fully qualified class name MAY have one or more sub-namespace names. -->
    3. 完全修飾クラス名は、終端クラス名を持たなければなりません。（MUST）<!-- 3. The fully qualified class name MUST have a terminating class name. -->
    4. 完全修飾クラス名のいかなる部分においても、アンダースコアは特別な意味を持ちません。<!-- 4. Underscores have no special meaning in any portion of the fully qualified class name. -->
    5. 完全修飾クラス名のアルファベット文字は、小文字と大文字の組み合わせであっても構いません。（MAY）<!-- 5. Alphabetic characters in the fully qualified class name MAY be any combination of lower case and upper case. -->
    6. 全てのクラス名は、大文字と小文字を区別して参照されなければなりません。（MUST）<!-- 6. All class names MUST be referenced in a case-sensitive fashion. -->

<!-- 3. When loading a file that corresponds to a fully qualified class name ... -->
1. 完全修飾クラス名に対応するファイルを読み込む場合 ...

    1. 完全修飾クラス名の中の一つまたはそれより多くの先頭の名前空間セパレータを含まない先行する名前空間とサブ名前空間の名前（「名前空間接頭辞」）は、少なくとも1つの「ベースディレクトリ」に対応します。<!-- 1. A contiguous series of one or more leading namespace and sub-namespace names, not including the leading namespace separator, in the fully qualified class name (a "namespace prefix") corresponds to at least one "base directory". -->

    2. 「名前空間接頭辞」の後の連続したサブ名前空間名は、「ベースディレクトリ」における名前空間セパレータがディレクトリセパレータを表すようなサブディレクトリに対応します。サブディレクトリ名は、サブ名前空間名の大文字小文字と一致しなければなりません。（MUST）<!-- 2. The contiguous sub-namespace names after the "namespace prefix" correspond to a subdirectory within a "base directory", in which the namespace separators represent directory separators. The subdirectory name MUST match the case of the sub-namespace names. -->

    3. 終端クラス名は、`.php`で終わるクラスファイル名の終端と対応します。ファイル名は、終端クラス名の大文字小文字と一致しなければなりません。（MUST）<!-- 3. The terminating class name corresponds to a file name ending in `.php`. The file name MUST match the case of the terminating class name. -->

2. オートローダーの実装は例外をスローしてはならず（MUST NOT）、いかなるレベルのエラーもレイズしてはならず（MUST NOT）、値を返すべきではありません（SHOULD NOT）。<!-- 4. Autoloader implementations MUST NOT throw exceptions, MUST NOT raise errors of any level, and SHOULD NOT return a value. -->

## 3. 例<!-- Examples -->

以下の表は、与えられた完全修飾クラス名、名前空間接頭辞、およびベースディレクトリに対応するファイルパスを示します。<!-- The table below shows the corresponding file path for a given fully qualified class name, namespace prefix, and base directory. -->

<!-- | Fully Qualified Class Name    | Namespace Prefix   | Base Directory           | Resulting File Path -->
| 完全修飾クラス名    | 名前空間接頭辞   | ベースディレクトリ           | ファイルパス
| :---------------------------- |:-------------------|:-------------------------|:------------------------------------------
| \Acme\Log\Writer\File_Writer  | Acme\Log\Writer    | ./acme-log-writer/lib/   | ./acme-log-writer/lib/File_Writer.php
| \Aura\Web\Response\Status     | Aura\Web           | /path/to/aura-web/src/   | /path/to/aura-web/src/Response/Status.php
| \Symfony\Core\Request         | Symfony\Core       | ./vendor/Symfony/Core/   | ./vendor/Symfony/Core/Request.php
| \Zend\Acl                     | Zend               | /usr/includes/Zend/      | /usr/includes/Zend/Acl.php

例えば、仕様に従うオートローダーの実装は、[例のファイル](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader-examples.md)を参照してください。実装例は仕様の一部とみなされてはならず（MUST NOT）、いつでも変更される可能性があります（MAY）。
<!-- For example implementations of autoloaders conforming to the specification, please see the [examples file][]. Example implementations MUST NOT be regarded as part of the specification and MAY change at any time. -->
