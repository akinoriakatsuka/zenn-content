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
## 最大値・最小値

```cpp:Main.cpp
#include <iostream>
using namespace std;

int main()
{
  int list[] = {1,2,3,4,5};

  cout << min_element(list, list + 5) << endl; // 最小の要素のポインタ
  cout << *min_element(list, list + 5) << endl; // 1
  cout << max_element(list, list + 5) << endl; //  最大の要素のポインタ
  cout << *max_element(list, list + 5) << endl; // 5

  return 0;
}
```
