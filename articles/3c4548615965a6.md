---
title: "【Swift】Dynamic island をとりあえず使ってみる"
emoji: "📖"
type: "tech"
topics:
  - "swift"
published: true
published_at: "2022-12-13 20:52"
---

SwiftKotlin愛好会アドベントカレンダー14日目の記事です。
https://qiita.com/advent-calendar/2022/love_swift_kotlin

# 概要
ライブアクティビティを表示するための仕組みとしてiPhone14 Proから新しく追加されたDynamic islandを使ってみる記事です。

![](https://storage.googleapis.com/zenn-user-upload/8da167c61625-20221213.png)

いくつかチュートリアルがあったのですが、UIの作成などが多く、とりあえず動かすという観点からは複雑すぎるものが多かったので、最小限のコードで表示させてみるところまでの手順を紹介します。

ソースコードは[こちら](https://github.com/akinoriakatsuka/ios-dynamic-island-sample)

https://github.com/akinoriakatsuka/ios-dynamic-island-sample

# 環境

MacOS Version 13.0.1（22A400）
Xcode Version 14.1 (14B47b)

# 手順

## プロジェクトの作成

PlatformはiOS
Applicationはappを選択

プロジェクト名はここでは、LiveActivitiesとする

![](https://storage.googleapis.com/zenn-user-upload/0d5ad2cb0937-20221213.png)

## Targetの追加

![](https://storage.googleapis.com/zenn-user-upload/f3d9eba80374-20221213.png)

![](https://storage.googleapis.com/zenn-user-upload/bc20ce672d00-20221213.png)

Target名はここでは、OrderStatusとする

![](https://storage.googleapis.com/zenn-user-upload/eedb539ad96c-20221213.png)

エクステンションのschemeを有効にするか聞かれるので、**Cancel**と答える

### Target Membershipの追加

OrderStatusLiveActivity.swiftをメインのプロジェクトから参照できるようにTargetMembershipのLiveActivitiesにチェックをつける

![](https://storage.googleapis.com/zenn-user-upload/2b7254fc5525-20221213.png)

## info.plistにNSSupportsLiveActivitesを追加し値をYesにする

![](https://storage.googleapis.com/zenn-user-upload/dc6696374b9d-20221213.png)


## 画面にLiveActivityを呼び出すボタンを追加

ContentView.swiftを以下のように変更

```swift:ContentView.swift
import SwiftUI
import ActivityKit

struct ContentView: View {
    var body: some View {
        VStack {
            Button("Add Live Activity") {
                addLiveActivity()
            }
        }
        .padding()
    }
    
    func addLiveActivity(){
        let orderAttributes = OrderStatusAttributes(name: "test")
        let initialContentState = OrderStatusAttributes.ContentState(value: 1)
        
        do{
            let activity = try Activity<OrderStatusAttributes>.request(attributes: orderAttributes, contentState: initialContentState)
            print("Activity Added Successfully. id: \(activity.id)")
        }catch{
            print(error.localizedDescription)
        }
        
    }
}

struct ContentView_Previews: PreviewProvider {
    static var previews: some View {
        ContentView()
    }
}
```

Targetを作った時にデフォルトのAttributesとContentStateのコードが書かれているので、それに従ってActivityを設定します。
```Activity<T>.request()```の部分で実際にLiveActivityを追加しています。

## 実行

![](https://storage.googleapis.com/zenn-user-upload/51b87e8fca21-20221213.png =250x)
*アプリの画面*

![](https://storage.googleapis.com/zenn-user-upload/046251158617-20221213.png =250x)
*ホーム画面　デフォルトのViewとしてLeadingにはLがTrailingにはTが表示されている*

![](https://storage.googleapis.com/zenn-user-upload/8a20694f79f1-20221213.png =250x)
*Dynamic islandを長押しすると、ExpandedのViewが表示される*

![](https://storage.googleapis.com/zenn-user-upload/dcd15b8ec90c-20221213.png =250x)
*ロック画面*

# トラブルシューティング

## SendProcessControlEvent:toPid: encountered an error: Error

ビルドスキームがエクステンションになっていないか確認

![](https://storage.googleapis.com/zenn-user-upload/c457ecf6d761-20221213.png)

## The operation couldn’t be completed. (com.apple.ActivityKit.ActivityInput error 1.)

[info.plistにNSSupportsLiveActivitiesを設定](#info.plist%E3%81%ABnssupportsliveactivites%E3%82%92%E8%BF%BD%E5%8A%A0%E3%81%97%E5%80%A4%E3%82%92yes%E3%81%AB%E3%81%99%E3%82%8B)

## Cannot find 'OrderStatusAttributes' in scope

[OrderStatusLiveActivity.swiftのTarget MembershipにLiveActivitiesがチェックされているか確認](#target-membershipの追加)

# 参考
- https://developer.apple.com/documentation/activitykit
- https://www.youtube.com/watch?v=mBAgCZJr6jw
- https://qiita.com/MaShunzhe/items/6cc8d9d204f40cbee19c