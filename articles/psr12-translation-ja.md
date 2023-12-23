---
title: "PSR-12 拡張コーディングスタイル（日本語訳）"
emoji: "🐘"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["php"]
published: true
---

# PSR-12 拡張コーディングスタイル
<!-- The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in RFC 2119. -->
"MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY"および"OPTIONAL"というキーワードは、このドキュメントでは、RFC 2119で説明されているように解釈されます。

<!-- ## Overview -->
## 概要

<!-- This specification extends, expands and replaces PSR-2, the coding style guide and requires adherence to PSR-1, the basic coding standard. -->
この仕様は、PSR-2（コーディングスタイルガイド）を延長、拡張および置き換え、PSR-1（基本的なコーディングスタンダード）への遵守を必要とします。

<!-- Like PSR-2, the intent of this specification is to reduce cognitive friction when scanning code from different authors. It does so by enumerating a shared set of rules and expectations about how to format PHP code. This PSR seeks to provide a set way that coding style tools can implement, projects can declare adherence to and developers can easily relate to between different projects. When various authors collaborate across multiple projects, it helps to have one set of guidelines to be used among all those projects. Thus, the benefit of this guide is not in the rules themselves but the sharing of those rules. -->

PSR-2のように、この仕様の関心は、異なる作者のコードを読むときの認知摩擦を減らすことです。これは、PHPコードのフォーマット方法に関する共有されたルールと期待を列挙することによって行われます。このPSRは、コーディングスタイルツールが実装できる一連の方法、プロジェクトが遵守を宣言できる一連の方法、および開発者が異なるプロジェクト間で簡単に関連付けられる一連の方法を提供しようとします。さまざまな作者が複数のプロジェクトで協力するとき、それはそれら全てのプロジェクトの間で使われる一連のガイドラインを持つことを助けます。したがって、このガイドの利点は、ルール自体ではなく、それらのルールを共有することにあります。

<!-- PSR-2 was accepted in 2012 and since then a number of changes have been made to PHP which has implications for coding style guidelines. Whilst PSR-2 is very comprehensive of PHP functionality that existed at the time of writing, new functionality is very open to interpretation. This PSR, therefore, seeks to clarify the content of PSR-2 in a more modern context with new functionality available, and make the errata to PSR-2 binding. -->
PSR-2は2012年に承認され、その後、コーディングスタイルガイドに影響を与えるPHPの変更がいくつか行われています。一方PSR-2は、執筆時点で存在していたPHP機能に非常に包括的ですが、新しい機能は解釈の余地が非常に大きいです。したがって、このPSRは、PSR-2の内容を新しい機能が利用可能になったより現代的なコンテキストで明確にし、PSR-2の拘束に訂正を生じさせることを目的としています。

<!-- ### Previous language versions -->
### 以前の言語バージョン

<!-- Throughout this document, any instructions MAY be ignored if they do not exist in versions of PHP supported by your project. -->
このドキュメントでは、あなたのプロジェクトでサポートされているPHPのバージョンに存在しない場合、いかなる指示を無視してもかまいません。

<!-- ### Example -->
### 例
<!-- This example encompasses some of the rules below as a quick overview: -->
この例は、短い概要として以下のルールの一部を網羅しています。

```php
<?php

declare(strict_types=1);

namespace Vendor\Package;

use Vendor\Package\{ClassA as A, ClassB, ClassC as C};
use Vendor\Package\SomeNamespace\ClassD as D;

use function Vendor\Package\{functionA, functionB, functionC};

use const Vendor\Package\{ConstantA, ConstantB, ConstantC};

class Foo extends Bar implements FooInterface
{
    public function sampleFunction(int $a, int $b = null): array
    {
        if ($a === $b) {
            bar();
        } elseif ($a > $b) {
            $foo->bar($arg1);
        } else {
            BazClass::bar($arg2, $arg3);
        }
    }

    final public static function bar()
    {
        // method body
    }
}
```

<!-- ## 2. General -->
## 2. 一般
<!-- ### 2.1 Basic Coding Standard -->
## 2.1 基本的なコーディングスタンダード
<!-- Code MUST follow all rules outlined in PSR-1. -->
コードは、PSR-1で概説されているすべてのルールに従わねばなりません。

<!-- The term 'StudlyCaps' in PSR-1 MUST be interpreted as PascalCase where the first letter of each word is capitalized including the very first letter. -->
StudlyCapsという用語は、PSR-1では、各単語の最初の文字が大文字である、最初の文字を含むPascalCaseとして解釈されなければなりません。

<!-- ### 2.2 Files -->
### 2.2 ファイル
<!-- All PHP files MUST use the Unix LF (linefeed) line ending only. -->
すべてのPHPファイルは、Unix LF（ラインフィード）の行末を使用しなければなりません。

<!-- All PHP files MUST end with a non-blank line, terminated with a single LF. -->
全てのPHPファイルは、単一のLFで終了する、空行でない行で終了しなければなりません。

<!-- The closing ?> tag MUST be omitted from files containing only PHP. -->
PHPのみを含むファイルからは、`?>`タグを省略しなければなりません。

