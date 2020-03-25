---
layout: post
author: Hiroto Kaneko
title: Tello EDU 4台を使ったドローン編隊飛行に挑戦（第2回：Python 環境の構築）
tags:
---
Tello EDU 4台を使ったドローン編隊飛行に挑戦するシリーズ、第2回です。

Tello EDU（[Tello EDU 公式サイト](https://www.ryzerobotics.com/jp/tello-edu)）は、香港のとなりのIT産業の盛んな町、深圳のベンチャー企業 Ryze Technology 社から発売されている小さなちいさなドローンです。同じ会社から発売されている無印の Tello との最大の違いは、なんと複数台で編隊飛行ができること！

第2回では、Python を使った Tello EDU の制御に向けて、Python 環境を構築し、編隊飛行用のレポジトリを導入していきます。

[第1回](https://ku-macs-com.github.io/2020/02/20/MultiTelloPart1.html) - [第3回](https://ku-macs-com.github.io/2020/03/25/MultiTelloPart3.html) - [第4回](https://ku-macs-com.github.io/2020/03/25/MultiTelloPart4.html)

### Python 環境構築とは？

今回ドローンの制御には、プログラミング言語 Python を使っています。この Python、Mac や Linux では初めから入っている状態ですし、Windows でも Python の公式サイトから最新版をダウンロードできます。

しかし Python を実用的に使いこなしていくには、初めから入っていたり公式サイトからダウンロードしたものではダメで、「環境構築」が欠かせません。それはなぜかというと、30年近いの歴史のある Python には最新版以外にも複数のバージョンがあり、時と場合に応じてそれらを使い分けていく必要があるからです。

今回 Python 環境の構築は Anaconda をベースに進めていきます（すでに Anaconda を使っていたり、ほかの方法で環境を作って使っている場合は、斜め読みしてしてもらって構いません）。

### Anaconda のインストール

Anaconda は、Python のための仮想環境を作成・管理するソフトウェアです。一つひとつの仮想環境に特定のバージョンの Python と、Python で書かれた様々なパッケージを導入していきます。この仮想環境を切り替えることで、時と場合に応じて様々な味付けの Python を使い分けることができるわけです。

それでは、Anaconda のインストールをしましょう。Anaconda のインストールの手順は、インストールしたいパソコンの環境によって次の2つに分かれます。

#### 1. Windows ユーザ、Mac ユーザ （homebrew を使っていない場合）
この場合、Anaconda のインストールは超簡単です！まず、 [Anaconda の公式サイト](https://www.anaconda.com/)にアクセスし、メニューから Individual Edition を選んでインストーラーをダウンロードします。あとは指示にしたがってインストールすれば完了です！

#### 2. Mac ユーザ （homebrew を使っている場合）、Linux ユーザ
この場合、Anaconda のインストールはちょっと複雑です。Anaconda とパッケージ管理ソフトウェア homebrew あるいは apt-get が干渉すると言う問題があるためです。そこでまず homebrew あるいは  apt-get を使って pyenv をインストールし、その pyenv を使って Anaconda をインストールすると言う形で、ワンクッション挟みます。詳しい手順は [Qiita の @aical さんの記事](https://qiita.com/aical/items/2d066801a7464a676994) が参考になると思います。

### 仮想環境の作成

Anaconda のインストールが終わったら、Tello EDU の制御のための仮想環境を作成しましょう。仮想環境には、Python 2.7 と、パッケージ netaddr 並びに netifaces を導入します。ターミナル（Windows の場合は Anaconda プロンプト）を開いて以下のコマンドを入力して実行します。

`$ conda create -n tello -c conda-forge python=2.7 netaddr netifaces`

これで完了です！

少しコマンドの意味を解説したいと思います。まず `conda create` は「仮想環境を作成する」という Anaconda のコマンドで、引数には導入する Python のバージョンとパッケージを指定します。オプション `-n tello` は、仮想環境の名前を tello に指定しています。ここは好きな名前にしてもらって大丈夫です。オプション `-c conda-forge` はパッケージを探すチャンネルを指定しています。conda-forge には Python で書かれた便利なツールが無数に登録されており、Python の人気の理由の一つにもなっています。

### ネットワーク制御パッケージ netaddr と netifaces

さて、仮想環境に導入したパッケージ netaddr と netifaces についても少し解説してみます。これらは Python を使って IPアドレスの検出や設定など、ネットワークの制御を行う際に便利なパッケージです。今回はドローンと無線ルータを接毒した際に、無線ルータが各ドローンに何番のIPアドレスを割り当てたのかを知るためにこれらのパッケージを使用します。

### 仮想環境への入り方と抜け出し方

作成した仮想環境に入るには

`$ conda activate tello`

と打ちます。仮想環境から抜け出すには、

`$ conda deactivate`

と打ちます。

### 編隊飛行用のレポジトリの導入

さて、これで準備が整いました。あとは git-hub 上で公式に公開されている Tello EDU 編隊飛行のレポジトリを導入しましょう。git-hub のレポジトリ [Multi-Tello-Formation](https://github.com/TelloSDK/Multi-Tello-Formation) にアクセスし、Clone or download から Download ZIP を選択し、ダウンロードして解凍します（git を使っている方は clone してもいいと思います）。これで導入完了です！

### 次回

[次回](https://ku-macs-com.github.io/2020/03/25/MultiTelloPart3.html)は、今回準備した環境を使って実際に Tello EDU を編隊飛行させてみましょう！
