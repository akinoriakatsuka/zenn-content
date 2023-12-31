---
title: "PSR-0 オートローディング標準（日本語訳）"
emoji: "🐘"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["php"]
published: true
---

オートローディング標準<!-- Autoloading Standard -->
====================

<!-- > **Deprecated** - As of 2014-10-21 PSR-0 has been marked as deprecated. [PSR-4] is now recommended as an alternative. -->
> **非推奨** - 2014-10-21にPSR-0は非推奨となりました。[PSR-4]が代替として推奨されています。

[PSR-4]: https://www.php-fig.org/psr/psr-4/

以下は、オートローダーの相互運用性を確保するために必須となる要件を記述しています。<!-- The following describes the mandatory requirements that must be adhered to for autoloader interoperability. -->

必須要件<!-- Mandatory -->
---------

* 完全修飾名前空間とクラスは、次の構造を持たなければなりません。`\<Vendor Name>\(<Namespace>\)*<Class Name>`<!-- * A fully-qualified namespace and class must have the following structure `\<Vendor Name>\(<Namespace>\)*<Class Name>` -->
* 各名前空間は、トップレベル名前空間（ベンダー名前空間とも呼ばれる）を持たなければなりません。<!-- * Each namespace must have a top-level namespace ("Vendor Name"). -->
* 各名前空間は、サブ名前空間を求める数だけ持つことができます。<!-- * Each namespace can have as many sub-namespaces as it wishes. -->
* 各名前空間の区切り文字は、ファイルシステムからロードしたときに、`DIRECTORY_SEPARATOR`に変換されます。<!-- * Each namespace separator is converted to a `DIRECTORY_SEPARATOR` when loading from the file system. -->
* クラス名の中の各`_`文字は、`DIRECTORY_SEPARATOR`に変換されます。`_`文字は名前空間において特別な意味を持ちません。<!-- * Each `_` character in the CLASS NAME is converted to a `DIRECTORY_SEPARATOR`. The `_` character has no special meaning in the namespace. -->
* 完全修飾名前空間とクラスは、ファイルシステムからロードするときに、`.php`で終えられます。<!-- * The fully-qualified namespace and class are suffixed with `.php` when loading from the file system. -->
* ベンダ名、名前空間、クラス名の中のアルファベットの文字は、大文字と小文字の組み合わせであっても構いません。<!-- * Alphabetic characters in vendor names, namespaces, and class names may be of any combination of lower case and upper case. -->

例<!-- Examples -->
--------

* `\Doctrine\Common\IsolatedClassLoader` => `/path/to/project/lib/vendor/Doctrine/Common/IsolatedClassLoader.php`
* `\Symfony\Core\Request` => `/path/to/project/lib/vendor/Symfony/Core/Request.php`
* `\Zend\Acl` => `/path/to/project/lib/vendor/Zend/Acl.php`
* `\Zend\Mail\Message` => `/path/to/project/lib/vendor/Zend/Mail/Message.php`

名前空間名とクラス名の中のアンダースコア<!-- Underscores in Namespaces and Class Names -->
-----------------------------------------

* `\namespace\package\Class_Name` => `/path/to/project/lib/vendor/namespace/package/Class/Name.php`
* `\namespace\package_name\Class_Name` => `/path/to/project/lib/vendor/namespace/package_name/Class/Name.php`

我々がここに設定する標準は、痛みのないオートローダーの相互運用性のための最低限の共通の基準であるべきです。これらの標準に従っていることをテストすることができるように、このサンプルのSplClassLoader実装を利用することができます。この実装はPHP 5.3のクラスをロードすることができます。<!-- The standards we set here should be the lowest common denominator for painless autoloader interoperability. You can test that you are following these standards by utilizing this sample SplClassLoader implementation which is able to load PHP 5.3 classes. -->

実装例<!-- Example Implementation -->
----------------------

以下は、上記で提案されている標準がどのようにオートロードされるかを単純に示すための関数の例です。<!-- Below is an example function to simply demonstrate how the above proposed standards are autoloaded. -->

```php
<?php

function autoload($className)
{
    $className = ltrim($className, '\\');
    $fileName  = '';
    $namespace = '';
    if ($lastNsPos = strrpos($className, '\\')) {
        $namespace = substr($className, 0, $lastNsPos);
        $className = substr($className, $lastNsPos + 1);
        $fileName  = str_replace('\\', DIRECTORY_SEPARATOR, $namespace) . DIRECTORY_SEPARATOR;
    }
    $fileName .= str_replace('_', DIRECTORY_SEPARATOR, $className) . '.php';

    require $fileName;
}
spl_autoload_register('autoload');
```

SplClassLoader実装<!-- SplClassLoader Implementation -->
-----------------------------

以下のgistは、オートローダーの相互運用の標準に従う場合に、クラスをロードできるSplClassLoaderの実装のサンプルです。これは、現在の推奨されるPHP 5.3クラスのロード方法です。<!-- The following gist is a sample SplClassLoader implementation that can load your classes if you follow the autoloader interoperability standards proposed above. It is the current recommended way to load PHP 5.3 classes that follow these standards. -->

* [http://gist.github.com/221634](http://gist.github.com/221634)