<!-- ### 2.3 Lines -->
### 2.3 行
<!-- There MUST NOT be a hard limit on line length. -->
行の長さには厳格な制限を設けてはなりません。

<!-- The soft limit on line length MUST be 120 characters. -->
行の長さの緩い制限は120文字でなければなりません。

<!-- Lines SHOULD NOT be longer than 80 characters; lines longer than that SHOULD be split into multiple subsequent lines of no more than 80 characters each. -->
行は80文字を超えないべきで、それ以上の行は80文字を超えない複数の行に分割されるべきです。

<!-- There MUST NOT be trailing whitespace at the end of lines. -->
行の末尾の空白はあってはなりません。

<!-- Blank lines MAY be added to improve readability and to indicate related blocks of code except where explicitly forbidden. -->
空白の行は、明示的に禁止されていない限り、可読性を向上させ、関連するコードブロックを示すために追加することができます。

<!-- There MUST NOT be more than one statement per line. -->
一行に一つより多くの文を含んではなりません。

<!-- ### 2.4 Indenting -->
### 2.4 インデント
<!-- Code MUST use an indent of 4 spaces for each indent level, and MUST NOT use tabs for indenting. -->
1つのインデントレベルにつき4つのスペースを使用しなければならず、インデントにタブを使用してはなりません。

<!-- ### 2.5 Keywords and Types -->
### 2.5 キーワードと型
<!-- All PHP reserved keywords and types [1][2] MUST be in lower case. -->
全てのPHPの予約されたキーワードと型は小文字でなければなりません。

<!-- Any new types and keywords added to future PHP versions MUST be in lower case. -->
将来のPHPバージョンに追加れる、あらゆる新しい型とキーワードは、ローワーケースでなければなりません。

<!-- Short form of type keywords MUST be used i.e. `bool` instead of `boolean`, `int` instead of `integer` etc. -->
型キーワードの短い形式を使用しなければなりません。例えば、`boolean`の代わりに`bool`、`integer`の代わりに`int`などを使用しなければなりません。

<!-- ## 3. Declare Statements, Namespace, and Import Statements -->
## 3. 宣言文、名前空間、およびインポート文
<!-- The header of a PHP file may consist of a number of different blocks. If present, each of the blocks below MUST be separated by a single blank line, and MUST NOT contain a blank line. Each block MUST be in the order listed below, although blocks that are not relevant may be omitted. -->
PHPファイルのヘッダーは、複数の異なるブロックで構成される場合があります。その場合、以下の各ブロックは、単一の空行で区切られなければならず、空行を含んではなりません。各ブロックは、以下にリストされている順序でなければなりませんが、関連しないブロックは省略することができます。

<!-- - Opening `<?php` tag.
- File-level docblock.
- One or more declare statements.
- The namespace declaration of the file.
- One or more class-based `use` import statements.
- One or more function-based `use` import statements.
- One or more constant-based `use` import statements.
- The remainder of the code in the file. -->
- `<?php`タグ
- ファイルレベルのdocblock
- 1つ以上のdeclare文
- ファイルの名前空間宣言
- 1つ以上のクラスベースの`use`インポート文
- 1つ以上の関数ベースの`use`インポート文
- 1つ以上の定数ベースの`use`インポート文
- ファイル内の残りのコード

<!-- When a file contains a mix of HTML and PHP, any of the above sections may still be used. If so, they MUST be present at the top of the file, even if the remainder of the code consists of a closing PHP tag and then a mixture of HTML and PHP. -->
ファイルがHTMLとPHPの混合を含む場合、上記のいずれのセクションをも使用することができます。その場合、たとえコードの残りがPHPの終了タグとHTMLとPHPの混合であっても、それらはファイルの先頭に存在しなければなりません。

<!-- When the opening `<?php` tag is on the first line of the file, it MUST be on its own line with no other statements unless it is a file containing markup outside of PHP opening and closing tags. -->
`<?php`タグがファイルの最初の行にある場合、それがPHPの開始と終了タグの外にマークアップを含むファイルでない限り、それは他の文がない行にある必要があります。

<!-- Import statements MUST never begin with a leading backslash as they must always be fully qualified. -->
インポート文は、常に完全修飾名である必要があるため、バックスラッシュで始まってはなりません。

<!-- The following example illustrates a complete list of all blocks: -->
下記の例は、すべてのブロックの完全なリストを示しています。

```php
<?php

/**
 * This file contains an example of coding styles.
 */

declare(strict_types=1);

namespace Vendor\Package;

use Vendor\Package\{ClassA as A, ClassB, ClassC as C};
use Vendor\Package\SomeNamespace\ClassD as D;
use Vendor\Package\AnotherNamespace\ClassE as E;

use function Vendor\Package\{functionA, functionB, functionC};
use function Another\Vendor\functionD;

use const Vendor\Package\{CONSTANT_A, CONSTANT_B, CONSTANT_C};
use const Another\Vendor\CONSTANT_D;

/**
 * FooBar is an example class.
 */
class FooBar
{
    // ... additional PHP code ...
}
```

