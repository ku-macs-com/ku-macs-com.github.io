---
title: Rust で emojify
layout: post
author: Daichi Mukai
---

Rust で emojify を書いたので宣伝です。
リポジトリは [こちら](https://github.com/daichimukai/emojify) にあります。

インストール
------------
Rust プログラマの方は
```
$ cargo install emojify
```
で OK です。
`cargo` って何という方は、これを期に Rust をインストールしてみて下さい。 [rustup](https://rustup.rs/) を利用するのが標準的です。
リンク先を見て頂けるとわかるようにワンライナーの実行だけですのでとても簡単です。rustup をインストールすると `cargo` も一緒に
インストールされますので、その後上のコマンドで emojify をインストールして下さい。

使い方
------
引数としてとるか、パイプで渡すかです。前者なら
```
$ emojify "Good night :moon:"
Good night 🌔
```
のように使い、後者なら
```
$ echo "Good morning :sunrise:" | emojify
Good morning 🌅
```

実装
----
Rust で `:sparkles:` のような文字列を対応する絵文字に置き換えてくれる crate である[emojicons](https://github.com/jiri/rust-emojicons) を利用しました。
はじめはライブラリを使わずその処理も自前で作っていたのですが、release でビルドするときだけひどく時間がかかったので emojicons を使いました。

crates.io
---------
作った crate を始めて [crates.io](https://crates.io) に上げました。
そこまでハマりポイントもないですね。

さいごに
--------
ぜひ使ってみてフィードバックを下さい。Issue や Pull Request お待ちしております。
