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

### ソート

```cpp
   sort(v.begin(),v.end());
```

### 重複要素を削除する

```cpp
   v.erase(unique(v.begin(), v.end()),v.end());
```

参考:https://qiita.com/ysk24ok/items/30ae72f4f1060b088588


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