<!-- Compound namespaces with a depth of more than two MUST NOT be used. Therefore the following is the maximum compounding depth allowed: -->
深さが2を超える合成名前空間は使用してはなりません。したがって、以下が許可される最大の合成深度です。

```php
<?php

use Vendor\Package\SomeNamespace\{
    SubnamespaceOne\ClassA,
    SubnamespaceOne\ClassB,
    SubnamespaceTwo\ClassY,
    ClassZ,
};
```

<!-- And the following would not be allowed: -->
そして、以下は許可されません。

```php

<?php

use Vendor\Package\SomeNamespace\{
    SubnamespaceOne\AnotherNamespace\ClassA,
    SubnamespaceOne\ClassB,
    ClassZ,
};
```

<!-- When wishing to declare strict types in files containing markup outside PHP opening and closing tags, the declaration MUST be on the first line of the file and include an opening PHP tag, the strict types declaration and closing tag. -->
PHPの開始タグと終了タグの外にマークアップを含むファイルでstrict typesを宣言したい場合、宣言はファイルの最初の行にあり、開始PHPタグ、strict types宣言、終了タグが含まれていなければなりません。

For example:

```php

<?php declare(strict_types=1) ?>
<html>
<body>
    <?php
        // ... additional PHP code ...
    ?>
</body>
</html>
```

<!-- Declare statements MUST contain no spaces and MUST be exactly `declare(strict_types=1)` (with an optional semi-colon terminator). -->
宣言文はスペースを含まず、正確に `declare(strict_types=1)` でなければなりません。（オプションのセミコロン終端子を含む）

<!-- Block declare statements are allowed and MUST be formatted as below. Note position of braces and spacing: -->
ブロック宣言文は許可され、以下のようにフォーマットしなければなりません。括弧とスペースの位置に注意してください。

```php

declare(ticks=1) {
    // some code
}
```

<!-- ## 4. Classes, Properties, and Methods -->
## 4. クラス、プロパティ、およびメソッド
<!-- The term "class" refers to all classes, interfaces, and traits. -->
"class" という用語は、すべてのクラス、インターフェース、トレイトを指します。

<!-- Any closing brace MUST NOT be followed by any comment or statement on the same line. -->
あらゆる閉じ括弧の後には、同じ行にコメントや文が続いてはなりません。

<!-- When instantiating a new class, parentheses MUST always be present even when there are no arguments passed to the constructor. -->
新しいクラスをインスタンス化する時、引数がコンストラクタに渡されない場合でも、常に括弧を使用しなければなりません。

```php
new Foo();
```

<!-- ### 4.1 Extends and Implements -->
### 4.1 拡張と実装
<!-- The `extends` and `implements` keywords MUST be declared on the same line as the class name. -->
`extends` と `implements` キーワードは、クラス名と同じ行に宣言しなければなりません。

<!-- The opening brace for the class MUST go on its own line; the closing brace for the class MUST go on the next line after the body. -->
クラスの開始括弧は、独自の行に配置しなければなりません。クラスの終了括弧は、本体の次の行に配置しなければなりません。

<!-- Opening braces MUST be on their own line and MUST NOT be preceded or followed by a blank line. -->
開始括弧は、独自の行に配置しなければなりません。また、前後に空行を配置してはなりません。

<!-- Closing braces MUST be on their own line and MUST NOT be preceded by a blank line. -->
終了括弧は、独自の行に配置しなければなりません。また、前に空行を配置してはなりません。

```php
<?php

namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class ClassName extends ParentClass implements \ArrayAccess, \Countable
{
    // constants, properties, methods
}
```

<!-- Lists of `implements` and, in the case of interfaces, `extends` MAY be split across multiple lines, where each subsequent line is indented once. When doing so, the first item in the list MUST be on the next line, and there MUST be only one interface per line. -->
`implements` のリストと、インターフェースの場合は `extends` のリストは、各行が1回インデントされた複数の行に分割することができます。その場合、リスト内の最初の項目は次の行に配置しなければならず、1行に1つのインターフェースしかないようにしなければなりません。

```php
<?php

namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class ClassName extends ParentClass implements
    \ArrayAccess,
    \Countable,
    \Serializable
{
    // constants, properties, methods
}
```

<!-- ### 4.2 Using traits -->
### 4.2 トレイトの使用
<!-- The use keyword used inside the classes to implement traits MUST be declared on the next line after the opening brace. -->
クラス内で使用されるトレイトを実装するためのuseキーワードは、開始括弧の次の行に宣言しなければなりません。

```php
<?php

namespace Vendor\Package;

use Vendor\Package\FirstTrait;

class ClassName
{
    use FirstTrait;
}
```

<!-- Each individual trait that is imported into a class MUST be included one-per-line and each inclusion MUST have its own `use` import statement. -->
クラスにインポートされる各個別のトレイトは、1行に1つずつ含まれていなければならず、各インクルードには独自の`use`インポート文が必要です。

```php
<?php

namespace Vendor\Package;

use Vendor\Package\FirstTrait;
use Vendor\Package\SecondTrait;
use Vendor\Package\ThirdTrait;

class ClassName
{
    use FirstTrait;
    use SecondTrait;
    use ThirdTrait;
}
```

