---
layout: post
author: Hiroto Kaneko
title: Tello EDU 4台を使ったドローン編隊飛行に挑戦（第3回：実際に編隊飛行してみる！！）
tags:
---
Tello EDU 4台を使ったドローン編隊飛行に挑戦するシリーズ、第3回です。

Tello EDU（[Tello EDU 公式サイト](https://www.ryzerobotics.com/jp/tello-edu)）は、香港のとなりのIT産業の盛んな町、深圳のベンチャー企業 Ryze Technology 社から発売されている小さなちいさなドローンです。同じ会社から発売されている無印の Tello との最大の違いは、なんと複数台で編隊飛行ができること！

第3回では、前回準備した環境を使って実際に Tello EDU を編隊飛行させてみます！

### Tello EDU と無線ルータの接続

まずは Tello EDU と無線ルータを接続します。初期状態では Tello EDU はパソコンや携帯電話と一対一で接続し、通信を行うことができます。ところがこれでは複数台の制御は不可能なため、Tello EDU を無線ルータに接続した上で、無線ルータを介した制御を行うわけです。

概念図は、こんな感じになります。

<img src="/images/kaneko/tello_multi_system.png" width="300">

前回導入した Multi-Tello-Formation の中には `formation_setup.py` という Python プログラムがあると思います。これをエディタで開き、26行目（一番下）の関数

`set_ap('Tello_Nest', 'tellotello')`

の引数を変更します。最初の引数 'Tello_Nest' に接続したい無線ルータの SSID、2番目の引数 'tellotello' にパスワードを入力します。例えば

`set_ap('Buffalo-G-A480', 'korewanisemono')`

と言う感じです。

次に、Tello EDU とパソコンを接続します。パソコンの Wi-Fi 設定画面を開くと、`TELLO-58XXXX` というような名前 (SSID) が見つかると思います。それを選んで接続すると、Tello EDU とパソコンが接続されます。この SSID は、TELLO EDU の機体から電池を抜くと、内側に書いてありますので、確認しておきましょう。

最後に、formation_setup.py を実行して Tello EDU と無線ルータに接続します。この際まず、前回作成した仮想環境に入っておきます。その上で

`$ python formation_setup.py`

と打つと、プログラムが実行され、Tello EDU と無線ルータに接続します。この作業を4台全ての Tello EDU に対して行えば OK です！

ちなみに、Tello EDU を再び一対一接続の設定に戻すには、電源ボタンの長押しをします。

### 飛行プログラムの作成

テスト用に、4台の Tello EDU が離陸して、15秒後に着陸するという、ただそれだけの飛行プログラムを作成します。テキストファイルに、以下の内容を書き込んで `multi_tello_test.py` と同じ場所に保存してください。名前はなんでも良いです（ここでは `test_flight.txt` としましょう）。

`test_flight.txt`
```
scan 4 
battery_check 20
correct_ip
1=0TQDXXXXXXXXXX
2=0TQDXXXXXXXXXX
3=0TQDXXXXXXXXXX
4=0TQDXXXXXXXXXX
*>takeoff
sync 15
*>land
```

ここで、`1=0TQDXXXXXXXXXX` などのイコールの後ろ側 `0TQDXXXXXXXXXX` の部分には、各 Tello EDU のシリアルナンバーを入力してください。このシリアルナンバーも、TELLO EDU の機体から電池を抜くと、内側に書いてありますので、確認しておきましょう。

### Take off!!!!!

長かった準備も終わり、ついに take off の瞬間がやってきました！まず、Wi-Fi 設定画面を開き、パソコンと無線ルータを接続します。次に、前回作成した仮想環境に入っておきます。そして

`$ python multi_tello_test.py test_flight.txt`

と打つと、4台の Tello EDU が同時に離陸するはずです！！！そしてすぐ着陸するはずです。。。これではつまらない。。。次回はもっといろいろな動きをさせてみましょう！

### 次回

次回は4台の Tello EDU に色々な動きをさせて、格好良い編隊飛行に挑戦しましょう！
