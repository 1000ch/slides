---
marp: true
theme: default
paginate: true
footer: The Silver Searcher のススメ by [@1000ch](https://bento.me/1000ch)
---

# The Silver Searcher のススメ

---

![bg left:30% 60%](https://shogosensui.com/img/1000ch.avif)

# @1000ch

> Web アプリケーション開発を専門とするソフトウェアエンジニア。企業で働く傍ら、技術顧問として複数企業のエンジニアリングに関わり、高品質で維持しやすい Web アプリケーションを作るための活動を続けている。

---

# ファイルの中身を検索するときに何を使っている？

- `grep`: Linux に標準搭載されている
- `ack`: `grep` より高速に動作する

---

# [The Silver Searcher](https://github.com/ggreer/the_silver_searcher) というものがあります

---

# The Silver Searcher?

- `ack` よりも速い
- `ack` よりもコマンドが短い
- `.gitignore` の内容を検索対象から除外
- オプションが直感的で便利

---

# ベンチマーク vs ack

```bash
$ ack test_blah ~/code/
// => 104.66s user 4.82s system 99% cpu 1:50.03 total

$ ag test_blah ~/code/
// => 4.67s user 4.58s system 286% cpu 3.227 total
```

---

# インストール via Homebrew

```bash
$ brew install the_silver_searcher
```

---

# keyword で検索

```bash
# keyword で検索
$ ag keyword

# keyword で folder 配下を検索
$ ag keyword folder
```

---

# 検索オプションはいろいろ

```bash
# 圧縮されたファイルも検索
$ ag -z/--search-zip keyword

# パターンにマッチするファイル・フォルダを検索
$ ag -G/--file-search-regex '\.(js|json)' keyword

# 隠しファイルも検索
$ ag --hidden keyword

# 全ファイルを検索
$ ag -u/--unrestricted keyword

# JS ファイルを検索
$ ag --js keyword
```

---

# 出力のオプションもいろいろ

```bash
# マッチしたファイル名だけ表示
$ ag -l/--files-with-matches keyword

# マッチしなかったファイル名だけ表示
$ ag -L/--files-without-matches keyword

# マッチした回数を表示
$ ag -c/--count keyword

# マッチした行のみ表示
$ ag -o/--only-matching keyword
```

---

# 所感

- タイプ数が少ないのは結構大きい
- プロジェクトが大きくてもログが膨大でも大丈夫
- `yum` でも `apt-get` でも使えるのでサーバーに入れる価値ある

---

# おしまい
