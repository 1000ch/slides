---
marp: true
title: はじめての Git
theme: default
paginate: true
footer: はじめての Git by [@1000ch](https://bento.me/1000ch)
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

# <!-- fit --> はじめての Git

by [@1000ch](https://bento.me/1000ch)

---

![bg left:30% 60%](https://shogosensui.com/img/1000ch.avif)

# @1000ch

> Web アプリケーション開発を専門とするソフトウェアエンジニア。企業で働く傍ら、技術顧問として複数企業のエンジニアリングに関わり、高品質で維持しやすい Web アプリケーションを作るための活動を続けている。

---

![bg right:30%](https://upload.wikimedia.org/wikipedia/commons/thumb/0/01/LinuxCon_Europe_Linus_Torvalds_03_%28cropped%29.jpg/440px-LinuxCon_Europe_Linus_Torvalds_03_%28cropped%29.jpg)

# Git とは

> Git（ギット）は、プログラムのソースコードなどの変更履歴を記録・追跡するための分散型バージョン管理システムである。Linuxカーネルのソースコード管理に用いるためにリーナス・トーバルズによって開発され、それ以降ほかの多くのプロジェクトで採用されている。
> via [Git - Wikipedia](https://ja.wikipedia.org/wiki/Git)

---

<!-- _class: invert -->

# <!-- fit --> バージョン管理とは何か

---

# バージョン管理の概念がない場合の運用例

<div class="mermaid">
flowchart LR
subgraph LocalX[Local 🙍🏻‍♀️💻]
  local-file-xa[File A]
  local-file-xb[File B]
  local-file-xc[File C]
end
subgraph Server[Server 🖥️]
  server-file-a[File A]
  server-file-b[File B]
  server-file-c[File C]
end
subgraph LocalY[Local 🙍🏻‍♂️💻]
  local-file-ya[File A]
  local-file-yb[File B]
  local-file-yc[File C]
end
LocalX -- copy --> Server
LocalY -- copy --> Server
</div>

- ファイルをコピーして本番に反映させるため、問題が発生時に復元が難しい。ローカルに `ファイル_20230101.txt` のようなファイルが増え続ける
- 作業者の間でファイルを同期するなどの管理が難しい。何らかの通信手段を用いて共有するも、どれを正とすれば良いかわからず容易に競合する

---

# バージョン管理で解決できること

<div class="mermaid">
flowchart LR
subgraph LocalX[Local 🙍🏻‍♀️💻]
  local-file-xa[File A]
  local-file-xb[File B]
  local-file-xc[File C]
end
subgraph Repository[Repository 📀]
  repository-file-a[File A]
  repository-file-b[File B]
  repository-file-c[File C]
end
subgraph LocalY[Local 🙍🏻‍♂️💻]
  local-file-ya[File A]
  local-file-yb[File B]
  local-file-yc[File C]
end
subgraph Server[Server 🖥️]
  server-file-a[File A]
  server-file-b[File B]
  server-file-c[File C]
end
LocalX <-- sync --> Repository
LocalY <-- sync --> Repository
Repository -- copy --> Server
</div>

- 変更の履歴を貯蔵庫に記録し、作業者が履歴を取得したり新たに積み上げ、貯蔵庫のデータを正として管理していく
- 履歴に記録されているどの時点の状態も復元できる。各時点の差分を確認し、問題点の発見を容易にする

---

<!-- _class: invert -->

# <!-- fit --> Git の概念を理解する

---

# ローカルリポジトリとリモートリポジトリ

<div class="mermaid">
flowchart LR
subgraph LocalX[Local 🙍🏻‍♀️💻]
  subgraph LocalCommitsX[Commits]
    commitedX[File]
  end
end
subgraph Remote[Remote 🖥️]
  subgraph RemoteCommits[Commits]
    pushed[File]
  end
end
subgraph LocalY[Local 🙍🏻‍♂️💻]
  subgraph LocalCommitsY[Commits]
    commitedY[File]
  end
end
LocalCommitsX -- git push --> RemoteCommits
RemoteCommits -- git pull --> LocalCommitsX
LocalCommitsY -- git push --> RemoteCommits
RemoteCommits -- git pull --> LocalCommitsY
</div>

- ローカルもリモートも Git のリポジトリであり、Git における差分のまとまりであるリビジョンを格納している
- リビジョンの履歴を、リモートから [`git pull`](https://git-scm.com/docs/git-pull) でローカルに受信したり、ローカルから [`git push`](https://git-scm.com/docs/git-push) でリモートに送信する

---

# ローカルの変更を差分としてコミット

<div class="mermaid">
flowchart LR
subgraph Local[Local 🙍🏻‍♀️💻]
  changed[File]
  subgraph LocalStaged[Staged]
    staged[File]
  end
  subgraph LocalCommits[Commits]
    commited[File]
  end
end
subgraph Remote[Remote 🖥️]
  subgraph RemoteCommits[Commits]
    pushed[File]
  end
end
changed -- git add --> LocalStaged
LocalStaged -- git reset --> changed
LocalStaged -- git commit --> LocalCommits
LocalCommits -- git push --> RemoteCommits
</div>

- ファイルを変更すると差分が発生する。差分を [`git diff`](https://git-scm.com/docs/git-diff) で確認し、[`git add`](https://git-scm.com/docs/git-add) でコミットの対象に含め、[`git reset`](https://git-scm.com/docs/git-reset) でコミットの対象から外す
- 対象に含めた差分全体を [`git commit`](https://git-scm.com/docs/git-commit) で差分のまとまりであるリビジョンを作成する、これをコミットと呼ぶ

---

# 作業のコンテキストをブランチで分割

<div class="mermaid">
gitGraph
commit
commit
branch work-a
checkout work-a
commit
checkout main
commit
branch work-b
checkout work-b
commit
checkout main
commit
checkout work-a
commit
checkout main
merge work-a
checkout work-b
commit
checkout main
merge work-b
commit tag: "v0.1.0"
</div>

- 履歴に対する差分をコミットする、という一連のコンテキストをブランチを作ることで分割できる
- [`git branch`](https://git-scm.com/docs/git-branch) で現在のブランチから新しいブランチを作成し、[`git switch`](https://git-scm.com/docs/git-switch) で現在のブランチを切り替える

---

# ファイルを作成したり変更してプッシュ

```sh
$ git branch add-x-and-update-y
$ git switch add-x-and-update-y

# file-x.md というファイルを作成する
# 既存の file-y.md というファイルを修正する

$ git diff
$ git add ./x.md
$ git add ./y.md
$ git commit -m 'x を追加したついでに y を変更した'
$ git push origin add-x-and-update-y
```

<script type="module">
import mermaid from 'https://unpkg.com/mermaid@10/dist/mermaid.esm.min.mjs';
mermaid.initialize({startOnLoad: true});
</script>
<script defer src="https://platform.x.com/widgets.js"></script>
