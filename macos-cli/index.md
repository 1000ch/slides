---
marp: true
title: macOS の黒い画面
theme: default
paginate: true
footer: macOS の黒い画面 by [@1000ch](https://bento.me/1000ch)
---

<!-- _class: invert -->

# <!-- fit --> macOS の黒い画面

---

![bg left:30% 60%](https://shogosensui.com/img/1000ch.avif)

# @1000ch

> Web アプリケーション開発を専門とするソフトウェアエンジニア。企業で働く傍ら、技術顧問として複数企業のエンジニアリングに関わり、高品質で維持しやすい Web アプリケーションを作るための活動を続けている。

---

![bg right:50%](https://cdn.dribbble.com/users/1538311/screenshots/12265146/media/39965e040d04683fbdfadea9965da36f.png?resize=1600x1200&vertical=center)

# macOS の CLI

CLI は Command Line Interface の略、[Terminal](https://support.apple.com/ja-jp/guide/terminal/welcome/mac) や [iTerm2](https://iterm2.com/) は macOS のシステムと CLI で対話するアプリケーション

---

![bg right:50%](https://help.apple.com/assets/642601949698396B0B0C2097/6426019B9698396B0B0C20AF/ja_JP/cc7512aa13a504b680919a832af2ee36.png)

# macOS の GUI

GUI は Graphical User Interface の略、オペレーティングシステムとしての macOS や Finder は macOS のシステムと GUI で対話するアプリケーション

---

<!-- _class: invert -->

# <!-- fit --> 黒い画面は怖くない 👻

敷居が高く見られるのは、愛着が湧きにくいモノクロなインターフェースのせいという仮説

---

# [iTerm2](https://iterm2.com/) をインストールしてセットアップ

1. 好みのカラープロファイルを [iTerm2-Color-Schemes](https://github.com/mbadolato/iTerm2-Color-Schemes) からダウンロードする。[iTerm の環境設定 > Profiles > Colors > Color Presets](https://iterm2.com/documentation-preferences-profiles-colors.html) からインポートする
2. 好みの等幅フォントを [Fira](https://github.com/mozilla/Fira), [Roboto](https://github.com/google/fonts/tree/main/apache/robotomono) あたりからダウンロードして、[Font Book](https://support.apple.com/ja-jp/guide/font-book/welcome/mac) でインストールし、[iTerm の環境設定 > Profiles > Text > Font](https://iterm2.com/documentation-fonts.html) で選択する

---

# [Homebrew](https://brew.sh/) をインストールしてセットアップ

1. zsh を `brew install zsh` でインストールする
2. git を `brew install git` でインストールする
3. [pure](https://github.com/sindresorhus/pure) を `brew install pure` でインストールする

```sh
# .zshrc
autoload -U promptinit; promptinit
prompt pure
```

---

<!-- _class: invert -->

# <!-- fit --> はじめに覚えるいくつかのこと

ディレクトリとエイリアス、相対パスと絶対パス、頻出コマンド

---

# ディレクトリとエイリアス

- ディレクトリは平たく言えばフォルダであり、macOSのシステムにある全てのファイルやフォルダを格納するフォルダをルートディレクトリと呼び `/` で表す
- 現在位置であるカレントディレクトリを `.` で表し、イチ階層上の親ディレクトリを `..` で表す
- macOS のログインユーザーのディレクトリは `/Users/<yourname>` に存在する。これをホームディレクトリと呼び、`~` と等価である

---

# 相対パスと絶対パス

- 相対パスはカレントディレクトリからの相対位置、絶対パスはルートディレクトリからの絶対位置を表す。
- カレントディレクトリが `/Users/1000ch` の場合に `/Users` を参照することを考える。相対パスであれば `..` であり、絶対パスであれば `/Users` である
- カレントディレクトリが `/Users/1000ch` の場合に `/` を参照することを考える。相対パスであれば `../..` であり、絶対パスであれば `/` である

---

# ディレクトリ移動の頻出コマンド

## `cd <directory>`

change directory の頭文字、対象ディレクトリに移動する

## `ls <directory>`

list segments の頭文字、対象ディレクトリのファイルを列挙する。`-a` や `-l` オプションと組み合わせて使うことが多い

## `pwd`

print working directory の頭文字、カレントディレクトリを絶対パスで出力する

---

# ファイル操作の頻出コマンド

## `touch <file>`

対象のファイルを新規作成もしくは更新する

## `mv <file a> <file b>`

move の省略形、対象のファイルを移動する

## `cp <file a> <file b>`

copy の省略形、対象のファイルを複製する

---

# ディレクトリ操作の頻出コマンド

## `mkdir <directory>`

make directory の省略形、対象のディレクトリを作成する

## `rm <file|directory>`

remove の省略形、対象のディレクトリを削除する。`-r` で配下を再帰的に削除する

## `open <file|directory>`

対象のファイルもしくはディレクトリを開く。`-a` で開くアプリケーションを指定する
