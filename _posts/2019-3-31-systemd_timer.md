---
layout: post
author: Akira SARASHINA
title: systemd.timer で定刻にコマンドを実行する
tags:
---
今回はRaspberry Piでsystemd.timerを使ってコマンドを定刻に実行する方法を書きます。おそらくDebian系OSならRaspberry Piでなくても同じ事が出来ると思います。

### 実行するコマンドを用意する

まず~/Documentsにdt.pyというファイル名で現在時刻をdt.txtというファイルに書き込むコマンドを用意します。

<!--
<img src="/images/sarashina/image1.png" width="400">
-->
<img src="/images/sarashina/dt_py.png" width="500">

### seviceファイルを作成する

/usr/lib/systemd/systemにdt.serviceという名前の以下のようなファイルを作成します。

<img src="/images/sarashina/dt_service.png" width="500">

[Unit]セクションにはこのUnitの説明を書きます。    
Unitという単語はsystemdで管理するプログラムの総称のようで、ここで作成したサービス(.service)はUnitの一種です。  
ここではDescriptionしか書いていませんが他の情報や設定も書く事ができます。

serviceファイルには[Service]セクションが必要で、ここにはこのUnit特有の設定を書きます。  
他のUnitとの依存関係や優先順位など一般的な設定は[Unit]セクションや[Install]セクション(このファイルにはない)に書くらしいです。  

Typeではこのサービスがどのように動作するかを大雑把に指定しているようです。  
このプログラムのように実行した後にプロセスが終了する場合はoneshotとします。

ExecStartでは実行するコマンドを指定します。

### timerファイルを作成する

/usr/lib/systemd/systemにdt.timerという名前の以下のようなファイルを作成します。  
拡張子より前の部分(ここではdt)は上で用意した.serviceファイルと一致している必要があります。

<img src="/images/sarashina/dt_timer.png" width="500">

[Timer]セクションのOnCalenderではコマンドを実行する時間を指定します。  
hourlyなら各時間の00分00秒にコマンドを実行します。

Persistent=trueとしておくと電源が切れていた等の理由でコマンドの最後の実行時間が過ぎていた場合に自動で実行してくれます(自動でactiveにしてくれるわけではないです)。

[Install]セクションにはsystemctlのenableやdisableコマンド実行時の設定を書きます。  
細かい仕様は理解していませんがWantedByに別のUnitを指定すると、そのUnitがstartされた時にこのUnitもstartされるようです。  
ここではtimers.targetというUnitを使ってこのコマンドを実行しているのだと思います。

### timerを起動する

LXTerminalで以下のコマンドを実行します。

> $ sudo systemctl start dt.timer
 
ちゃんとactiveになっているかは以下のコマンドで確認できます。

> $ systemctl status dt.timer

### ちゃんと動いているか確認

dt.txtを見てみます。

<img src="/images/sarashina/dt_txt.png" width="500">

成功!

### 参考にしたサイト

[Debian Manpages](https://manpages.debian.org/stretch/systemd/systemd.timer.5.en.html)

[ArchWiki](https://wiki.archlinux.jp/index.php/Systemd/タイマー)

ArchWikiにはサンプルファイルが載ってるので、それを雛形にして作りました。  
細かい仕様についてはDebian Manpagesを見ましたがlinuxに関する知識の問題で理解できないところも多かったです。