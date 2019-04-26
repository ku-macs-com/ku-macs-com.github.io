---
layout: post
author: Akira SARASHINA
title: ksnapshot を使って Raspberry pi でスクリーンショットを撮る
tags:
---

[前回のブログ](https://ku-macs-com.github.io/2019/03/31/systemd_timer.html)を書く際にraspberry piでスクリーンショットを撮りたいと思いksnapshotというパッケージをインストールしました。今回はknapshotのインストールのやり方と簡単な使い方を書きます。

###ksnapshotをインストールする

> $ sudo apt-get install ksnapshot

ファイルマネージャを開き「ツール→ファイルを検索する」でksnapshotを検索します。
ksnapshotという名前のファイル(歯車のマーク)が現れるので右クリックし「パスをコピーする」を選択します。

次に設定からMain Menu Editorを開きグラフィックスの「新しいアイテム」を選択します。

<img src="/images/sarashina/main_menu_editor.png" width="300">

> Name: ksnapshot  
> Command: Control+V (i.e. 上でコピーしたパス)  

と入力して「OK」をクリックします。
するとメニューのグラフィックスからksnapshotが使えるようになります。

どのような条件かわかりませんが何度か使用しているうちにksnapshotが「グラフィックス」から「その他」に移動していました。もし「グラフィックス」の中に無かったら「その他」を見てみると良いかもしれません。

### スクリーンショットを撮る

<img src="/images/sarashina/ksnapshot.png" width="400">

「Area: Window Under Cursor」で特定のウインドウのスクリーンショットが取れます。

 「On Click」をチェックしておくと「Take a New Screenshot」をクリックした後マウスが + のような形になり、撮影したいウインドウの上でクリックするとそのウインドウのスクリーンショットが撮れます。

「Include mouse pointer」をチェックを外しておくと、スクリーンショットを撮った際に画面内にマウスがあっても撮影した画像に反映されないのでオススメです。
 
### 注意
 
「Include window titlebar and boreders」のチェックを外すと(なぜか)画面内の別の場所のスクリーンショットが取られてしまいうまくいきませんでした。
  
たまに(おそらくウインドウが小さいときに)撮ったスクリーンショットのプレビューの色が反転している事がありますが保存される画像は元の色で保存されています。

### 感想
思ったより使い勝手が良くて満足しました。
