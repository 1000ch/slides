---
marp: true
title: 昨今の Web アプリの振る舞い
theme: default
paginate: true
footer: 昨今の Web アプリの振る舞い by [@1000ch](https://bento.me/1000ch)
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

# <!-- fit --> 昨今の Web アプリの振る舞い

---

![bg left:30% 60%](https://shogosensui.com/img/1000ch.avif)

# Shogo SENSUI ([shogosensui.com](https://shogosensui.com))

---

# 巷のソフトウェアプロダクトがどう動作しているか

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
- `<a>` / `<link>` / `<script>` 要素
- ブラウザグローバルの `fetch()` API や <s>`XMLHttpRequest`</s>

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

SSR と CSR はページロード時の話、MPA と SPA はランタイム時の話

| 行われている処理 | ページロード時 | ランタイム時 |
|---|---|---|
| サーバーが動的データを含む HTML を返却 | SSR | MPA |
| ブラウザが動的データを取得し HTML を更新 | CSR | SPA |

MPA は SSR を繰り返すデザインパターン、ページロード時に SPA を実装しているのが CSR、と言えるのではないか

---

<!-- _class: invert -->

# 昨今の UI ライブラリとフレームワーク

[jQuery](https://jquery.com/) から [Backbone.js](https://backbonejs.org/) を経て [React](https://ja.react.dev/), [Vue.js](https://ja.vuejs.org/), [Angular](https://angular.dev/) へ

---

# 古き良き Web から現代 Web への変遷

1. 静的な HTML ドキュメント配信とページ間リンクによる「WWW の誕生」
2. セッションの概念が誕生し「静的な Web から動的な Web への変化」
3. 非同期のデータ通信とページ更新による「Web フロントエンドのリッチ化」
4. 仮想 DOM の発明によるアーキテクチャの革命と「Web フロントエンドへの回帰」

---

# WWW の誕生

世界中のコンピュータを接続する「インターネット」と、HTTP を介して Web ページを公開する「WWW」によって、情報が民主化。

---

# 静的な Web から動的な Web への変化

HTML ファイルを公開する静的な Web から、サーバーで動作するプログラムを通じて HTML を生成する 動的な Web へ変化。セッションという概念が誕生し、Web ページが状態を持つように。

---

# Web フロントエンドのリッチ化

Google Maps に代表される、非同期のデータ通信とページ更新を駆使したインタラクティブな Web が誕生した (Ajax / DHTML の隆盛)。

Backend にあったロジックが Frontend にシフトし、アーキテクチャが求められるように。jQuery による DOM 操作から、Backbone.js をはじめとしたライブラリによる概念が導入。

---

# Web フロントエンドへの回帰

ライブラリによって各種デザインパターンがもたらされたが、DOM の更新コストと複雑性が立ちはだかる。仮想 DOM により「状態に応じて HTML を生成し、HTML の前後を比較し差分のみを更新」が実現。

昨今の Frontend で行われる「状態に応じて HTML を生成する」は Backend でやっていたことそのものであり、Frontend の責務が Backend を飲み込みながら拡大。

---

> 仮想 DOM により「状態に応じて HTML を生成し、HTML の前後を比較し差分のみを更新」

これを React/Vue.js 等で実装し「Node.js でホストして状態に応じた HTML を生成するのか」「ブラウザでデータを取得して HTML を更新するのか」といった方法論が先の SSR/CSR/MPA/SPA に帰着

<script type="module">
import mermaid from 'https://unpkg.com/mermaid@11/dist/mermaid.esm.min.mjs';
mermaid.initialize({startOnLoad: true});
</script>
