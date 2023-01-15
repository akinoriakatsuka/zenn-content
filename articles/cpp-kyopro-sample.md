---
title: "競技プログラミングでよく使うコード"
emoji: "😊"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["cpp","競技プログラミング"]
published: true
---

# 概要
よく使うコードを備忘録としてまとめておきます。
随時更新していきます。

# 出力

```cpp:Main.cpp
#include <iostream>
using namespace std;

int main()
{
  cout << "Hello World!" << endl; // Hello World!

  return 0;
}
```

# 入力

## 標準入力を受け取る

```txt:入力例
3
```

```cpp:Main.cpp
#include <iostream>
using namespace std;

int main()
{
  int n;
  cin >> n;

  return 0;
}
```

## 標準入力をN個受け取る

```txt:入力例
3
1 10 100
```

```cpp:Main.cpp
#include <iostream>
using namespace std;

int main()
{
  int n;
  cin >> n;
  int a[n];
  for (int i = 0; i < n; i++)
    cin >> a[i];
  
  return 0;
}
```

# 処理

## 配列

### ソート

```cpp:Main.cpp
#include <iostream>
using namespace std;

int main()
{
  int n = 5;
  int array[] = {1, 3, 5, 2, 4};

  sort(array, array + n); // 1,2,3,4,5
  sort(array, array + 5, greater<int>()); // 5,4,3,2,1
}
```

### 最大値・最小値

```cpp:Main.cpp
#include <iostream>
using namespace std;

int main()
{
  int array[] = {1,2,3,4,5};

  cout << min_element(array, array + 5) << endl; // 最小の要素のポインタ
  cout << *min_element(array, array + 5) << endl; // 1
  cout << max_element(array, array + 5) << endl; //  最大の要素のポインタ
  cout << *max_element(array, array + 5) << endl; // 5

  return 0;
}
```

## ベクトル

### 長さNのベクトルを作る

```cpp:Main.cpp
#include <iostream>
#include <vector>
using namespace std;

int main()
{
  int n = 5;
  cin >> n;
  vector<int> v(n);
  for (int i = 0; i < n; i++)
    cin >> v[i];
  return 0;
}
```

:::message alert
`v(n)`として長さを設定しないと、`cin >> v[i];`で値を割り当てる際にSegmentation faultとなる
:::

### ソート

```cpp
   sort(v.begin(),v.end());
```

### 重複要素を削除する

```cpp
   v.erase(unique(v.begin(), v.end()),v.end());
```

参考:https://qiita.com/ysk24ok/items/30ae72f4f1060b088588

### リサイズ

領域を確保する時に用いる。

```cpp
   v.resize(n)
```

## 整数

### 二進数

```cpp:Main.cpp
#include <iostream>
#include <bitset>
using namespace std;

int main()
{
  int number = 65535;
  bitset<32> bs(number);
  cout << bs << endl; // 00000000000000001111111111111111

  return 0;
}
```

## 文字・文字列

```cpp:Main.cpp
#include <iostream>
using namespace std;

int main()
{
  string s = "Some String";
  return 0;
}
```

### 反転させる

```cpp:Main.cpp
#include <iostream>
using namespace std;

int main()
{
  string s = "Some String";
  reverse(s.begin(),s.end());
  cout << s << endl; // gnirtS emoS

  return 0;
}
```

### 前方一致しているか判別する
```cpp:Main.cpp
#include <iostream>
using namespace std;

int main()
{
  string s1 = "abcde";
  string s2 = "abc";
  string s3 = "cde";

  cout << equal(s2.begin(),s2.end(),s1.begin()) << endl; // 1
  cout << equal(s3.begin(),s3.end(),s1.begin()) << endl; // 0

  return 0;
}
```

### 文字列の一部を削除する
```cpp:Main.cpp
#include <iostream>
using namespace std;

int main()
{
  string s = "abcde";
  s.erase(0,3);

  cout << s << endl; // de

  return 0;
}
```

### 文字コードを取得する

`+`を前につければ良い

```cpp:Main.cpp
#include <iostream>
using namespace std;

int main()
{
  string a = "A";
  cout << +a[0] << endl; // 65
  cout << +a[0] - 64 << endl; // 1
  return 0;
}
```