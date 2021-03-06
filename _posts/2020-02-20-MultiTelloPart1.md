---
layout: post
author: Hiroto Kaneko
title: Tello EDU 4台を使ったドローン編隊飛行に挑戦（第1回：ざっくり全体像）
tags:
---
今回から Tello EDU 4台を使ってドローン編隊飛行に挑戦していきます！

Tello EDU（[Tello EDU 公式サイト](https://www.ryzerobotics.com/jp/tello-edu)）は、香港のとなりのIT産業の盛んな町、深圳のベンチャー企業 Ryze Technology 社から発売されている小さなちいさなドローンです。同じ会社から発売されている無印の Tello との最大の違いは、なんと複数台で編隊飛行ができること！

今回から4回に分けて、プログラミング言語 Python を使った Tello EDU の編隊飛行までの道のりを紹介していきたいと思います。

[第2回](https://ku-macs-com.github.io/2020/03/25/MultiTelloPart2.html) - [第3回](https://ku-macs-com.github.io/2020/03/25/MultiTelloPart3.html) - [第4回](https://ku-macs-com.github.io/2020/03/25/MultiTelloPart4.html)

### ゴールを確認！

まずは目指すゴールを動画で確認しましょう！ これは実際に京大 MACS のメンバーで編隊飛行を試みて、成功した様子を撮ったものです。このシリーズでは、これを目指していきます。

{% include youtube.html id="l33BURhMC2A" %}

{% include youtube.html id="ts2wrf0xiUg" %}


### 用意するもの

次の3つが必要になります。

1. パソコン（ Windows でも Mac でもどちらでも OK ）
2. Tello EDU 4台（4台でなくとも2台以上あれば OK です）
3. 無線ルータ（ SSID とパスワードがわかれば既設のものでも OK ）

それから、Tello EDU を飛ばせる広めのスペースも重要です！8畳ぐらいのスペースがあれば大丈夫だと思います。注意点としては、カーペット敷きなど光を散乱する床の場合、Tello EDU の能動型赤外線センサが作動しなくなり、失敗します。光を反射する床のスペースを選びましょう。

### ざっくり全体像

次のステップで編隊飛行の準備をしていきます。

1. Python 環境の構築（ Anaconda のインストールと仮想環境の作成）
2. Tello EDU 編隊飛行用レポジトリ [Multi-Tello-Formation](https://github.com/TelloSDK/Multi-Tello-Formation) の導入
3. Tello EDU の設定を変更し無線ルータに接続
4. 無線ルータ経由で Tello SDK コマンドを Tello EDU に送信し編隊飛行を実行

1と2を[第2回](https://ku-macs-com.github.io/2020/03/25/MultiTelloPart2.html)、3と4を[第3回](https://ku-macs-com.github.io/2020/03/25/MultiTelloPart3.html)で詳しく紹介していきたいと思います。3と4において Tello EDU に Tello SDK コマンドを送信する際には、ソケット通信を使います。今回は Python の機能（[公式ドキュメント](https://docs.python.org/ja/3/library/socket.html)）を使ってソケット通信を行っていますが、node.js など別の言語を使ってもソケット通信は可能です。今回はわかりやすくするために、言語は Python に絞って説明していきます。

最終的に構築されるシステムは、図のようになります。

<img src="/images/kaneko/tello_multi_system.png" width="300">

初期設定ではドローンとパソコンが直接接続されるために1台のみしか制御できませんが、Tello EDU と無線ルータ、無線ルータとパソコン、というように無線ルータを間に挟んで接続することで、複数台（今回は4台）の編隊飛行が可能になります。

### 次回

[次回](https://ku-macs-com.github.io/2020/03/25/MultiTelloPart2.html)は、Tello EDU 編隊飛行のための Python 環境の構築について詳しく紹介していく予定です！
