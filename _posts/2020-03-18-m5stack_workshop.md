---
layout: post
author: Akira SARASHINA
title: M5Stackのワークショップを開催しました
tags:
---
3/13(金)に株式会社eftaxの小林万寿夫さんを講師として招いてM5Stackの使い方を学ぶワークショップを開催しました。参加者はSG10の参加教員である藤先生と私を含むSG10の学生5人の計6人でした。以下では今回のワークショップで学んだ内容を書いていきます。

<img src="/images/sarashina/m5stack_1.jpg" width="400">

講師の小林万寿夫さん

<br>

### M5Stackとは
M5Stackとはモニター、スピーカー、バッテリー、3つのボタン等を備えた小型のコンピュータです。Raspberry PiのようにOSが載っているわけではありません。別のWindows、Mac OSまたはLinuxを備えたコンピュータに接続し、そちらで書いたコードをビルドする事で様々な動きができます。

<img src="/images/sarashina/m5stack_2.jpg" width="400">

### ホスト側の環境構築
まず始めにModdable SDKというソフトウェアを開発するための環境を[Moddable SDKのGitHubページ](https://github.com/Moddable-OpenSource/moddable/blob/public/documentation/Moddable%20SDK%20-%20Getting%20Started.md)に書いてあるとおりに手持ちのコンピュータにインストールします。ここで該当するOSのHost environment setupとESP32 setupに書いてある操作を行います。ESP32とはM5Stackを構成する機材の一部(CPUやメモリ等)です。

### M5Stackを動かす
自分でプログラムを書いて動かすためにはJavaScript等を学ぶ必要があるので、今回は[meganetaaanさんのGitHubページ](https://github.com/meganetaaan/moddable-examples)で公開されているコードをダウンロードしてそれを動かしてみました。

まず上記のリポジトリをローカルにクローンし、ターミナルで興味のあるサンプルのディレクトリに移動します。そこで以下のコマンドを入力すると該当するプログラムがビルドされてM5Stackが動きます。
> $ mcconfig -d -m -p esp32/m5stack

一度ビルドしてしまえば手持ちのコンピュータに接続している必要はなく、バッテリーもついているので取り外しても使えます。

<img src="/images/sarashina/m5stack_3.jpg" width="400">

これは「bongo」というゲームをプレイしているところです。左右のボタンを押すと猫がボンゴを叩き、真ん中のボタンを押すと鳴きます。

### 感想
既に書いた特徴に加えて、持ち運びがしやすい形状である事や背面についている磁石で金属に貼り付ける事ができる点を活かして色々と使い道がありそうな気がしました。
