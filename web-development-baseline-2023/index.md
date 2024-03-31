---
marp: true
title: 2023 年の Web 開発のベースライン
theme: default
paginate: true
footer: 2023 年の Web 開発のベースライン by [@1000ch](https://bento.me/1000ch)
---

<!-- _class: invert -->

# <!-- fit --> 2023 年の Web 開発のベースライン

[TechFeed Experts Night #26](https://techfeed.io/events/techfeed-experts-night-26)

---

![bg left:30% 60%](https://shogosensui.com/img/1000ch.avif)

## Shogo SENSUI ([shogosensui.com](https://shogosensui.com))

SIer での受託開発を経て、2012 年に株式会社サイバーエージェントに入社。プロダクト開発の傍ら、エンジニア組織のマネジメントに従事。2018 年に株式会社メルカリに入社後は、[株式会社メルペイの Frontend チームの立ち上げ](https://engineering.mercari.com/blog/entry/20201222-merpay-frontend/)や [Web 版の「メルカリ」の刷新](https://engineering.mercari.com/blog/entry/20210810-the-new-mercari-web/)、[メルカリアプリのコードベース刷新](https://engineering.mercari.com/blog/entry/20221213-ground-up-app/)を牽引した後に、執行役員 VP of Engineering としてメルペイのエンジニアリング部門を管掌。2023 年 4 月にデジタル庁入庁。2023 年 7 月に株式会社ハウテレビジョン入社、執行役員プロダクト本部長に就任。[mond 認定回答者](https://mond.how/1000ch)、[TechFeed 公認エキスパート](https://techfeed.io/people/@1000ch) (Web 標準技術 • JavaScript)。

---

# 🤔

- 変化し続けてきた Frontend 領域の、背景と現在地を整理する
- Web 標準技術とブラウザ事情? 進化を支えるエコシステム? 設計のパラダイム?
- Web ページに向き合う開発者として、これからのスキルマップを思考する

---

<!-- _class: invert -->

# <!-- fit --> Web 標準技術とブラウザ

---

# IE11 サポート終了後のブラウザシェアの推移

<div id="desktop-browser-JP-monthly-202206-202305" style="margin: 0 auto; width: 600px; height: 400px;"></div>
<script defer src="https://www.statcounter.com/js/fusioncharts.js"></script>
<script defer src="https://gs.statcounter.com/chart.php?desktop-browser-JP-monthly-202206-202305&chartWidth=600"></script>

[IE11 の終了](https://blogs.windows.com/japan/2022/06/15/internet-explorer-11-is-no-longer-supported/)から早 1 年…ブラウザエンジンが Chromium 寡占になる懸念はありつつも、日本におけるモダンブラウザは定着したと言って良い ([StatCounter Global Stats](https://gs.statcounter.com/browser-market-share/desktop/japan/#monthly-202206-202305))。

---

# Interop による持続的な相互運用性の改善

<iframe loading="lazy" src="https://wpt.fyi/interop-2023" style="width: 100%; aspect-ratio: 3; border: 0;"></iframe>

[Web Standards Interop 2022](https://techfeed.io/entries/6298e525ed640020f3f19a58) でも触れた通り、Interop により Web 標準技術の相互運用性が持続的に改善されている。[Interop 2023](https://web.dev/interop-2023/) の焦点は [Container Queries](https://web.dev/cq-stable/) や Custom Properties の [`@property`](https://web.dev/at-property/) など。

---

# Open UI グループによる "Web の" UI 拡張

HTML 標準で提供されている UI は Web 黎明期にデザインされたもので、そのプラットフォームニュートラルな性質も相まって、長らく Web 開発者は UI の実装に苦労してきた。

[`<dialog>` 要素](https://caniuse.com/dialog)などの実用的な UI も追加されたが、より現代のユースケースに即した UI インキュベーションを行う [W3C の Open UI](https://open-ui.org/) によって、[`<selectlist>` 要素](https://open-ui.org/components/selectlist/)のような試験的な UI 要素が提案されている。

---

# Web 標準技術のボトムアップと漸進

## モダンブラウザの一般化と Interop が意味するところ

ブラウザエンジンが複数種類存在する限りブラウザ間の差はなくならないが、IE11 を中心とした後方互換性の考慮は大きく削減された。Interop によるモダンブラウザ間の相互運用性の向上も、Web アプリケーション実装のベースラインを大幅に前進させている。

## 各プロダクトによる試験的な Web 標準技術への貢献

[Figma の性能](https://www.figma.com/blog/webassembly-cut-figmas-load-time-by-3x/)や [Squoosh のコーデック](https://github.com/GoogleChromeLabs/squoosh/tree/dev/codecs)は WASM で実現していたり、[Astro v3 の View Transition API サポート](https://astro.build/blog/astro-3/)など、プロダクトによって優れた技術の導入も進んでいる。

---

<!-- _class: invert -->

# <!-- fit --> エコシステムと開発者体験

---

![bg vertical right:30%](https://upload.wikimedia.org/wikipedia/commons/thumb/d/d9/Node.js_logo.svg/1200px-Node.js_logo.svg.png)
![bg](https://upload.wikimedia.org/wikipedia/commons/e/e8/Deno_2021.svg)
![bg](https://blog.cloudflare.com/content/images/2019/06/45DEDC7B-B31F-461C-B786-12FBAF1A5391.png)
![bg](https://user-images.githubusercontent.com/709451/182802334-d9c42afe-f35d-4a7b-86ea-9985f73f20c3.png)

# JavaScript Runtime の群雄割拠

[Node.js](https://nodejs.org/) のエコシステムは、今や Web 開発に無くてはならない存在になった。[Deno](https://deno.com) や [Bun](https://bun.sh/) といった実行環境や [Cloudflare Workers](https://developers.cloudflare.com/workers/) のようなサービスも新たに登場し、[JavaScript Runtime の相互運用性の改善を目指す WinterCG](https://wintercg.org/) が組成された。

---

![bg vertical right:30%](https://upload.wikimedia.org/wikipedia/commons/thumb/0/02/Babel_Logo.svg/1200px-Babel_Logo.svg.png)
![bg](https://upload.wikimedia.org/wikipedia/commons/thumb/4/4c/Typescript_logo_2020.svg/1200px-Typescript_logo_2020.svg.png)
![bg](https://github.com/evanw/esbuild/raw/main/images/wordmark-light.svg)
![bg](https://raw.githubusercontent.com/biomejs/resources/main/biome-logo-slogan.svg)

# 開発におけるビルドの一般化

JavaScript の実装は [Babel](https://babeljs.io/) や [TypeScript](https://www.typescriptlang.org/) によるトランスパイルが一般化した。実行環境は Node.js に留まらず、実行速度の向上を目指して Go/Rust で実装された [esbuild](https://esbuild.github.io/) や [swc](https://github.com/swc-project/swc)、[Biome](https://biomejs.dev/) などのツールチェインが登場した。

---

# Node.js や React が Web 開発に与えた影響

## TypeScript および型付テンプレートとしての TSX

[Facebook ですら JSX が市民権を得ると思わなかった](https://www.youtube.com/watch?v=8pDqJVdNa44)が、[TypeScript の JSX サポート](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-1-6.html#jsx-support)や [VS Code といったエディタの TypeScript サポート](https://code.visualstudio.com/docs/languages/typescript)など、**[Language Server Protocol](https://microsoft.github.io/language-server-protocol/) 実装がある型付きテンプレートエンジン** として、品質と生産性の向上に寄与している。

## 開発者体験へフォーカスするプラットフォーム

[Next.js on Vercel](https://vercel.com/solutions/nextjs) や [Remix on Cloudflare](https://developers.cloudflare.com/pages/framework-guides/deploy-a-remix-site/) といった、アーキテクチャだけでなくデプロイ環境といった開発者体験を統合的にサポートするフレームワークとプラットフォームの組み合わせが登場している。

---

<!-- _class: invert -->

# <!-- fit --> アプリケーションアーキテクチャ
---

# Virtual DOM がもたらしたパラダイムシフト

## 差分描画と単一方向のデータフロー

Virtual DOM が実現する HTML の差分描画はアプリケーションの状態に応じたページの高速な再描画を実現し、昨今の UI ライブラリの多くはこの概念を踏襲している。これは[単一方向のデータフロー設計である Flux](https://www.youtube.com/watch?v=nYkdrAPrdcw) を一般化させた。

## CSR or SSR? SPA or MPA?

アプリケーションの要件に応じたアーキテクチャの試行錯誤が繰り返され、概念が成熟していく。[Universal JavaScript](https://en.wikipedia.org/wiki/Isomorphic_JavaScript) や [Jamstack](https://jamstack.org/) などのパラダイムが発明された。MPA への揺り戻しを[ブラウザ実装の最適化である bfcache](https://web.dev/bfcache/) が後押しする。

---

# 広がり続ける Frontend の責務

サーバーサイドエンジニアが Backend を実装してマークアップエンジニアが HTML/CSS を実装する時代から、Node.js が成すエコシステムの普及と成熟によって Software Engineer (Frontend) が Web アプリケーション全域をカバーしつつある。

<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">.<a href="https://twitter.com/1000ch?ref_src=twsrc%5Etfw">@1000ch</a> さんの「フロントエンドの責務が広がってバックエンドを飲み込んでいる」という話があって、これは結構象徴的だなと思いました。たとえばフロントエンドエンジニア向けのミートアップでCDNが話の中心になるというのは隔世の感があります。 <a href="https://twitter.com/hashtag/%E9%AB%98%E9%80%9F%E5%8C%96_findy?src=hash&amp;ref_src=twsrc%5Etfw">#高速化_findy</a></p>&mdash; FUJI Goro (@__gfx__) <a href="https://twitter.com/__gfx__/status/1638497684708552705?ref_src=twsrc%5Etfw">March 22, 2023</a></blockquote>

---

<!-- _class: invert -->

# <!-- fit --> ベースラインをどこに置くべきか

---

# 堅牢な UI の実装技術

セマンティックで HTML を使いつつ、[@layer](https://developer.mozilla.org/ja/docs/Web/CSS/@layer)/[@container](https://developer.mozilla.org/en-US/docs/Web/CSS/@container) クエリ, [`:has()`](https://developer.mozilla.org/ja/docs/Web/CSS/:has), [CSS Nesting](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_nesting/Using_CSS_nesting) など CSS の新機能を抑えていく。<u>**[Sass](https://sass-lang.com/) や [Autoprefixer](https://github.com/postcss/autoprefixer) は役目を終えつつある**</u>。

# プログラミング言語

JavaScript は [ES2015](https://kangax.github.io/compat-table/es6/) をベースにしつつ、実利と投資を含めて <u>**[ES2016+](https://kangax.github.io/compat-table/es2016plus/) を前提にして差し支えない**</u>。TypeScript も積極的に導入し、target も同様に ES2015+ で問題ない。

---

# 実行環境やアーキテクチャ

Node.js とそのエコシステムは Web 開発にとって今や欠かせない。要件に応じて UI ライブラリとビルドツールを選びながら、ベストプラクティスを模索していく。

# 拡がる Frontend のスキルマップ

[Frontend Developer Roadmap](https://roadmap.sh/frontend) を参考に、<u>**Software Engineer (Frontend) としての分化する専門性を磨いていく**</u>。

<script type="module">
import mermaid from 'https://unpkg.com/mermaid@10/dist/mermaid.esm.min.mjs';
mermaid.initialize({startOnLoad: true});
</script>
<script defer src="https://platform.x.com/widgets.js"></script>
