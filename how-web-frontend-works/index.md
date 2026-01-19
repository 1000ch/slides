---
marp: true
title: 昨今の Web アプリ事情
theme: default
paginate: true
footer: 昨今の Web アプリ事情 by [@1000ch](https://shogosensui.com)
style: |
  section:has(> .mermaid) {
    padding-top: 0;
    padding-bottom: 0;
  }
  .mermaid {
    display: flex;
    justify-content: center;
  }
---

<!-- _class: invert -->

# <!-- fit --> 昨今の Web アプリ事情

---

![bg left:30% 60%](https://shogosensui.com/img/1000ch.avif)

# Shogo SENSUI ([shogosensui.com](https://shogosensui.com))

---

# 巷のソフトウェアプロダクトの振る舞い

---

<!-- _header: ソフトウェアプロダクトのシステムとしての振る舞い -->

<div class="mermaid">
flowchart LR
subgraph client-side[クライアントサイド]
  subgraph ios[iOS]
    iosapp[iOS アプリ]
  end
  subgraph android[Android]
    androidapp[Android アプリ]
  end
  subgraph web[Web]
    subgraph browser[ブラウザ]
      webapp[Web アプリ]
    end
  end
end
subgraph server-side[サーバーサイド]
  subgraph Linux
    system[システム]
    database[データベース]
  end
end
iosapp <--> system
androidapp <--> system
webapp <--> system
system <--> database
</div>

---

<!-- _header: Web アプリケーションにフォーカス -->

<div class="mermaid">
flowchart LR
subgraph browser[ブラウザ]
  webapp[Web アプリ]
end
subgraph server[サーバー]
  system[システム]
  database[データベース]
end
webapp --HTTP リクエスト--> system
system <--> database
system --HTTP レスポンス--> webapp
</div>

---

# ブラウザとサーバーのやりとり

## ブラウザで表示する Web ページが HTTP リクエストを送る

- アドレスバーの URL ナビゲーション
- [`<a>`](https://html.spec.whatwg.org/multipage/text-level-semantics.html#the-a-element) / [`<link>`](https://html.spec.whatwg.org/multipage/semantics.html#the-link-element) / [`<script>`](https://html.spec.whatwg.org/multipage/scripting.html#the-script-element) / [`<iframe>`](https://html.spec.whatwg.org/multipage/iframe-embed-object.html#the-iframe-element) 要素
- ブラウザグローバルの [`fetch()`](https://developer.mozilla.org/ja/docs/Web/API/Fetch_API) 関数や <s>[`XMLHttpRequest`](https://developer.mozilla.org/ja/docs/Web/API/XMLHttpRequest)</s>

## それを受け取ったサーバーが HTTP レスポンスを返す

- HTML / CSS / JavaScript / 画像などの静的ファイル
- API エンドポイントが返す JSON などの動的データ

---

<!-- _class: invert -->

# SSR と CSR、MPA と SPA

巷で耳にするこれらのキーワードの理解を整理する

---

# SSR: Server-Side Rendering

ブラウザの URL ナビゲーション時に、サーバーが動的なデータを含む HTML を返す

---

<!-- _header: サーバーが動的なデータを取得し、完全版 HTML を生成して返す SSR -->

<div class="mermaid">
sequenceDiagram
participant Browser
participant Server
participant Database
Browser->>Server: URL Navigation
Server<<->>Database: Data Query
Note left of Database: SQL Execution
Server-->>Browser: Complete HTML
loop
  Browser->>Browser: HTML Parse
  Note right of Browser: HTML Patch by UI Library
end
</div>

---

# CSR: Client-Side Rendering

ブラウザがサーバーから動的なデータを非同期で取得し、ブラウザが HTML を作る

---

<!-- _header: ブラウザが動的なデータを取得し HTML を更新する CSR -->

<div class="mermaid">
sequenceDiagram
participant Browser
participant Server
participant Database
Browser->>Server: URL Navigation
Server-->>Browser: Skelton HTML
loop
  Browser->>Browser: HTML Parse
end
Browser->>Server: API Request
Server<<->>Database: Data Query
Note left of Database: SQL Execution
Server-->>Browser: API Response
loop
  Browser->>Browser: HTML Render
  Note right of Browser: HTML Patch by UI Library
end
</div>

---

# MPA: Multi-Page Application

サーバーから配信される複数の HTML ページをブラウザが取得し、URL ナビゲーションを介してページ遷移する

---

<!-- _header: サーバーから配信される複数の HTML ページをブラウザが取得する -->

<div class="mermaid">
sequenceDiagram
participant Browser
participant Server
participant Database
Browser->>Server: URL Navigation
Server<<->>Database: Data Query
Note left of Database: SQL Execution
Server-->>Browser: Complete HTML
loop
  Browser->>Browser: HTML Parse
end
</div>

---

# [SPA](https://developer.mozilla.org/ja/docs/Glossary/SPA): Single-Page Application

単一の HTML ページを基に、ブラウザが動的にデータを取得して HTML を更新し、URL ナビゲーションを介さずページ遷移する

---

<!-- _header: ブラウザで動的なデータを取得し HTML を更新してページ遷移する -->

<div class="mermaid">
sequenceDiagram
participant Browser
participant Server
participant Database
loop
  Browser->>Browser: Navigation
end
Browser->>Server: API Request
Server<<->>Database: Data Query
Note left of Database: SQL Execution
Server-->>Browser: API Response
loop
  Browser->>Browser: HTML Render
  Note right of Browser: HTML Patch by UI Library
end
</div>

---

# 語弊を恐れながら整理した表

| 行われている処理 | ページロード時 | ランタイム時 |
|---|---|---|
| サーバーが動的データを含む HTML を返却 | SSR | MPA |
| ブラウザが動的データを取得し HTML を更新 | CSR | SPA |

SSR と CSR はページロード時、MPA と SPA はランタイム時の話であり、MPA は SSR を繰り返すデザインパターン、ページロード時に SPA を実装しているのが CSR、と言えるのではないか。

---

<!-- _class: invert -->

# 昨今の UI ライブラリとフレームワーク

[jQuery](https://jquery.com/) から [Backbone.js](https://backbonejs.org/) を経て [React](https://ja.react.dev/), [Vue.js](https://ja.vuejs.org/), [Angular](https://angular.dev/) へ

---

# 古き良き Web から現代 Web への変遷

1. 静的な HTML ドキュメント配信とページ間リンクによる「WWW の誕生」
2. セッションの概念が誕生し「静的な Web から動的な Web への変化」
3. 非同期のデータ通信とページ更新による「Web のリッチ化と領域確立」
4. 仮想 DOM の発明によるアーキテクチャの革命と「Backend に回帰する Frontend」


---

# WWW の誕生

世界中のコンピュータを接続する「インターネット」と、HTTP を介して Web ページを公開する「WWW」によって、情報が民主化。

---

[ASCII.jp：あの「愛生会病院」のサイトが、ついに閉鎖](https://ascii.jp/elem/000/000/804/804010/)

![bg right:50%](https://ascii.jp/img/2013/07/01/366120/l/8b33f8fc1f1772a0.jpg)

---

# 静的な Web から動的な Web への変化

HTML ファイルを公開する静的な Web から、サーバーで動作するプログラムを通じて HTML を生成する 動的な Web へ変化。セッションという概念が誕生し、Web ページが状態を持つように。

---

# Web のリッチ化と領域確立

Google Maps に代表される、非同期のデータ通信とページ更新を駆使したインタラクティブな Web が発明され、急速にリッチ化が進んだ (Ajax / DHTML の隆盛)。

Backend にあったロジックが Frontend にシフトし、アーキテクチャが求められるように。jQuery による DOM 操作から、Backbone.js をはじめとしたライブラリによる概念が導入。

---

# Backend に回帰する Frontend

ライブラリによって各種デザインパターンがもたらされたが、DOM の更新コストと複雑性が立ちはだかる。[仮想 DOM](https://zenn.dev/mizchi/books/0c55c230f5cc754c38b9) により「状態に応じた HTML 生成と、HTML の前後比較による差分更新」が実現。

昨今の Frontend で平然と実行される「状態に応じて HTML を生成する」は、旧来の Backend でやっていたことそのものであり、Backend から切り出された Frontend の責務が広がり、今度は Backend に侵食。

---

<!-- _class: invert -->

# Web フロントエンドを取り巻く技術

React/Vue.js, TypeScript, Next/Nuxt, Vite/Biome, etc.

---

# 取り巻く技術が実現していること

> 仮想 DOM により「状態に応じて HTML を生成し、HTML の前後を比較し差分のみを更新」

React/Vue.js といった昨今の UI ライブラリは、これらをハイレベルに抽象化し、「コンポーネント化」や「TypeScript 対応」といった開発者体験と共に提供している。

その上で、「Node.js でホストするのか」「ブラウザでデータを取得して HTML を更新するのか」といった方法論が発生し、先の SSR/CSR/MPA/SPA に帰着。

---

## ランタイム: JavaScript の実行環境

- [Chromium](https://www.chromium.org/)/[V8](https://v8.dev/): Chrome や Brave などのベース
- [Gecko](https://developer.mozilla.org/ja/docs/Glossary/Gecko)/[SpiderMonkey](https://spidermonkey.dev/): Firefox のベース
- [WebKit](https://webkit.org/)/[JavaScriptCore](https://developer.apple.com/documentation/javascriptcore): Safari のベース
- [Node.js](https://nodejs.org/): V8 ベース
- [Deno](https://deno.com/): V8 ベースで TypeScript をサポート
- [Bun](https://bun.sh/): JavaScriptCore ベース
- [Cloudflare Workers](https://www.cloudflare.com/ja-jp/developer-platform/products/workers/): V8 ベースのエッジ環境

![bg vertical right:30%](https://upload.wikimedia.org/wikipedia/commons/2/28/Chromium_Logo.svg)
![bg vertical right:30%](https://upload.wikimedia.org/wikipedia/commons/thumb/d/d9/Node.js_logo.svg/1200px-Node.js_logo.svg.png)
![bg vertical right:30%](https://upload.wikimedia.org/wikipedia/commons/e/e8/Deno_2021.svg)
![bg vertical right:30%](https://blog.cloudflare.com/content/images/2019/06/45DEDC7B-B31F-461C-B786-12FBAF1A5391.png)
![bg vertical right:30%](https://user-images.githubusercontent.com/709451/182802334-d9c42afe-f35d-4a7b-86ea-9985f73f20c3.png)

---

## UI ライブラリ: 仮想 DOM を内蔵し View を効率よく更新

- [React](https://ja.react.dev/): Facebook 謹製の VDOM 内蔵 UI ライブラリ
- [Vue.js](https://ja.vuejs.org/): 同じく VDOM 内蔵の UI ライブラリ
- [Preact](https://preactjs.com/): React 互換の軽量実装

## フレームワーク: 開発上の作法を提供

- [Next](https://nextjs.org/): React を前提としたフレームワーク
- [Nuxt](https://nuxt.com/): Vue.js を前提としたフレームワーク

![bg vertical right:30%](https://upload.wikimedia.org/wikipedia/commons/thumb/a/a7/React-icon.svg/1024px-React-icon.svg.png)
![bg vertical right:30%](https://upload.wikimedia.org/wikipedia/commons/9/95/Vue.js_Logo_2.svg)
![bg vertical right:30%](https://raw.githubusercontent.com/preactjs/preact/8b0bcc927995c188eca83cba30fbc83491cc0b2f/logo.svg?sanitize=true)
![bg vertical right:30%](https://upload.wikimedia.org/wikipedia/commons/8/8e/Nextjs-logo.svg)
![bg vertical right:30%](https://v2.nuxt.com/design-kit/colored-text.svg)

---

## トランスパイラ: プログラムを動作上の互換性を保ち変換

- [TypeScript](https://www.typescriptlang.org/ja/): JavaScript のスーパーセット言語
- [esbuild](https://esbuild.github.io/): TS/JS のトランスパイラ兼バンドラ
- [SWC](https://swc.rs/): TS/JS のトランスパイラ兼バンドラ

![bg vertical right:30%](https://upload.wikimedia.org/wikipedia/commons/thumb/4/4c/Typescript_logo_2020.svg/1200px-Typescript_logo_2020.svg.png)
![bg vertical right:30%](https://github.com/evanw/esbuild/raw/main/images/wordmark-light.svg)
![bg vertical right:30%](https://swc.rs/logo.png)
![bg vertical right:30%](https://ja.vite.dev/logo.svg)
![bg vertical right:30%](https://rollupjs.org/twitter-card.jpg)

## バンドラ: リソースの依存関係を解決

- [Vite](https://ja.vite.dev/): esbuild 内蔵のビルドツール
- [Rollup](https://rollupjs.org/): Web 標準の ESM に準拠するバンドラ
- [Webpack](https://webpack.js.org/)

---

<!-- _class: invert -->

# 要件に相応しく持続可能な技術選定を目指して

- システムの振る舞いと Web アプリの変遷についての基礎理解
- Web フロントエンドの比重が著しく肥大化し、周辺技術が発達
- 巷でよく聞く Web 技術や実行環境それぞれの役割や位置づけ

<script type="module">
import mermaid from 'https://unpkg.com/mermaid@11/dist/mermaid.esm.min.mjs';
mermaid.initialize({startOnLoad: true});
</script>