<!-- When the class has nothing after the use import statement, the class closing brace MUST be on the next line after the use import statement. -->
クラスがuseインポート文の後に何も持たない場合、クラスの終了括弧はuseインポート文の次の行に配置しなければなりません。

```php
<?php

namespace Vendor\Package;

use Vendor\Package\FirstTrait;

class ClassName
{
    use FirstTrait;
}
```

<!-- Otherwise, it MUST have a blank line after the use import statement. -->
そうでない場合は、useインポート文の後に空行を置かなければなりません。

```php
<?php

namespace Vendor\Package;

use Vendor\Package\FirstTrait;

class ClassName
{
    use FirstTrait;

    private $property;
}
```

<!-- When using the `insteadof` and `as` operators they must be used as follows taking note of indentation, spacing, and new lines. -->
`insteadof` と `as` 演算子を使用する場合は、インデント、スペース、および改行に注意して、以下のように使用しなければなりません。

```php
<?php

class Talker
{
    use A;
    use B {
        A::smallTalk insteadof B;
    }
    use C {
        B::bigTalk insteadof C;
        C::mediumTalk as FooBar;
    }
}
```

<!-- ### 4.3 Properties and Constants -->
### 4.3 プロパティと定数
<!-- Visibility MUST be declared on all properties. -->
可視性はすべてのプロパティについて宣言しなければなりません。

<!-- Visibility MUST be declared on all constants if your project PHP minimum version supports constant visibilities (PHP 7.1 or later). -->
可視性は、プロジェクトのPHPの最小バージョンが定数の可視性をサポートしている場合（PHP 7.1以降）、すべての定数について宣言しなければなりません。

<!-- The `var` keyword MUST NOT be used to declare a property. -->
`var` キーワードを使用してプロパティを宣言してはなりません。

<!-- There MUST NOT be more than one property declared per statement. -->
1つの文に複数のプロパティを宣言してはなりません。

<!-- Property names MUST NOT be prefixed with a single underscore to indicate protected or private visibility. That is, an underscore prefix explicitly has no meaning. -->
protectedまたはprivateの可視性を示すために、プロパティ名をアンダースコアで始めてはなりません。つまり、アンダースコアの接頭辞には明示的には意味がありません。

<!-- There MUST be a space between type declaration and property name. -->
型宣言とプロパティ名の間にはスペースを置かなければなりません。

<!-- A property declaration looks like the following: -->
プロパティ宣言は以下のようになります。

```php
<?php

namespace Vendor\Package;

class ClassName
{
    public $foo = null;
    public static int $bar = 0;
}
```

<!-- ### 4.4 Methods and Functions -->
### 4.4 メソッドと関数
<!-- Visibility MUST be declared on all methods. -->
可視性はすべてのメソッドについて宣言しなければなりません。

<!-- Method names MUST NOT be prefixed with a single underscore to indicate protected or private visibility. That is, an underscore prefix explicitly has no meaning. -->
protectedまたはprivateの可視性を示すために、メソッド名をアンダースコアで始めてはなりません。つまり、アンダースコアの接頭辞には明示的には意味がありません。

<!-- Method and function names MUST NOT be declared with space after the method name. The opening brace MUST go on its own line, and the closing brace MUST go on the next line following the body. There MUST NOT be a space after the opening parenthesis, and there MUST NOT be a space before the closing parenthesis. -->
メソッド名や関数名は、その後にスペースを置いて宣言してはなりません。開始波括弧は独自の行に配置しなければならず、終了波括弧は本体の次の行に配置しなければなりません。開始丸括弧の後にスペースを置いてはならず、終了丸括弧の前にスペースを置いてはなりません。

<!-- A method declaration looks like the following. Note the placement of parentheses, commas, spaces, and braces: -->
メソッド宣言は以下のようになります。括弧、カンマ、スペース、波括弧の配置に注意してください。

```php
<?php

namespace Vendor\Package;

class ClassName
{
    public function fooBarBaz($arg1, &$arg2, $arg3 = [])
    {
        // method body
    }
}
```

<!-- A function declaration looks like the following. Note the placement of parentheses, commas, spaces, and braces: -->
関数宣言は以下のようになります。括弧、カンマ、スペース、波括弧の配置に注意してください。

```php
<?php

function fooBarBaz($arg1, &$arg2, $arg3 = [])
{
    // function body
}
```

<!-- ### 4.5 Method and Function Arguments -->
### 4.5 メソッドと関数の引数
<!-- In the argument list, there MUST NOT be a space before each comma, and there MUST be one space after each comma. -->
引数リストでは、カンマの前にスペースを置いてはならず、カンマの後にスペースを置かなければなりません。

<!-- Method and function arguments with default values MUST go at the end of the argument list. -->
メソッドと関数のデフォルト値のある引数は、引数リストの最後に配置しなければなりません。

```php
<?php

namespace Vendor\Package;

class ClassName
{
    public function foo(int $arg1, &$arg2, $arg3 = [])
    {
        // method body
    }
}
```

