---
marp: true
title: Webフロントエンドの変遷 2017年初春
theme: default
paginate: true
footer: Webフロントエンドの変遷 2017年初春 by [@1000ch](https://shogosensui.com)
---

<!-- _class: invert -->

# <!-- fit --> Webフロントエンドの変遷 2017年初春

2017.02.16 [Developer Summit 2017](http://event.shoeisha.jp/devsumi/20170216/session/1270/)

---

![bg left:30% 60%](https://shogosensui.com/img/1000ch.avif)

# @1000ch

> Web アプリケーション開発を専門とするソフトウェアエンジニア。企業で働く傍ら、様々な企業のエンジニアリングに顧問として関わり、高品質で維持しやすい Web アプリケーションを作るための活動を続けている。

---

# ドキュメントからアプリケーションへ

Web の役割の変化に応じてアーキテクチャが高度化してきた

---

## フレームワーク・ライブラリ

- prototype.js、jQuery -> DOM抽象
- Backbone、Angular v1.x -> MVC抽象
- React、Vue.js -> コンポーネント抽象

---

## よりダイナミックな Web へ

- XMLHttpRequest の台頭
- Single Page Application の普及

---

## 開発環境の複雑化と Node.js の普及

- コマンドラインによる作業の抽象化
- Grunt や Gulp などのタスクランナーによる自動化
- npm scripts や Makefile への回帰

---

# Web フロントエンドの専門化と分業化

---

![bg brightness:0.5](./img/smartphone.jpg)

<!-- _class: invert -->

## ネイティブアプリの隆盛

---

## Web に足りなかったもの

- 初期化と実行時のパフォーマンス
- プッシュ通知によるエンゲージメント
- デバイス固有の機能へのアクセス

<blockquote class="twitter-tweet" data-lang="ja"><p lang="en" dir="ltr">A year ago, I asked what features made you turn to native. #1 response: push notifications. Today, they&#39;re available: <a href="http://t.co/wDOKa5qVbf">http://t.co/wDOKa5qVbf</a></p>&mdash; Paul Irish (@paul_irish) <a href="https://twitter.com/paul_irish/status/576089864514326528">2015年3月12日</a></blockquote>

---

## ブラウザのパフォーマンスと HTML 描画の壁

---

## Virtual DOM

- [なぜ仮想DOMという概念が俺達の魂を震えさせるのか](http://qiita.com/mizchi/items/4d25bc26def1719d52e6)
- DOM の diff と patch アルゴリズムによる HTML の差分描画
- Server Side Rendering への回帰

---

## Universal JavaScript

- サーバーとクライアントの両方で動作する JavaScript
- [Server Side Rendering と Single Page Application](https://havelog.ayumusato.com/develop/javascript/e675-spa_and_server_rendering_with_fluxible.html) の同居
- 品質の優位性と開発時のメリットを享受できる

---

## Web Standards

- W3C と WHATWG
- [Extensible Web](http://jxck.hatenablog.com/entry/extendthewebforward)
- [Vendor Prefix](https://developer.mozilla.org/ja/docs/Glossary/Vendor_Prefix) から [Origin Trials](https://blog.jxck.io/entries/2016-09-29/vender-prefix-to-origin-trials.html) へ
- ECMAScript のバージョニング

---

## <del>選択肢の変遷</del> ≠ 選択肢の増加

---

# 技術ではなく課題へのフォーカス
