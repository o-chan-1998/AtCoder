# GitHub Pages 記事作成ガイド

このドキュメントは、AtCoder の学習メモを GitHub Pages 用の記事へ清書するときの作業手順をまとめたものです。

方針の詳細や経緯は `github-pages-handover.md` を正とし、このファイルでは実際に記事を作るときの確認項目に絞ります。

## 基本方針

- 公開対象は `docs` 配下の HTML / CSS / 公開用画像だけにする。
- `D` / `E` 配下は学習用の原本として扱い、公開しない。
- 問題文全文は転載せず、AtCoder の問題ページへのリンクと自分の言葉による要約を載せる。
- 既存の学習用画像はそのまま公開しない。
- 難易度の数字や難易度表示には触れない。
- `sample.py` がファイル入力形式の場合、公開記事には標準入力版へ直したコードを載せる。

## ディレクトリ構成

問題ごとの記事は次の場所に置きます。

```txt
docs/problems/{contest}-{problem}/index.html
```

例:

```txt
docs/problems/abc276-e/index.html
docs/problems/abc307-e/index.html
```

派生学習や比較用の補助ページは次の場所に置きます。

```txt
docs/notes/{topic}/index.html
```

例:

```txt
docs/notes/linear-vs-cycle-coloring/index.html
```

公開用に新規生成した画像は、問題ごとに次の場所へ置きます。

```txt
docs/assets/{contest}-{problem}/
```

## 記事作成の流れ

1. 対象問題を決める。
2. `D` / `E` 配下の学習用ファイルを読む。
3. 公開記事に載せる内容を、問題文転載ではなく自分の説明として再構成する。
4. 必要なら公開用の図解を新しく作る。
5. `docs/problems/{contest}-{problem}/index.html` を作成する。
6. `docs/index.html` の一覧へ記事リンクを追加する。
7. 補助ページを作った場合は、本編と補助ページに相互リンクを置く。
8. 表示確認を行う。
9. `git status --short` で公開対象と非公開対象を確認する。

## 記事テンプレート

各問題の記事には、原則として次の要素を入れます。

```txt
問題リンク
問題の要約
考察
解法方針
図解または文章による補足
実装の注意点
コード
つまずきポイント
まとめ
```

考察が本質の問題では、コードの行ごとの説明よりも、状態定義、言い換え、遷移式が出る理由を厚めに書きます。

抽象的な状態遷移が読みにくい場合は、先に小さい具体例を置きます。その後でケース分けを見せ、最後に一般式へ戻します。

## HTML の基本形

既存記事と同じ静的 HTML/CSS の形式を使います。

```html
<!doctype html>
<html lang="ja">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>ABC000 X - Problem Title | AtCoder Study Notes</title>
    <meta name="description" content="ABC000 X - Problem Title の解説記事です。">
    <link rel="stylesheet" href="../../styles.css">
  </head>
  <body>
    <header class="site-header">
      <div class="wrap header-grid">
        <div>
          <p class="label"><a href="../../">AtCoder Study Notes</a></p>
          <h1>ABC000 X - Problem Title</h1>
          <p class="lead">
            この記事で説明する要点を書く。
          </p>
        </div>
      </div>
    </header>

    <main>
      <section class="wrap intro" id="summary">
        <div class="problem-box">
          <span class="problem-tag">Article</span>
          <h2>問題の要約</h2>
          <p>
            問題文を転載せず、自分の言葉で要約する。
          </p>
          <p>
            問題ページ:
            <a href="https://atcoder.jp/contests/abc000/tasks/abc000_x">AtCoder ABC000 X</a>
          </p>
        </div>
      </section>

      <section class="wrap article-section" id="idea">
        <h2>考察</h2>
        <p>何を見抜く問題かを書く。</p>
      </section>

      <section class="wrap article-section" id="implementation">
        <h2>実装の注意点</h2>
        <p>添字、初期値、境界条件などを書く。</p>
      </section>

      <section class="wrap article-section" id="code">
        <h2>コード</h2>
        <pre><code>標準入力で動く提出用コードを載せる</code></pre>
      </section>
    </main>
  </body>
</html>
```

## 図解の扱い

図解が必要な場合は、公開用として新しく作ります。

- HTML/CSS で表現できるなら、まず HTML/CSS で作る。
- PNG が必要なら、`matplotlib` や `networkx` などで新規生成する。
- 生成済み PNG は `docs/assets/{contest}-{problem}/` に置く。
- 生成用 Python スクリプトはローカル作業ファイルとして扱い、Git 管理対象にしない。

`visual_###.py` を新規作成する場合は、既存ファイル名を上書きせず、続きの連番を使います。

## 補助ページの相互リンク

補助ページを作る場合は、必ず相互リンクを置きます。

- 問題本編から補助ページへのリンク
- 補助ページから関連する問題本編への戻りリンク

問題本編側のリンクは、関連する考察段落の直後に補足ボックスとして置きます。

補助ページ側のリンクは、冒頭の目的説明または末尾のまとめに置きます。

## 公開前チェック

作業後は次を確認します。

- `docs/index.html` から新しい記事へ移動できる。
- 新しい記事の相対パスが正しい。
- CSS が `../../styles.css` など、階層に合ったパスになっている。
- 画像を使う場合、`src` と `alt` が入っている。
- 問題文全文を転載していない。
- 難易度表示に触れていない。
- コードが標準入力版になっている。
- 補助ページを作った場合、相互リンクがある。
- `git status --short` で、公開しない `D` / `E` や生成スクリプトが含まれていない。

## Git 管理の注意

公開するもの:

- `docs/index.html`
- `docs/styles.css`
- `docs/problems/**/index.html`
- `docs/notes/**/index.html`
- `docs/assets/**` の公開用画像
- 引継書や作業ガイド

公開しないもの:

- `D/`
- `E/`
- `docs/scripts/`
- `visual_*.py`
- `**/visual_*.py`
- 学習用に作った未清書の画像
