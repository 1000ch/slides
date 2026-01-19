---
marp: true
math: mathjax
title: 開発生産性と組織
theme: default
paginate: true
footer: 開発生産性と組織 by [@1000ch](https://shogosensui.com)
---

<!-- _class: invert -->

# <!-- fit --> 開発生産性と組織

[フロントエンドの開発生産性〜Online Conference〜](https://findy.connpass.com/event/294482/)

---

![bg left:30% 60%](https://shogosensui.com/img/1000ch.avif)

## Shogo SENSUI ([shogosensui.com](https://shogosensui.com))

> Web アプリケーション開発を専門とするソフトウェアエンジニア。企業で働く傍ら、様々な企業のエンジニアリングに顧問として関わり、高品質で維持しやすい Web アプリケーションを作るための活動を続けている。

---

[![w:240](https://m.media-amazon.com/images/I/51XoTDOKNCL._SY346_.jpg)](https://www.amazon.co.jp/dp/B0142S78BO?tag=1000ch-22) [![w:240](https://m.media-amazon.com/images/I/51qIstIPvFL._SY346_.jpg)](https://www.amazon.co.jp/dp/B00BN16XX8?tag=1000ch-22) [![w:240](https://m.media-amazon.com/images/I/51JxJVl5YXL._SY346_.jpg)](https://www.amazon.co.jp/dp/B09MS8BML8) [![w:240](https://m.media-amazon.com/images/I/513kY6L-3yL._SY346_.jpg)](https://www.amazon.co.jp/dp/B079TLW41L?tag=1000ch-22) [![w:240](https://m.media-amazon.com/images/I/415i2B4p4mL.jpg)](https://www.amazon.co.jp/dp/B09MHRWJKN?tag=1000ch-22) [![w:240](https://m.media-amazon.com/images/I/41SlY0zvpKL._SX350_BO1,204,203,200_.jpg)](https://www.amazon.co.jp/dp/4873116309?tag=1000ch-22) [![w:240](https://m.media-amazon.com/images/I/51lusOSU33L.jpg)](https://www.amazon.co.jp/dp/B00OJVMK5O?tag=1000ch-22) [![w:240](https://m.media-amazon.com/images/I/51TuqLnPBCL.jpg)](https://www.amazon.co.jp/dp/B07L2R3LTN?tag=1000ch-22)

---

# 🤔

- 私達を取り巻く組織（会社、チーム、コミュニティ、etc）とは一体何なのか
- 我々の職能にとって重要なテーマである開発生産性に、組織がどう影響するのか
- Frontend という切り口でそれらを俯瞰したときの要因分析と課題設定

---

# 開発生産性とは？

[経済学における労働生産性](https://ja.wikipedia.org/wiki/%E7%94%9F%E7%94%A3%E6%80%A7)は $\frac{産出量}{投入量}$なので、ソフトウェアを生産するということは

$$
開発生産性 = \frac{ソフトウェアの生産量}{投資した開発リソース}
$$

ソフトウェア開発の現場は必ずしも営利事業を営む会社ではないが、**「ソフトウェアを生産する」ために「開発リソースを投資する」** が原理として根底にある。

---

# 組織とは？

> 生物学における組織とは、形態及び機能を同じくする細胞の集合体。via [組織 (生物学) Wikipedia](https://ja.wikipedia.org/wiki/%E7%B5%84%E7%B9%94_(%E7%94%9F%E7%89%A9%E5%AD%A6))

> 社会科学における組織は、共通の目標を有し、目標達成のために協働を行う、何らかの手段で統制された複数の人々の行為やコミュニケーションによって構成されるシステムのことである。via [組織 (社会科学) Wikipedia](https://ja.wikipedia.org/wiki/%E7%B5%84%E7%B9%94_(%E7%A4%BE%E4%BC%9A%E7%A7%91%E5%AD%A6))

> **ある目的を達成するために、分化した役割を持つ個人や下位集団から構成される集団。** _via 広辞苑_

---

<!-- _header: 良い組織は良い生産性を体現する -->

# 開発生産性と組織の関係

$$
開発生産性 = 組織 \ast \frac{生産されたソフトウェア量}{投資した開発リソース}
$$

**「モノづくりに関わる人」と「個々の能力や技術力」の掛け算** だけでなく、組織はシステムとして開発リソースという資源を統率管理する。

---

# よくある組織の営み

<div class="mermaid">
graph TD
A(報酬) --> |対価としての報酬が動機になる| B
B(労働) --> |成果や自己実現のために挑戦する| C
C(評価) --> |評価と称賛により承認される| A
</div>

組織は大きい単位では会社かもしれないし、小さい単位ではチームかもしれない。サイズの大小はあれど、集合体であれば端的には組織。労働の対価として金銭を得る場合もあれば自己実現のためにボランティアとして奉仕する場合もあり、動機は色々。

---

<!-- _class: invert -->

# <!-- fit --> 動機は行動の源泉

組織と個人、双方の期待値ベクトルを揃える

---

# 組織の期待値

## 組織の目標に対する、報酬に見合った貢献

組織に説明責任があり、個人に遂行責任がある。これらを接続するのがマネジメントの仕事であり、レポートラインにおけるピープルマネジメントやプロジェクトにおけるプロジェクトマネジメント。

---

# 個人の期待値

## 組織の目標に対する、貢献に見合った報酬

目標設定は双方の期待値を擦り合わせるプロセス、期待値と現状のギャップを埋めるのが組織のマネジメントと各自の努力。

## 組織の営みを通じた自己実現や承認

多面的で人それぞれ。金銭的報酬（≒生理的欲求・安全の欲求）だけではなく、組織内外の協調（≒社会的欲求・承認欲求）や、内発的動機の実現（≒自己実現欲求）に及ぶ。

---

![bg right:30% 60%](https://m.media-amazon.com/images/I/519FUfDdTgL._SY291_BO1,204,203,200_QL40_ML2_.jpg)

# <!-- fit --> 納得は全てに優先する

**納得は動機の源泉** であり、「組織の期待値」と「個人の期待値」の一致の度合いが働く上での納得に強く影響する。

---

<!-- _class: invert -->

# <!-- fit --> 組織統治の仕組み

仕組み＝事をうまく運ぶために工夫された計画・構造・機構

---

# ガバナンスの存在目的

## ガバナンスは体制

組織の所有者が組織行動を制御するためのシステムや体制。例えば、組織の制度やポリシーを定めて、管理で執行し、監査で妥当性を評価する。

## マネジメントは実行

ヒエラルキー型のように階級や役職などが存在する管理体制があれば、ホラクラシー型のように階層構造を設けない組織形態もある。

---

# 組織の統治機構

## 日本国や株式会社のガバナンス

日本国で言えば司法・立法・行政の三権を基底にした、複雑な制度や機構が機能している。株式会社なら、株主総会をはじめ多層化されたマネジメント、職務権限規定や就業規則といったルールやポリシーがある。

---

<!-- _class: invert -->

# <!-- fit --> Frontend の責務と納得

組織の期待値と、我々の納得と、あなたと私

---

# 広がり続ける Frontend の責務

サーバーサイドエンジニアが Backend を実装してマークアップエンジニアが HTML/CSS を実装する時代から、Node.js が成すエコシステムの普及と成熟によって Software Engineer (Frontend) が Web アプリケーション全域をカバーしつつある。

<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">.<a href="https://twitter.com/1000ch?ref_src=twsrc%5Etfw">@1000ch</a> さんの「フロントエンドの責務が広がってバックエンドを飲み込んでいる」という話があって、これは結構象徴的だなと思いました。たとえばフロントエンドエンジニア向けのミートアップでCDNが話の中心になるというのは隔世の感があります。 <a href="https://twitter.com/hashtag/%E9%AB%98%E9%80%9F%E5%8C%96_findy?src=hash&amp;ref_src=twsrc%5Etfw">#高速化_findy</a></p>&mdash; FUJI Goro (@__gfx__) <a href="https://twitter.com/__gfx__/status/1638497684708552705?ref_src=twsrc%5Etfw">March 22, 2023</a></blockquote>

---

<!-- _header: Frontend とは何なのか -->

> # ユーザーとサービスを UI で繋ぐために HTML 生成処理を整える技能領域
> AND/OR
> # システムとデザインの境界で責任を持ちユーザーに届ける品質を司る職能
> via [Webフロントエンドと アーキテクチャ事情の持論を喋る](https://speakerdeck.com/ahomu/webhurontoendoto-akitekutiyashi-qing-nochi-lun-wodie-ru) by @ahomu

---

# Frontend の納得はどこにあるか

## 組織の Frontend という領域への期待値

事業価値をユーザーに提供するために、ブラウザ上の UI を実現する HTML 生成を担う専門性を以て、デザインとシステムの境界の品質を担保すること。

## Frontend を取り巻く要因

開発現場では、変化し続ける Frontend の職務範囲、意思決定を含む開発プロセスにおける裁量、技術的挑戦の余地など。管理体制で言えば、従業員に対して認めるワークスタイル、エンジニアリングの評価、職域の組織内ヒエラルキーなど。

---

# モノづくりに於いて意思決定に手が届く

自分の意志が合意形成のプロセスに含まれ、専門領域内外で最適化を施す余地がある

<div class="mermaid">
journey
section Plan
  Feature Plan: 5: Product Management
  User Interface: 4: Design
section Development
  Development: 3: Frontend, Backend
  Test: 2: QA
  Release: 3: Frontend, Backend
section Evaluation
  User Feedback: 5: Product Management, QA
</div>

---

# その組織における承認

自らの専門性が組織で必要とされ、より[高次の欲求](https://ja.wikipedia.org/wiki/%E8%87%AA%E5%B7%B1%E5%AE%9F%E7%8F%BE%E7%90%86%E8%AB%96)に近づける

<div class="mermaid">
journey
section Expectation
  Company Mission: 5: Executive
  Team Direction: 4: Engineering Manager
  Goal Setting: 4: Software Engineer
section Daily Work
  Development: 3: Engineering Manager, Software Engineer
section Evaluation
  Look Back: 4: Software Engineer
  Feedback: 3: Engineering Manager
</div>

---

# 取り巻く要因と付随する課題例

## Frontend という責務への主体性

役割や職責は組織それぞれ、自己実現欲求の究極系があるとすればコミュニティや会社のためではなく自分のために開発すること。組織というコンテキストは制限を作る。

## 協調するにあたってのマインドセット

専門性によるポジショントークをしてはいけない。事業目標の達成に向けた課題を、異なる専門性をかけ合わせてどう解くのかが肝要

---

<!-- _class: invert -->

# <!-- fit --> Frontend としての問の在処を探そう

<script type="module">
import mermaid from 'https://unpkg.com/mermaid@11/dist/mermaid.esm.min.mjs';
mermaid.initialize({startOnLoad: true});
</script>
<script defer src="https://platform.x.com/widgets.js"></script>
