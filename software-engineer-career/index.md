---
marp: true
title: ソフトウェアエンジニアのキャリア
theme: default
paginate: true
footer: ソフトウェアエンジニアとしてのキャリア by [@1000ch](https://shogosensui.com)
---

<!-- _class: invert -->

# <!-- fit --> ソフトウェアエンジニアのキャリア

2023.05.22 [外資就活 Terminal](https://gaishishukatsu.com/lp/terminal)

---

![bg left:30% 60%](https://shogosensui.com/img/1000ch.avif)

## Shogo SENSUI ([shogosensui.com](https://shogosensui.com))

> Web アプリケーション開発を専門とするソフトウェアエンジニア。企業で働く傍ら、様々な企業のエンジニアリングに顧問として関わり、高品質で維持しやすい Web アプリケーションを作るための活動を続けている。

---

<!-- _class: invert -->

# <!-- fit --> ソフトウェアエンジニアとして働く環境

---

<!-- _header: ソフトウェアエンジニアとして働く環境 -->

# ソフトウェア開発を業務に含む環境は多種多様

- プロダクトを提供している[事業](https://ja.wikipedia.org/wiki/%E4%BA%8B%E6%A5%AD)会社や[受託](https://ja.wikipedia.org/wiki/%E5%8F%97%E8%A8%97)開発会社
- [各種法人](https://ja.wikipedia.org/wiki/%E6%B3%95%E4%BA%BA)に限らず、デジタル庁のような行政機関
- GitHub のようなプラットフォームでの活動やコミュニティという形も

---

# 環境への関わり方も多種多様

- どんな期待値を交わすか、多くの場合は「社員かどうか」に帰結
- 交わす契約の特徴を踏まえて、どういった役割を担うか
- あるいは契約を交わさない環境や状況もあり得る

---

<!-- _header: ソフトウェアエンジニアリングが活きる環境 -->

<div class="mermaid">
graph LR
  subgraph workstyles[働き方]
    internal[社員]
    individual[個人]
  end
  subgraph environments[環境]
    subgraph company[企業]
      commercial[営利企業]
      non-profit[非営利企業]
      administrative-agency[行政機関]
    end
    subgraph community[コミュニティ]
      study-meetup[勉強会]
      github[GitHub]
    end
  end
  workstyles <--> environments
</div>

---

<!-- _class: invert -->

# <!-- fit --> ソフトウェアエンジニアとしてのキャリアパス

---

<!-- _header: ソフトウェアエンジニアとしてのキャリアパス -->

# エンジニアリングを軸に近接する役割

- 専門性を以てソフトウェア開発に従事する Individual Contributor
- 高い専門性を以て技術的な意思決定を担う Tech Lead
- プレイヤーやリードを含む組織を束ねる Engineering Manager

---

<!-- _header: ソフトウェアエンジニアとしてのキャリアパス -->

# 分化し発展したことで確立された専門性

- Web/iOS/Android といったプラットフォーム技術
- サーバーで動作するシステムに焦点を当てた Backend/Site Reliability
- ソフトウェアの品質として Performance/Accessibility/Security
- 要件定義や意思決定のプロセスに近い ML Engineering/Data Engineering

---

<!-- _header: ソフトウェアエンジニアとしてのキャリアパス -->

<div class="mermaid">
graph TB
  subgraph swe[Software Engineering]
    subgraph roles[Roles]
      ic[Individual Contributor]
      tl[Technical Lead]
      em[Engineering Manager]
      ic <--> tl
      tl <--> em
      ic <--> em
    end
    subgraph expertise[Expertise]
      subgraph client[Client-side]
        frontend[Web Frontend]
        mobile[Mobile App]
      end
      subgraph server[Server-side]
        backend[Backend]
        sre[Site Reliability]
      end
      subgraph quality[Quality]
        performance[Performance]
        accessibility[Accessibility]
        security[Security]
        test[Test]
      end
      subgraph bi[Business Intelligence]
        data[Data]
        ml[Machine Learning]
      end
      client <--> quality
      quality <--> server
      client <--> server
    end
    roles <--> expertise
  end
</div>

<script type="module">
import mermaid from 'https://unpkg.com/mermaid@11/dist/mermaid.esm.min.mjs';
mermaid.initialize({startOnLoad: true});
</script>
