# What's StoryboardHeper

![画像](http://i.imgur.com/zmFJl1q.jpg)

StoryboardHelperは、iOSアプリ開発初心者が各端末への画面サイズの対応を直感的に行い、なるべく簡単にアプリをリリースするためのヘルパーです。AutoLayout、SizeClassなどを一切使わずに各端末への画面サイズに対応できます。ViewControllerの数が少ないアプリでの使用を想定していますののでらあらかじめご理解下さい。

# How to use StoryboardHelper
以下では、StoryboardHelperの使い方について説明しています。

## ①プロジェクトの設定
1. Xcodeを起動し、プロジェクトを作成します。すでにプロジェクトがある場合はそれを開きます。
2. `Main.storyboard`を開き、中央下部の`View as: iPhoneXX`を**iPhone SE**のサイズにします。
3. `LaunchScreen.xib`ファイルを右クリックし、Deleteを選択して削除します。
4. プロジェクトファイルの設定からLaunchScreenを削除します。

![画像](http://i.imgur.com/DpME0go.gif)

5. StoryboardHelperをXcodeの左側のフォルダ部分にドラッグ&ドロップでコピーします。
6. そのとき、Destinationにチェックが入っていること、Refereneの選択が上の方を選んでいること、Targetにチェックが入っていることに気をつけましょう。
7. 先程消したLaunchScreenの上のLaunch Images SourceのUse Asset Catalog...をクリックしLaunchScreenを選択してください。もし赤文字になった場合はもう一度クリックしLaunchImageをしましょう。
8. この時点でiPhone5/5S/6/6Plus/6s/6sPlus/7/7Plusへの対応は完了です。

## ②3.5インチ端末(iPhone4S以下)とiPadへの対応
1. `AppDelegate.swift`を開きます。
2. `application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool { ... }` メソッド内に以下のプログラムを書きます。なおdevicesにはXcodeの対応デバイスの設定に合わせて`.universal`,`.iPhone`,`.iPad`のいずれかを選択してください。
```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    /* ここから */
    StoryboardHelper.adjust(to: window, devices: .universal)
    /* ここまで */

    return true
}
```
3. NewFileから「`3.5inch.storyboard`」という名前で新しいStoryboardファイルを作成します。
4. `Main.storyboard`からViewController群をコピーし、`3.5inch.storyboard`に貼り付けます。
5. 3.5inchの方の`initialViewController`のチェックが外れているので、チェックを入れます。
6. 3.5inchの方のデザインを整えます。
7. Runしてうまくいけば完成です。

## iPhone X, XS, XR, XS Maxへの対応

こちらは5.8inch.storyboardという名前でiPhone XS向けレイアウトを、6.5inch.storyboardという名前でiPhoneXR向けレイアウトを同様に作成することで対応できます。

## LunchScreenを設定したい人、または上級者向けカスタマイズ方法

- LaunchScreenを自分のオリジナルにしたい人はDMStoryboardHelperのDefaultsの中のLaunchScreen.xcassetsに入っている画像を同解像度の使いたい画像に置き換えてください
- iOSの仕様上、LaunchScreen.xcassetsで設定されているデバイスはその比率で、設定されていないものはそれよりも小さい解像度でもっとも近いものが拡大されて表示されるようになっています。このヘルパーの初期状態ではiPhone 8やiPhone 8 PlusのLaunchScreenを空にしているためこれらのサイズの端末ではiPhone SE向けのデザインが拡大表示されています。それが嫌な場合は同梱されている画像該当の部分に設定して、StoryboardHelperの該当デバイスの部分で別のStoryboardを読み込むように書き直してください。
- 逆にStoryboardの数をへらすことも同様の原理でできます。その場合iPhone X, XS, XR, XS Maxに関しては上部と下部に大きく黒い余白が取られることになるので注意してください。

## iPad 12.9 3rd genに関して

こちらは外側に小さく黒い余白ができるようになっています。これは現状の仕様だとうめられないようです。あらかじめご了承ください。
