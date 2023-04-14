---
marp: true
theme: default
paginate: true
footer: Introduction to Resource Hints by [Shogo SENSUI](https://bento.me/1000ch)
---

![bg brightness:0.5](./img/cover.jpg)

<!-- _class: invert -->

# Introduction to Resource Hints

2016.12.05 [Frontrend Vol.8](https://frontrend.connpass.com/event/45238/) [@1000ch](http://twitter.com/1000ch)

---

## @1000ch

- 株式会社サイバーエージェント
- 専門は Web 技術全般
- 趣味で Node.js や iOS など

---

![bg brightness:0.5](./img/cat-reading.gif)

<!-- _class: invert -->

## Resource Hints とは

これから必要になるリソースを `<link>` 要素で定義し、それをブラウザが **投機的に** 取得する機能

---

# 投機的に？

---

![bg brightness:0.5](./img/cat-jumping.gif)

<!-- _class: invert -->

## 「成否は確実でないが、機会を上手く利用して利益を得ようとする行為を形容する。」

現在のページロードを邪魔しないように、ブラウザがアイドルの時に必要になるリソースをロードしてもらう

---

## [Resource Hints](https://w3c.github.io/resource-hints/)

- [DNS Prefetch](https://w3c.github.io/resource-hints/#dns-prefetch): 投機的な DNS 解決
- [Preconnect](https://w3c.github.io/resource-hints/#preconnect): 投機的な TCP 接続
- [Prefetch](https://w3c.github.io/resource-hints/#prefetch): 投機的なリソース取得
- [Prerender](https://w3c.github.io/resource-hints/#prerender): 投機的なページ描画

---

<!-- _class: invert -->

## DNS Prefetch

```html
<link rel="dns-prefetch" href="//example.com">
```

- 指定したオリジンへの DNS 解決を行う
- ドメインがわかるが、スキーマが定まらない場合に使う

---

<!-- _class: invert -->

## Preconnect

```html
<link rel="preconnect" href="//example.com">
<link rel="preconnect" href="//cdn.example.com" crossorigin>
```

- 指定したオリジンへの DNS 解決を含む TCP 接続を行う
- ドメイン及びスキーマがわかっている場合に使う

---

<!-- _class: invert -->

## Prefetch

```html
<link rel="prefetch" href="//example.com/next-page.html" as="html" crossorigin="use-credentials">
<link rel="prefetch" href="/library.js" as="script">
```

- 指定した URL のリソースを取得する
- `as` はオプショナルだが、付けておくと良い

---

## Preload directive

- **(none)**: XHR, fetch	`link rel=preload href=...`
- **media**: `audio`, `video`
- **script**: `script`, importScripts の script
- **style**: `link rel="stylesheet"`, CSS の `@import`
- **font**: CSS の `@font-face`
- **image**: `img`, `picture`, `srcset`, CSS の `-image`

他には `worker`, `embed`, `object`, `documenet` など

---

<!-- _class: invert -->

## Prerender

```html
<link rel="prerender" href="//example.com/next-page.html">
```

- 指定した URL の HTML ドキュメントの取得及び評価を行う
- 描画まで実行するので、高速にナビゲーションされる
- コストも大きいので、次に発生する可能性の高いナビゲーションに対して実施すると良い

---

<!-- _class: invert -->

## Hint probability

```html
<link rel="dns-prefetch" href="//widget.com" pr="0.75">
<link rel="preconnect" href="//cdn.example.com" pr="0.42">
<link rel="prefetch" href="//example.com/next-page.html" pr="0.75">
<link rel="prerender" href="//example.com/thankyou.html" pr="0.25">
```

- リソースの優先度を `pr` 属性に `0.0~1.0` で指定する

---

## 👆 ハイコストハイリターン

- `prerender`: 予め決まった遷移、プライマリなアクション
- `prefetch`: クリティカルなCSS/JS、キーとなるメディア
- `preconnect`: 別ドメインのAPIサーバーやCDN
- `dns-prefetch`: 同上

## 👇 ローコストローリターン

---

## Chrome の Prerender History

[`chrome://net-internals/#prerender`](chrome://net-internals/#prerender)

---

<!-- _class: invert -->

## Try in your browser?

```javascript
const link = document.createElement('link');
link.rel = 'prerender';
link.href = document.querySelector('a').href;
document.head.appendChild(link);
```
