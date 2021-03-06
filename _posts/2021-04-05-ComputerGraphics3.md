---
layout: post
author: Kion Imai
title: コンピュータグラフィックスでキャラクター制作をしてみよう（第3回：UV展開って？）
tags:
---
CGによるキャラクター制作に挑戦するシリーズの第3回です。

CGを用いた映像制作の工程は第1回の時に挙げた工程の他にも多く存在します。
キャラクターモデリング、ハードサーフェスモデリング、背景モデリング、リギング、アニメーション、テクスチャ、ライティング、エフェクト、レンダリング、コンポジットなどなど・・・
それぞれの工程ごとに専属のアーティストがいます。
その他に、各工程との連携を可能にするゼネラリストやテクニカルアーティストがいたりもします。
どの工程も重要なポイントを持っていてとても楽しそうです！

さて、前回に引き続き今回もEVANGELION初号機を制作していきます。
特に、UV展開と呼ばれる工程を紹介していきます！

### UV展開って？
UV展開とは3次元のモデルの展開図を作る作業になります。
CG作品は3次元のオブジェクトに2次元の画像を貼り付けることで出来上がります。
その際、貼り付け方を決める必要があります。
つまり3次元のオブジェクトと2次元の画像を結び付けるための展開図を定義してやる必要があるということです！
作業そのものは単純で裁縫をしているような感覚です！
3Dオブジェクトを切ったり縫合したりしながら展開図を制作していきます！

<img src="/images/KionImai/UV.png" width="300">

これは立方体に対してUV展開を行った時の図です。
左の立方体に白のカット線を入れることで右のような展開図が出来上がります！
基本的には切ったり縫合したりしながら広げて並べるだけなので簡単な工程です！

それでは実際に、初号機に対してUV展開をしてみます！

### 初号機のUV展開
前回までに制作してきた初号機モデルに対してUV展開を施していきます。
全ての部品に対してUV展開を行うのは骨の折れる作業ですが完成を楽しみにして頑張りましょう(笑)
こちらが実際にUV展開を行った結果です。

<img src="/images/KionImai/EVAUV.png" width="300">

展開図が正方形のブロックごとに分けて配置されていることが分かります。
このブロック１つ１つはUdimと呼ばれています。
UV展開の作成時には注意事項があるので記しておきます。
1. 展開図はなるべく歪みが少なくなるように作成します。歪みを少なくしておくことで綺麗にテクスチャを貼ることができます。
2. モデルのスケールと展開図のスケールはおおよそ等しくなるようにしておきます。つまり、大きな部品には大きな展開図を定義し、小さな部品には小さな展開図を割り当てます。部品ごとにテクスチャの解像度が違うと見栄えが悪くなってしまいます。
3. 1つのUdimの中には同じような色や質感の展開図を配置しておきます。こうしておくことで、テクスチャ制作(第4回)の負担が大きく軽減されます。
4. 展開図はなるべく無駄が少なくなるように敷き詰めましょう。展開図の大きさは大きいほど滑らかな絵になるのですが、大きすぎると計算量が増えてしまいます。計算時間を抑えつつ滑らかな表現ができるように、可能な限りUdimのスペースいっぱいいっぱいに配置しましょう。

慣れてくると鼻歌を歌いながらでもできるので楽しい作業です(笑)

### 次回
次回はテクスチャ制作をしていきます！
この工程を行うことで一気に絵が映えるようになるのでテンションも上がります。
楽しんで制作しましょう。
