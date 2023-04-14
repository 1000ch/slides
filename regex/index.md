---
marp: true
theme: default
paginate: true
footer: 正規表現コト始め by [Shogo SENSUI](https://bento.me/1000ch)
---

<!-- _class: invert -->

# 正規表現コト始め

---

# @1000ch

- 株式会社サイバーエージェント
- 専門は Web 技術全般
- 趣味で Node.js や iOS など

---

# 正規表現とは

> 正規表現（せいきひょうげん、英: regular expression）とは、文字列の集合を一つの文字列で表現する方法の一つである

[正規表現 - Wikipedia](https://ja.wikipedia.org/wiki/%E6%AD%A3%E8%A6%8F%E8%A1%A8%E7%8F%BE)

---

<!-- _class: invert -->

# 例1 `colou?r`

`?`: 直前の表現が 0 個か 1 個あることを示す

- ❌ colr
- ✅ color
- ✅ colour
- ❌ colouur

---

<!-- _class: invert -->

# 例2 `go*gle`

`*`: 直前の表現が 0 個以上あることを示す

- ✅ ggle
- ✅ gogle
- ✅ google
- ✅ gooogle

---

<!-- _class: invert -->

# 例3 `go+gle`

`+`: 直前の表現が 1 個以上あることを示す

- ❌ ggle
- ✅ gogle
- ✅ google
- ✅ gooogle

---

<!-- _class: invert -->

# よく使うやつ

- `^`: 入力の先頭にマッチする
- `$`: 入力の末尾にマッチする
- `.`: 改行文字以外のどの 1 文字にもマッチする
- `x|y`: x または y にマッチする
- `{n}`: 直前の文字がちょうど n 回出現するものにマッチする
- `{n,m}`: 直前の文字が少なくとも n 回、多くても m 回出現するものにマッチする
- `[xyz]`: 文字集合を表し、角括弧で囲まれた文字のいずれか一個にマッチする

---

<!-- _class: invert -->

# よく使うエイリアス

- `\d`: `[0-9]` と等価であり、数字にマッチする
- `\s`: スペース、タブ、改ページ、改行を含む 1 個のホワイトスペース文字にマッチする
- `\t`: タブにマッチする
- `\w`: `[A-Za-z0-9_]` と等価であり、アンダースコアを含むどの英数字にもマッチする

---

# 参考リンク

- [正規表現 - JavaScript | MDN](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Regular_Expressions)
- [正規表現 - Wikipedia](https://ja.wikipedia.org/wiki/%E6%AD%A3%E8%A6%8F%E8%A1%A8%E7%8F%BE)
- [https://1000ch.github.io/regex-test/](https://1000ch.github.io/regex-test/)