<!-- Argument lists MAY be split across multiple lines, where each subsequent line is indented once. When doing so, the first item in the list MUST be on the next line, and there MUST be only one argument per line. -->
引数リストは、各行が1回インデントされた複数の行に分割することができます。その場合、リスト内の最初の項目は次の行に配置しなければならず、1行に1つの引数しかないようにしなければなりません。

<!-- When the argument list is split across multiple lines, the closing parenthesis and opening brace MUST be placed together on their own line with one space between them. -->
引数リストが複数の行に分割される場合、終了丸括弧と開始波括弧は、それらの間に1つのスペースを置いて、独自の行に一緒に配置しなければなりません。

```php
<?php

namespace Vendor\Package;

class ClassName
{
    public function aVeryLongMethodName(
        ClassTypeHint $arg1,
        &$arg2,
        array $arg3 = []
    ) {
        // method body
    }
}
```

<!-- When you have a return type declaration present, there MUST be one space after the colon followed by the type declaration. The colon and declaration MUST be on the same line as the argument list closing parenthesis with no spaces between the two characters. -->
戻り値の型宣言がある場合、コロンの後には、型宣言が続くスペースが1つ必要です。コロンと宣言は、引数リストの終了丸括弧と同じ行に配置しなければなりません。2つの文字の間にスペースを置いてはなりません。

```php
<?php

declare(strict_types=1);

namespace Vendor\Package;

class ReturnTypeVariations
{
    public function functionName(int $arg1, $arg2): string
    {
        return 'foo';
    }

    public function anotherFunction(
        string $foo,
        string $bar,
        int $baz
    ): string {
        return 'foo';
    }
}
```

<!-- In nullable type declarations, there MUST NOT be a space between the question mark and the type. -->
null許容型宣言では、疑問符と型の間にスペースを置いてはなりません。

```php
<?php

declare(strict_types=1);

namespace Vendor\Package;

class ReturnTypeVariations
{
    public function functionName(?string $arg1, ?int &$arg2): ?string
    {
        return 'foo';
    }
}
```

<!-- When using the reference operator & before an argument, there MUST NOT be a space after it, like in the previous example. -->
引数の前に参照演算子&を使用する場合、前の例のように、その後にスペースを置いてはなりません。

<!-- There MUST NOT be a space between the variadic three dot operator and the argument name: -->
可変長引数の3点演算子と引数名の間にスペースを置いてはなりません。

```php
public function process(string $algorithm, ...$parts)
{
    // processing
}
```

<!-- When combining both the reference operator and the variadic three dot operator, there MUST NOT be any space between the two of them: -->
参照演算子と可変長引数の3点演算子を組み合わせる場合、2つの間にスペースを置いてはなりません。

```php
public function process(string $algorithm, &...$parts)
{
    // processing
}
```

<!-- ### 4.6 `abstract`, `final`, and `static` -->
### 4.6 `abstract`、`final`、および `static`
<!-- When present, the abstract and final declarations MUST precede the visibility declaration. -->
存在する場合、abstractとfinalの宣言は、可視性の宣言の前に配置しなければなりません。

<!-- When present, the static declaration MUST come after the visibility declaration. -->
存在する場合、staticの宣言は、可視性の宣言の後に配置しなければなりません。

```php
<?php

namespace Vendor\Package;

abstract class ClassName
{
    protected static $foo;

    abstract protected function zim();

    final public static function bar()
    {
        // method body
    }
}
```

<!-- ### 4.7 Method and Function Calls -->
### 4.7 メソッドと関数の呼び出し
<!-- When making a method or function call, there MUST NOT be a space between the method or function name and the opening parenthesis, there MUST NOT be a space after the opening parenthesis, and there MUST NOT be a space before the closing parenthesis. In the argument list, there MUST NOT be a space before each comma, and there MUST be one space after each comma. -->
メソッドや関数を呼び出す場合、メソッドや関数名と開始丸括弧の間にスペースを置いてはなりません。開始丸括弧の後にスペースを置いてはならず、終了丸括弧の前にスペースを置いてはなりません。引数リストでは、カンマの前にスペースを置いてはならず、カンマの後にスペースを置かなければなりません。

```php
<?php

bar();
$foo->bar($arg1);
Foo::bar($arg2, $arg3);
```

<!-- Argument lists MAY be split across multiple lines, where each subsequent line is indented once. When doing so, the first item in the list MUST be on the next line, and there MUST be only one argument per line. A single argument being split across multiple lines (as might be the case with an anonymous function or array) does not constitute splitting the argument list itself. -->
引数リストは、各行が1回インデントされた複数の行に分割しても構いません。その場合、リスト内の最初の項目は次の行に配置しなければならず、1行に1つの引数しかないようにしなければなりません。複数行に分割されている単一の引数（無名関数や配列の場合）は、引数リスト自体を分割するものではありません。

```php
<?php

$foo->bar(
    $longArgument,
    $longerArgument,
    $muchLongerArgument
);
```

```php
<?php

somefunction($foo, $bar, [
  // ...
], $baz);

$app->get('/hello/{name}', function ($name) use ($app) {
    return 'Hello ' . $app->escape($name);
});
```

