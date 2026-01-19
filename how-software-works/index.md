---
marp: true
title: ソフトウェアプロダクトの仕組み
theme: default
paginate: true
footer: ソフトウェアプロダクトの仕組み by [@1000ch](https://shogosensui.com)
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

# <!-- fit --> ソフトウェアプロダクトの仕組み

---

![bg left:30% 60%](https://shogosensui.com/img/1000ch.avif)

## Shogo SENSUI ([shogosensui.com](https://shogosensui.com))

> Web アプリケーション開発を専門とするソフトウェアエンジニア。企業で働く傍ら、様々な企業のエンジニアリングに顧問として関わり、高品質で維持しやすい Web アプリケーションを作るための活動を続けている。

---

<!-- _class: invert -->

# <!-- fit --> インターネットの爆発的な普及

---

# なぜインターネットが革命的だったのか

## インターネットがなかった時代のコンピュータ技術

- 人間と比較したときのコンピュータの優位性はデータの計算処理
- そのデータはアナログな方法💾💿で輸送する必要があった

## 世界中のコンピュータをネットワークで接続

- インターネットの本質はデータのコピー障壁の排除
- 世界中のデータが集まり、**情報の民主化が急速に進んだ**

---

# Disruptive Technology の存在

## [破壊的技術](https://ja.wikipedia.org/wiki/%E7%A0%B4%E5%A3%8A%E7%9A%84%E6%8A%80%E8%A1%93)がもたらす不可逆な変化

- 既存市場の価値基準を根底から覆し破壊する、革新的な技術
- 革新により代替された市場は、**縮小して戻らない**

## LLM は我々の手元にある破壊的技術の1つ

- マーケットフィットをしている最中なのが LLM やブロックチェーン
- 少し前だとモバイル通信やメディア配信、更に前だと PC や自動車など

---

<!-- _class: invert -->

# <!-- fit --> [Software is eating the world](https://a16z.com/why-software-is-eating-the-world/)

インターネットに接続されたコンピュータの世界で何が起こっているか

---

# コンピュータを構成するソフトウェアとハードウェア

## ハードウェア上でソフトウェアが動作する

- 端末はソフトウェアが搭載されていなければ、ただの機械
- ハードウェアを動作させる基本ソフトウェアとして OS

## ソフトウェアにも層があり、それ同士がやりとりする

- OS 上で動作する様々なソフトウェアが、いわゆるネイティブアプリケーション
- その1つにブラウザがあり、ブラウザ上で動作するのが Web アプリケーション

---

<!-- _header: コンピュータはソフトウェアとハードウェアで構成される -->

<div class="mermaid">
flowchart TB
subgraph hardware[ハードウェア]
  subgraph desktop[デスクトップ]
    cpu[CPU]
    harddisk[ハードディスク]
    display[ディスプレイ]
  end
  subgraph mobile[モバイル]
  end
end
subgraph software[ソフトウェア]
  subgraph os[オペレーティングシステム]
    windows[Windows]
    macos[macOS]
    linux[Linux]
    ios[iOS]
    android[Android]
  end
end
hardware <--> software
</div>

---

<!-- _header: ソフトウェアにも様々なレイヤが存在する -->

<div class="mermaid">
flowchart TB
subgraph software[ソフトウェア]
  subgraph os[オペレーティングシステム]
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
end
</div>

---

# アプリケーションの基本的な動作原理

## デバイス上で動作するアプリケーション

- デバイス上にホストされるソフトウェアが、ユーザーアクションに応答する
- URL にアクセスしたりストアからソフトウェアをダウンロードする

## それと疎通するクラウド上のシステム

- クラウド上にホストされるソフトウェアが、ネットワーク越しの要求に応答する

---

<!-- _header: 実際のソフトウェア動作を表現すると -->

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
  subgraph linux
    subgraph server[サーバー]
      system[システム]
      database[データベース]
    end
  end
end
iosapp <--> server
androidapp <--> server
webapp <--> server
system <--> database
</div>

---

<!-- _class: invert -->

# <!-- fit --> プロダクトを構成するもの

---

# プロダクトを成すソフトウェアと組織

## 様々な"システム"の捉え方

- 広義には「多くの物事や一連の働きを秩序立てた全体的なまとまり、体系」
- 狭義には「組織やそれを構成する制度」、更に狭くは「プロダクトのソフトウェア」

## プロダクトは価値提供を目的とした"システム"

- それはソフトウェアだけでなく組織的協調も含む
- ソフトウェアシステムがどう開発され、運用され、どう機能するか

---

<!-- _header: プロダクトの価値がデリバリーされるまでの例 -->

<div class="mermaid">
graph LR
subgraph product[プロダクト]
  subgraph product-development[プロダクト開発]
      plan-design[企画・デザイン]
      software-development[ソフトウェア実装]
      quality-assurance[品質担保]
  end
  subgraph product-operation[プロダクト運用]
      content-edit[コンテンツ制作]
      customer-success[問い合わせ対応]
  end
end
subgraph product-marketing[マーケティング]
  user-marketing[ユーザーマーケティング]
  client-marketing[クライアントマーケティング]
end
subgraph business-development[ビジネス開発]
  sales-plan[商品の企画]
  sales[商品の販売]
end
subgraph customer[カスタマー]
  user[ユーザー]
  client[クライアント]
end
product-development <--> product-operation
product <--> product-marketing
product-marketing <--> business-development
user-marketing --> user
client-marketing --> client
business-development --> client
</div>

---

# ミッションに向かって組織が一体となるために

## 組織は目的達成のために集まった集合体

- 営利企業であろうとコミュニティであろうと、組織であれば理は同じ
- 目的に付随する営みを理解することは、互いに信頼し協調するために必要不可欠

## 全知全能の人間は存在しない

- 理解や実践の範囲が広い程、目的に貢献する幅だけでなく質が高まる
- 優れた知識や専門性を持っていても、協調できなければ反乱因子

<script type="module">
import mermaid from 'https://unpkg.com/mermaid@11/dist/mermaid.esm.min.mjs';
mermaid.initialize({startOnLoad: true});
</script>
<script defer src="https://platform.x.com/widgets.js"></script>
