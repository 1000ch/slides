---
marp: true
theme: default
paginate: true
footer: Web Components Updates 2017 by [Shogo SENSUI](https://bento.me/1000ch)
---

<!-- _class: invert -->

# <!-- fit --> Web Components Updates 2017

2017.11.15 [html_modules_study](https://web-study.connpass.com/event/70731/)

---

![bg left:30% 60%](https://shogosensui.com/img/1000ch.avif)

# @1000ch

> Web アプリケーション開発を専門とするソフトウェアエンジニア。企業で働く傍ら、技術顧問として複数企業のエンジニアリングに関わり、高品質で維持しやすい Web アプリケーションを作るための活動を続けている。

[超速本](https://www.amazon.co.jp/dp/477419400X) をよろしくおねがいします📕🙏

---

# これから入るかもしれない仕様

- [Void or Self-closing Elements](#4)
- [HTMLSlotElement#assignedElements()](#9)
- [Custom Psuedo-elements](#13)
- [CSS Shadow Parts](#15)
- [HTML Modules](#17)
- [HTML Template Instantiation](#20)
- [`<link rel="modulepreload">`](#23)

※2017年11月現在、議論中の実験的な仕様です

---

# Void or Self-closing Elements

カスタム要素で `/` の省略やセルフクロージングをできるようにする

- [Custom 'void' or self-closing elements #624](https://github.com/w3c/webcomponents/issues/624)
- [Make the HTML parser put audio/video/source/iframe/canvas-in-svg into the HTML namespace #919](https://github.com/whatwg/html/issues/919#issuecomment-276329905)

---

## カスタム要素で終了タグが必須な件

```html
<!-- まぁわかる -->
<fancy-button>fancy button</fancy-button>

<!-- だがてめーは（ry -->
<fancy-input></fancy-input>

<!-- できればこう書きたい -->
<fancy-input />

<!-- あるいはこう書きたい -->
<fancy-input>
```

---

## `/` の省略やセルフクロージングの意義

`<input>` や `<img>` のように独立して意味を成すカスタム要素があるかもしれない

---

## カスタム要素の長さに応じて冗長になる記述

`<the-most-important-element><the-most-important-element>` は `<the-most-important-element />` と書けても良さそう

---

## 各所での議論

- **HTML Parser の挙動を変えるのは危険が伴う**
- カスタム要素名の制約にハイフン付きがあるなら大丈夫かも？
- TPAC 2017 でどういう話になったのか気になる…

---

# `assignedElements()`

`<slot>` 要素に挿入された要素を参照する

- [Add assignedElements() method to <slot> #2269](https://github.com/whatwg/html/pull/2269)

---

## 挿入された要素を Shadow DOM 内部で参照したい

```html
<fancy-button>
  <the-icon></the-icon>
  Fancy Button
</fancy-button>
```

`<the-icon>` と `Fancy Button` が `<fancy-button>` のデフォルトスロットに挿入される

---

## `HTMLSlotElement#assignedNodes()` は？

```javascript
const button = document.querySelector('fancy-button');
const slot = button.shadowRoot.querySelector('slot');

// 要素だけでなくテキストノードも返る
console.log(slot.assignedNodes());
```

---

## `HTMLElement` だけ取得したい === `assignedElements()`

```javascript
HTMLSlotElement.prototype.assignedElements = function() {
  const nodes = this.assignedNodes();
  const elements = nodes.filter(function (node) {
    return node.nodeType === Node.ELEMENT_NODE;
  });

  return elements;
};
```

---

# Custom Psuedo-elements

Shadow DOM 内の要素に任意の疑似セレクタを定義できるようにする

- [Custom Pseudo-Elements](https://github.com/w3c/webcomponents/blob/gh-pages/proposals/Custom-Pseudo-Elements.md)
- [Support Custom Pseudo-elements #300](https://github.com/w3c/webcomponents/issues/300)

---

## Custom Psuedo-elements のイメージ

```html
<date-range-selector>
  <!-- #shadow-root -->
    <input pseudo="start-date" type="date">
    <input pseudo="end-date" type="date">
  <!-- /shadow-root -->
</date-range-selector>
<style>
  date-range-selector::start-date,
  date-range-selector::end-date {
    color: red;
  }
</style>
```

_パーサーの振る舞いと相性が若干悪そうで、旗色が悪い？_

---

# CSS Shadow Parts

Shadow Host を `::part()` や `::theme()` で参照する CSS セレクタ。`/deep/` やら `::shadow` の登場によって削除された仕様だが、Custom Psuedo-elements によって復活？

- [CSS Shadow Parts](https://tabatkins.github.io/specs/css-shadow-parts/)
- [Shadow parts](https://www.w3.org/2017/11/10-webplat-minutes.html#item03)

---

## CSS Shadow Parts のイメージ

```html
<date-range-selector>
  <!-- #shadow-root -->
    <input part="start-date" type="date">
    <input part="end-date" type="date">
  <!-- /shadow-root -->
</date-range-selector>
<style>
  date-range-selector::part(start-date),
  date-range-selector::part(end-date) {
    color: red;
  }
</style>
```

---

# HTML Modules

ES Modules を拡張して HTML ファイルをロードできるようにする

- [HTML Modules #645](https://github.com/w3c/webcomponents/issues/645)
- [HTML Import replacement](https://www.w3.org/2017/11/10-webplat-minutes.html#item06) - WebPlat Web Components TPAC
- [Untrusted 3rd Party Web Components](https://gist.github.com/justinfagnani/fea819776d77eee5a108a3bcf873e7f4)

---

## HTML Modules のイメージ

```html
<!-- bar.html -->
<template>
  <div>Display!</div>
</template>

<!-- app.js -->
<script type="module">
  import bar from './bar.html';
  const template = bar.querySelector('template');
</script>
```

---

## HTML Modules 所感（個人の感想です）

- `import/export` で HTML をロードしていいのか
  - `as` によるキャスト前提なら大きな違和感はない
  - ECMAScript に足を踏み入れると広げた風呂敷が（ry
- `<script type="module" src=".html"></script>` で HTML パーサー上のみで動いたほうがしっくり来る
  - 一周回って HTML Imports の方が良い気もしてくる🤔
- **とにかく宣言的に Web Components を使いたい**

---

# HTML Template Instantiation

`template` 要素に mustache の文法を取り込んで、テンプレートとしての機能を拡充する

- [HTML Template Instantiation](https://github.com/w3c/webcomponents/blob/gh-pages/proposals/Template-Instantiation.md)
- [domenic/template-parts](https://github.com/domenic/template-parts)

---

## HTML Template Instantiation

```html
<template id="tmpl">
  <h1>{{name}}</h1>
  <a href="mailto:{{email}}">{{email}}</a>
</template>
<script>
  document.querySelector('#tmpl').createInstance({
    name: 'Shogo Sensui',
    email: 'shogosensui@gmail.com'
  }).update({
    name: '1000ch',
    email: 'shogosensui+1000ch@gmail.com'
  });
</script>
```

---

## type (processor) の定義

```html
<template type="tmpl-type">
  <h1>{{name}}</h1>
</template>
<script>
  document.defineTemplateType('tmpl-type', {
    processCallback: (instance, parts, state) => {
      for (const part of parts) {
        part.value = state[part.expression];
      }
    }
  });
</script>
```

---

# `<link rel="modulepreload">`

ES Modules な JavaScript ファイルを先読みする

- [Preload and Modules](https://docs.google.com/document/d/1WebH4IOCswACUbaczx5cGQPVl5mnqcieOd4MRJM2syk/edit?usp=sharing)
- [preload, destinations, and module scripts #486](https://github.com/whatwg/fetch/issues/486#issuecomment-282044172)

---

## 依存関係が深いとロードが遅くなる問題

<blockquote class="twitter-tweet" data-lang="ja"><p lang="ja" dir="ltr">モジュール数100以上 or 深さが5以上ならbundleした方がいいとのこと  &quot;Loading Performance with (Many) Modules: Summary as of Oct 7, 2017 - Go…&quot; <a href="https://t.co/8gZZBbejMn">https://t.co/8gZZBbejMn</a></p>&mdash; azu (@azu_re) <a href="https://twitter.com/azu_re/status/918675534632042496?ref_src=twsrc%5Etfw">2017年10月13日</a></blockquote>

---

## `rel="modulepreload"` の使い方

```html
<link rel="modulepreload" href="app.js">
<link rel="modulepreload" href="helpers.js">
<link rel="modulepreload" href="irc.js">
<link rel="modulepreload" href="fog-machine.js">

<script type="module" src="app.js"></script>
```

---

## `rel="preload"` と `as="module"` はダメ？

- `script` 要素の credential と一致している必要がある
- 事前に module なのかどうかわかっていないとパースに困る (v8?)
- `<link rel="preload">` は単一リソースをロードする仕様
- 保存先が preload cache ではなく module map である必要がある (chrome?)

---

<!--- _class: invert -->

# おしまい