<!-- ## 5. Control Structures -->
## 5. 制御構造
<!-- The general style rules for control structures are as follows: -->
制御構造の一般的なスタイルルールは以下の通りです。

<!-- - There MUST be one space after the control structure keyword
- There MUST NOT be a space after the opening parenthesis
- There MUST NOT be a space before the closing parenthesis
- There MUST be one space between the closing parenthesis and the opening brace
- The structure body MUST be indented once
- The body MUST be on the next line after the opening brace
- The closing brace MUST be on the next line after the body -->
- 制御構造キーワードの後には1つのスペースを置かなければなりません。
- 開始丸括弧の後にスペースを置いてはなりません。
- 終了丸括弧の前にスペースを置いてはなりません。
- 終了丸括弧と開始波括弧の間には1つのスペースを置かなければなりません。
- 構造体の本体は1回インデントされなければなりません。
- 本体は開始波括弧の次の行に配置しなければなりません。
- 終了波括弧は本体の次の行に配置しなければなりません。

<!-- The body of each structure MUST be enclosed by braces. This standardizes how the structures look and reduces the likelihood of introducing errors as new lines get added to the body. -->
制御構造の本体は波括弧で囲まれていなければなりません。これにより、構造の見た目が標準化され、本体に新しい行が追加されたときにエラーが発生する可能性が低くなります。

### 5.1 `if`, `elseif`, `else`
<!-- An `if` structure looks like the following. Note the placement of parentheses, spaces, and braces; and that `else` and `elseif` are on the same line as the closing brace from the earlier body. -->
`if` 構造は以下のようになります。括弧、スペース、波括弧の配置に注意してください。また、`else` と `elseif` は、前の本体の終了波括弧と同じ行にあります。

```php
<?php

if ($expr1) {
    // if body
} elseif ($expr2) {
    // elseif body
} else {
    // else body;
}
```

<!-- The keyword `elseif` SHOULD be used instead of `else if` so that all control keywords look like single words. -->
すべての制御キーワードが単語のように見えるようにするために、`else if` の代わりに`elseif` キーワードが使用されるべきです。

<!-- Expressions in parentheses MAY be split across multiple lines, where each subsequent line is indented at least once. When doing so, the first condition MUST be on the next line. The closing parenthesis and opening brace MUST be placed together on their own line with one space between them. Boolean operators between conditions MUST always be at the beginning or at the end of the line, not a mix of both. -->
丸括弧の中の式は、各行が1回インデントされた複数の行に分割することができます。その場合、最初の条件は次の行に配置しなければなりません。終了丸括弧と開始波括弧は、それらの間に1つのスペースを置いて、独自の行に一緒に配置しなければなりません。条件間のブール演算子は、常に行の先頭または行の末尾に配置しなければならず、両方の混合であってはなりません。

```php
<?php

if (
    $expr1
    && $expr2
) {
    // if body
} elseif (
    $expr3
    && $expr4
) {
    // elseif body
}
```

### 5.2 `switch`, `case`
<!-- A `switch` structure looks like the following. Note the placement of parentheses, spaces, and braces. The `case` statement MUST be indented once from `switch`, and the `break` keyword (or other terminating keywords) MUST be indented at the same level as the `case` body. There MUST be a comment such as `// no break` when fall-through is intentional in a non-empty `case` body. -->
`switch` 構造は以下のようになります。括弧、スペース、波括弧の配置に注意してください。`case` 文は `switch` から1回インデントされ、`break` キーワード（またはその他の終端キーワード）は `case` 本体と同じレベルにインデントされなければなりません。`case` 本体が空でないとき、意図的にフォールスルーする場合は、`// no break` のようなコメントを付けなければなりません。

```php
<?php

switch ($expr) {
    case 0:
        echo 'First case, with a break';
        break;
    case 1:
        echo 'Second case, which falls through';
        // no break
    case 2:
    case 3:
    case 4:
        echo 'Third case, return instead of break';
        return;
    default:
        echo 'Default case';
        break;
}
```

<!-- Expressions in parentheses MAY be split across multiple lines, where each subsequent line is indented at least once. When doing so, the first condition MUST be on the next line. The closing parenthesis and opening brace MUST be placed together on their own line with one space between them. Boolean operators between conditions MUST always be at the beginning or at the end of the line, not a mix of both. -->
丸括弧の中の式は、各行が少なくとも1回インデントされた複数の行に分割することができます。その場合、最初の条件は次の行に配置しなければなりません。終了丸括弧と開始波括弧は、それらの間に1つのスペースを置いて、独自の行に一緒に配置しなければなりません。条件間のブール演算子は、常に行の先頭または行の末尾に配置しなければならず、両方の混合であってはなりません。

```php
<?php

switch (
    $expr1
    && $expr2
) {
    // structure body
}
```

### 5.3 `while`, `do while`
<!-- A `while` statement looks like the following. Note the placement of parentheses, spaces, and braces. -->
`while` 文は以下のようになります。括弧、スペース、波括弧の配置に注意してください。

```php
<?php

while ($expr) {
    // structure body
}
```

