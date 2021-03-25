---
layout: post
author: Hiroto Kaneko
title: Tello EDU 4台を使ったドローン編隊飛行に挑戦（第4回：格好良い編隊飛行に挑戦！！）
tags:
---
Tello EDU 5台を使ったドローン編隊飛行に挑戦するシリーズ、第4回です。

Tello EDU（[Tello EDU 公式サイト](https://www.ryzerobotics.com/jp/tello-edu)）は、香港のとなりのIT産業の盛んな町、深圳のベンチャー企業 Ryze Technology 社から発売されている小さなちいさなドローンです。同じ会社から発売されている無印の Tello との最大の違いは、なんと複数台で編隊飛行ができること！

前回までで、実際に Tello EDU 4台を一度に離陸させ、着陸させることに成功しました。第4回では、いろいろな動きを取り入れた格好良い編隊飛行に挑戦します！

[第1回](https://ku-macs-com.github.io/2020/02/20/MultiTelloPart1.html) - [第2回](https://ku-macs-com.github.io/2020/03/25/MultiTelloPart2.html) - [第3回](https://ku-macs-com.github.io/2020/03/25/MultiTelloPart3.html)

### 前回の飛行プログラムの解説

[前回](https://ku-macs-com.github.io/2020/03/25/MultiTelloPart3.html)作ったのは、4台の Tello EDU が離陸して、15秒後に着陸するという、ただそれだけの飛行プログラムでした。まず初めに、これを `multi_tello_test.py` により実行した際になにが起こっているのか、解説します。飛行プログラムは、こんな内容でした。

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

`multi_tello_test.py` は、このプログラムを上から順に読み込んでいきます。

まず `scan 4` では4台の Tello EDU をネットワーク上で探索します。次に `battery_check 20` では各 Tello EDU のバッテリー残量をチェックし、20%以上あることを確認します（なかったらプログラムを停止します）。次の `correct_ip` で各 Tello EDU に割り当てられたIPアドレスを確認し、シリアルナンバーと紐付けます。そして `1=0TQDXXXXXXXXXX` などでは今度は飛行プログラム上の番号とシリアルナンバーとを紐付けます。ここまでは必ず必要な部分で、準備の段階にあたります。

ここからは、Tello EDU に動作を制御する Tello SDK コマンドを送信していきます。まず、 `*>takeoff` では `takeoff` という Tello SDK コマンドを1番から4番全ての Tello EDU に向けてソケット通信により送信します。ここで `*>` の部分は全ての Tello EDU に向けてコマンドを送信すると言う意味で、例えば `1>` などとすると1番の Tello EDU のみに向けてコマンドを送信することができます。続く `sync 15` では、単に15秒間待ちます。Tello EDU は、コマンドを受信して動作を行い、その動作が完了する前に次のコマンドを受信した場合はそのコマンドは無視します。そのために `sync 15` が必要になるわけです。最後に `*>land` で全て着陸します。

### Tello SDK コマンドについて

結局、[前回](https://ku-macs-com.github.io/2020/03/25/MultiTelloPart3.html)の飛行プログラム `test_flight.txt` は、全ての Tello EDU に向けて `takeoff` と `land` という Tello SDK コマンドを送っていたので離陸し、着陸したわけです。この Tello SDK コマンド、実は多数用意されていて、色々な動作を Tello EDU に命令することができます。たとえば 100 cm 上昇させたいなら

`up 100`

を、前方に宙返りさせたいなら

`flip f`

を送信します。

Tello EDU のパッケージにはミッションパッドという数字とロケット、そのほかの模様の書かれた板が同封されていたと思います。Tello EDU は、下部の能動型赤外線センサによってこのミッションパッドを認識し、今何番のミッションパッドの中心から見てどの位置にいるかを知ることができます。このミッションパッドを使った少し複雑な Tello SDK コマンドも用意されていて、例えば

`go 0 0 50 30 m3`

と言う感じです。これは3番のミッションパッドの中心から x = 0 cm (縦方向)、 y = 0 cm (横方向)、 z = 50 cm (天地方向) に毎秒 30 cm の速さで移動すると言う意味になります。ミッションパッドではロケットの向きが x 軸の正の向きと決められている点には注意してください。

こうした Tello SDK コマンドを組み合わせて飛行プログラムに書き込めば、格好良い編隊飛行が可能になります！ Tello SDK コマンドは他にも多数あり、詳しくは Ryze Technology 社が公開しているユーザガイド（[Tello SDK 2.0 User Guide.pdf](https://dl-cdn.ryzerobotics.com/downloads/Tello/Tello%20SDK%202.0%20User%20Guide.pdf)）を参考にしてみてください。

### ぐるっと回って宙返り！

それでは、実際に格好良い編隊飛行に挑戦してみましょう！ まずは、「ぐるっと回って宙返り」です。飛行プログラムは以下の通り。

`round_and_move_by_flip.txt`
```
scan 4
battery_check 20
correct_ip
1=0TQDXXXXXXXXXX
2=0TQDXXXXXXXXXX
3=0TQDXXXXXXXXXX
4=0TQDXXXXXXXXXX
*>mon
*>takeoff
sync 15
1>jump -100 0 200 30 -90 m1 m2
2>jump 0 -100 200 30 0 m2 m3
3>jump 100 0 200 30 90 m3 m4
4>jump 0 100 200 30 180 m4 m1
sync 15
1>flip f
2>flip f
3>flip f
4>flip f
sync 15
1>go 0 0 50 30 m3
2>go 0 0 50 30 m4
3>go 0 0 50 30 m1
4>go 0 0 50 30 m2
sync 15
*>land
```

ミッションパッド1番から4番を時計回りに並べて、その上に1番から4番の Tello EDU を置いておきます。そして上記の `round_and_move_by_flip.txt` を実行すると、下の動画のように、「ぐるっと回って宙返り」するはずです！

{% include youtube.html id="l33BURhMC2A" %}

### ドローンの交差！

次は、「ドローンの交差」です。飛行プログラムは以下の通り。

`cross.txt`
```
scan 4
battery_check 20
correct_ip
1=0TQDXXXXXXXXXX
2=0TQDXXXXXXXXXX
3=0TQDXXXXXXXXXX
4=0TQDXXXXXXXXXX
*>mon
*>takeoff
sync 15
1>go 0 0 100 30 m1
2>go 0 0 200 30 m2
3>go 0 0 200 30 m3
4>go 0 0 100 30 m4
sync 15
1>jump -100 -100 100 30 0 m1 m3
2>stop
3>jump 100 100 200 30 0 m3 m1
4>stop
sync 5
1>stop
2>jump 100 -100 200 30 0 m2 m4
3>stop
4>jump -100 100 100 30 0 m4 m2
sync 15
*>land
```

先ほどと同じく、ミッションパッド1番から4番を時計回りに並べて、その上に1番から4番の Tello EDU を置いておきます。そして上記の `cross.txt` を実行すると、下の動画のように、1番と3番のドローンが交差して場所を入れ替え、続いて2番と4番のドローンが交差するはずです！

{% include youtube.html id="ts2wrf0xiUg" %}

### まとめ

これで、4回に分けてお送りした、Tello EDU 4台を使ったドローン編隊飛行に挑戦するシリーズはおしまいです。

編隊飛行に成功するまで、なかなか長い道のりでした。

京大 MACS SG10 の有志で2019年の秋頃から何度が集まり、飛行を試してしましたが、最初はいくら試しても上手くいきませんでした。そして20年の2月の発表会を目前にして、もう発表会には間に合わないかと絶望しかけていたとき、その原因に気付きました。「カーペットがいけない」と。

Tello EDU が自分の位置を知る唯一の手段は、下部に搭載された能動型赤外線センサで、ここから照射される赤外線をきちんと反射する床であることが Tello EDU の飛行には欠かせません。それに気付いてから、一気に編隊飛行の成功までたどり着けました！

2月の発表会のあと、この編隊飛行の成功までの過程を広くシェアしたいと思い、早速第1回の記事を書きました。その後毎週ぐらいのペースで書けたらなと思っていたのですが、なかなかやる気が起きず、1ヶ月後の今日、第2回から第4回まで同時公開という形になりました。なんか全然シリーズ感ない！！けどおっけーとしましょう！！
