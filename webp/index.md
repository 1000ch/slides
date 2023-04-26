---
marp: true
title: WebP - A new image format for the Web
theme: default
paginate: true
footer: WebP - A new image format for the Web by [@1000ch](https://bento.me/1000ch)
---

![bg blur:1px brightness:0.8](./img/inokashira.jpg)

<!-- _class: invert -->

# <!-- fit --> Introduction to **WebP**

A new image format for the Web

---

![bg left:30% 60%](https://shogosensui.com/img/1000ch.avif)

# @1000ch

> Web アプリケーション開発を専門とするソフトウェアエンジニア。企業で働く傍ら、技術顧問として複数企業のエンジニアリングに関わり、高品質で維持しやすい Web アプリケーションを作るための活動を続けている。

---

# WebP とは？

- Google が開発する新しい画像フォーマット
- 可逆/非可逆圧縮・アルファチャネル・アニメーションなど豊富な機能
- 高圧縮率でファイルサイズがとても軽い

---

## どのくらい軽量なのか

- 可逆圧縮 → PNG 比で約 26 %小さい
- 非可逆圧縮 → JPEG 比で約 25 %~ 34 %小さい
- アルファチャネル付きの非可逆圧縮 → PNG 比で3倍以上小さい

---

<!-- _class: invert -->

## 1000ch.jpg (圧縮レベル80で33KB)

![bg](./img/1000ch.jpg)

---

<!-- _class: invert -->

## 1000ch.webp (圧縮レベル80で15KB)

![bg](./img/1000ch.jpg)

---

<!-- _class: invert -->

# <!-- fit --> 利用に向けて

---

## サポート環境

- Chrome/Firefox/Safari を含む最新モダンブラウザ
- macOS 11 Big Sur or later
- Windows 10 or later

---

## iOS 14.0 未満の Safari だと…

![bg contain](./img/webp-safari.jpg)

---

### iOS 14.0 未満の Chrome だと…

![bg contain](./img/webp-chrome.jpg)

---

## 非対応ブラウザのために

- [vwebp](https://developers.google.com/speed/webp/docs/vwebp) で表示し、[dwebp](https://developers.google.com/speed/webp/docs/dwebp) でデコードしたり、[Chrome Frame を使ってきた](https://cloud.googleblog.com/2013/06/retiring-chrome-frame.html)
- [WebPJS](https://github.com/obartra/webpjs) で `.webp` を dataURI に変換する
- `Accept: image/webp` がない場合に、異なる画像フォーマットを返却する
- `<picture>` 要素と `<source type="image/webp">` 要素で条件分岐する

やりようはいくらでもある

---

<!-- _class: invert -->

# <!-- fit --> 各種変換ツール

---

## CLI ツール

- [cwebp](https://developers.google.com/speed/webp/docs/precompiled): Homebrew からもインストール可
- [cwebp-bin](https://github.com/imagemin/cwebp-bin): cwebp の Node.js ラッパー

---

## GUI ツール

- [Squoosh](https://squoosh.app/): 画像の最適化やフォーマットの変換などを行う Web アプリ
- [WebPonize](http://github.com/webponize/webponize) - PNG/JPEG/GIF を WebP に変換する macOS アプリ

---

## WebPonize

![](./img/webponize.jpg)

Drag & Drop!

---

## WebPonize の機能

- ImageOptim にそっくりなインターフェース
- ドラッグアンドドロップで変換できる、複数ファイルのドロップも OK
- PNG・JPEG・GIF（アニメーションGIF）に対応している
- オプションで圧縮率やアルファチャネルを設定できる