<!-- Expressions in parentheses MAY be split across multiple lines, where each subsequent line is indented at least once. When doing so, the first condition MUST be on the next line. The closing parenthesis and opening brace MUST be placed together on their own line with one space between them. Boolean operators between conditions MUST always be at the beginning or at the end of the line, not a mix of both. -->
丸括弧の中の式は、各行が少なくとも1回インデントされた複数の行に分割することができます。その場合、最初の条件は次の行に配置しなければなりません。終了丸括弧と開始波括弧は、それらの間に1つのスペースを置いて、独自の行に一緒に配置しなければなりません。条件間のブール演算子は、常に行の先頭または行の末尾に配置しなければならず、両方の混合であってはなりません。

```php
<?php

while (
    $expr1
    && $expr2
) {
    // structure body
}
```

<!-- Similarly, a do while statement looks like the following. Note the placement of parentheses, spaces, and braces. -->
似たように、do while 文は以下のようになります。括弧、スペース、波括弧の配置に注意してください。

```php
<?php

do {
    // structure body;
} while ($expr);
```

<!-- Expressions in parentheses MAY be split across multiple lines, where each subsequent line is indented at least once. When doing so, the first condition MUST be on the next line. Boolean operators between conditions MUST always be at the beginning or at the end of the line, not a mix of both. -->
丸括弧の中の式は、各行が少なくとも1回インデントされた複数の行に分割することができます。その場合、最初の条件は次の行に配置しなければなりません。条件間のブール演算子は、常に行の先頭または行の末尾に配置しなければならず、両方の混合であってはなりません。

```php
<?php

do {
    // structure body;
} while (
    $expr1
    && $expr2
);
```

### 5.4 `for`
<!-- A `for` statement looks like the following. Note the placement of parentheses, spaces, and braces. -->
`for` 文は以下のようになります。括弧、スペース、波括弧の配置に注意してください。

```php
<?php

for ($i = 0; $i < 10; $i++) {
    // for body
}
```

<!-- Expressions in parentheses MAY be split across multiple lines, where each subsequent line is indented at least once. When doing so, the first expression MUST be on the next line. The closing parenthesis and opening brace MUST be placed together on their own line with one space between them. -->
丸括弧の中の式は、各行が少なくとも1回インデントされた複数の行に分割することができます。その場合、最初の式は次の行に配置しなければなりません。終了丸括弧と開始波括弧は、それらの間に1つのスペースを置いて、独自の行に一緒に配置しなければなりません。

```php
<?php

for (
    $i = 0;
    $i < 10;
    $i++
) {
    // for body
}
```

### 5.5 `foreach`
<!-- A `foreach` statement looks like the following. Note the placement of parentheses, spaces, and braces. -->
`foreach` 文は以下のようになります。括弧、スペース、波括弧の配置に注意してください。

```php
<?php

foreach ($iterable as $key => $value) {
    // foreach body
}
```

### 5.6 `try`, `catch`, `finally`
<!-- A `try-catch-finally` block looks like the following. Note the placement of parentheses, spaces, and braces. -->
`try-catch-finally` ブロックは以下のようになります。括弧、スペース、波括弧の配置に注意してください。

```php
<?php

try {
    // try body
} catch (FirstThrowableType $e) {
    // catch body
} catch (OtherThrowableType | AnotherThrowableType $e) {
    // catch body
} finally {
    // finally body
}
```

<!-- ## 6. Operators -->
## 6. 演算子
<!-- Style rules for operators are grouped by arity (the number of operands they take). -->
演算子のスタイルルールは、arity（そられがとるオペランドの数）によってグループ化されます。

<!-- When space is permitted around an operator, multiple spaces MAY be used for readability purposes. -->
演算子の周りにスペースを許可する場合、可読性を高めるために複数のスペースを使用することができます。

<!-- All operators not described here are left undefined. -->
ここで説明されていないすべての演算子は未定義のままです。

<!-- ### 6.1. Unary operators -->
### 6.1 単項演算子
<!-- The increment/decrement operators MUST NOT have any space between the operator and operand. -->
インクリメントまたはデクリメント演算子は、演算子とオペランドの間にスペースを置いてはなりません。

```php
$i++;
++$j;
```

<!-- Type casting operators MUST NOT have any space within the parentheses: -->
型キャスト演算子は、丸括弧の中にスペースを置いてはなりません。

```php
$intValue = (int) $input;
```

<!-- ### 6.2. Binary operators -->
### 6.2 二項演算子
<!-- All binary arithmetic, comparison, assignment, bitwise, logical, string, and type operators MUST be preceded and followed by at least one space: -->
全ての算術、比較、代入、ビット演算、論理、文字列、型の二項演算子は、前後に少なくとも1つのスペースを置かなければなりません。

```php
if ($a === $b) {
    $foo = $bar ?? $a ?? $b;
} elseif ($a > $b) {
    $foo = $a + $b * $c;
}
```

<!-- ### 6.3. Ternary operators -->
### 6.3 三項演算子
<!-- The conditional operator, also known simply as the ternary operator, MUST be preceded and followed by at least one space around both the ? and : characters: -->
条件演算子（三項演算子とも呼ばれる）は、? と : の両方の文字の前後に少なくとも1つのスペースを置かなければなりません。

```php
$variable = $foo ? 'foo' : 'bar';
```

<!-- When the middle operand of the conditional operator is omitted, the operator MUST follow the same style rules as other binary comparison operators: -->
条件演算子の中間オペランドが省略されている場合、演算子は他の二項比較演算子と同じスタイルルールに従わなければなりません。

```php
$variable = $foo ?: 'bar';
```

<!-- ## 7. Closures -->
## 7. クロージャー
<!-- Closures MUST be declared with a space after the `function` keyword, and a space before and after the `use` keyword. -->
クロージャーは、`function` キーワードの後にスペースを置いて宣言し、`use` キーワードの前後にスペースを置かなければなりません。

<!-- The opening brace MUST go on the same line, and the closing brace MUST go on the next line following the body. -->
開始波括弧は同じ行に配置しなければならず、終了波括弧は本体の次の行に配置しなければなりません。

<!-- There MUST NOT be a space after the opening parenthesis of the argument list or variable list, and there MUST NOT be a space before the closing parenthesis of the argument list or variable list. -->
開始丸括弧の後にスペースを置いてはならず、終了丸括弧の前にスペースを置いてはなりません。

<!-- In the argument list and variable list, there MUST NOT be a space before each comma, and there MUST be one space after each comma. -->
引数リストと変数リストでは、カンマの前にスペースを置いてはならず、カンマの後にスペースを置かなければなりません。

<!-- Closure arguments with default values MUST go at the end of the argument list. -->
クロージャーのデフォルト値を持つ引数は、引数リストの最後に配置しなければなりません。

<!-- If a return type is present, it MUST follow the same rules as with normal functions and methods; if the `use` keyword is present, the colon MUST follow the `use` list closing parentheses with no spaces between the two characters. -->
戻り値の方が存在する場合、通常の関数やメソッドと同じルールに従わなければなりません。`use` キーワードが存在する場合、コロンは `use` リストの終了丸括弧の後に、2つの文字の間にスペースを置かずに配置しなければなりません。

<!-- A closure declaration looks like the following. Note the placement of parentheses, commas, spaces, and braces: -->
クロージャーの宣言は以下のようになります。括弧、カンマ、スペース、波括弧の配置に注意してください。

```php
<?php

$closureWithArgs = function ($arg1, $arg2) {
    // body
};

$closureWithArgsAndVars = function ($arg1, $arg2) use ($var1, $var2) {
    // body
};

$closureWithArgsVarsAndReturn = function ($arg1, $arg2) use ($var1, $var2): bool {
    // body
};
```

<!-- Argument lists and variable lists MAY be split across multiple lines, where each subsequent line is indented once. When doing so, the first item in the list MUST be on the next line, and there MUST be only one argument or variable per line. -->
引数リストと変数リストは、各行が1回インデントされた複数の行に分割することができます。その場合、リスト内の最初の項目は次の行に配置しなければならず、1行に1つの引数または変数しかないようにしなければなりません。

<!-- When the ending list (whether of arguments or variables) is split across multiple lines, the closing parenthesis and opening brace MUST be placed together on their own line with one space between them. -->
終了リスト（引数または変数）が複数の行に分割される場合、終了丸括弧と開始波括弧は、それらの間に1つのスペースを置いて、独自の行に一緒に配置しなければなりません。

<!-- The following are examples of closures with and without argument lists and variable lists split across multiple lines. -->
以下は、引数リストと変数リストが複数の行に分割されたクロージャーの例です。

```php
<?php

$longArgs_noVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) {
   // body
};

$noArgs_longVars = function () use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
   // body
};

$longArgs_longVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
   // body
};

$longArgs_shortVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) use ($var1) {
   // body
};

$shortArgs_longVars = function ($arg) use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
   // body
};
```

<!-- Note that the formatting rules also apply when the closure is used directly in a function or method call as an argument. -->
クロージャーが引数として関数やメソッドの呼び出しに直接使用される場合でも、フォーマットルールが適用されることに注意してください。

```php
<?php

$foo->bar(
    $arg1,
    function ($arg2) use ($var1) {
        // body
    },
    $arg3
);
```

<!-- ## 8. Anonymous Classes -->
## 8. 無名クラス
<!-- Anonymous Classes MUST follow the same guidelines and principles as closures in the above section. -->
無名クラスは、上記のセクションにあるクロージャーと同じガイドラインと原則に従わなければなりません。

```php
<?php

$instance = new class {};
```

<!-- The opening brace MAY be on the same line as the class keyword so long as the list of implements interfaces does not wrap. If the list of interfaces wraps, the brace MUST be placed on the line immediately following the last interface. -->
開始波括弧は、implementsインターフェースのリストが折り返されない限り、classキーワードと同じ行にあっても構いません。インターフェースのリストが折り返される場合は、波括弧は最後のインターフェースの直後の行に配置しなければなりません。

```php
<?php

// Brace on the same line
$instance = new class extends \Foo implements \HandleableInterface {
    // Class content
};

// Brace on the next line
$instance = new class extends \Foo implements
    \ArrayAccess,
    \Countable,
    \Serializable
{
    // Class content
};
```
