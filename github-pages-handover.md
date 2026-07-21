# GitHub Pages 引継書

## 目的

AtCoder の学習内容を、GitHub Pages で解説記事として公開する。

主な用途は自分の学習用だが、「3日後の自分は赤の他人」とみなし、他の人が読んでも理解できる記事にする。

## 現在の学習ファイルの位置づけ

既存の `D` / `E` ディレクトリ内で AtCoder の学習を行っている。

各問題に対して、概ね次のファイルが存在する想定。

- `001.md`: 問題文
- `study_002.md`: 解答方針の解説
- `study_015.md`: まとめ
- `sample.py`: 解答コード
- 画像ファイル: 理解用の図解、メモ、補助資料

`sample.py` は学習用のため、標準入力ではなくファイル入力になっている。

## 公開方針

GitHub Pages に公開するのは、新規に作成する公開用ページのみとする。

既存の `D` / `E` ディレクトリは、学習用の原本として扱い、GitHub Pages にはアップロードしない。

公開記事では、既存ファイルをそのまま並べるのではなく、1問ごとに読みやすい解説記事へ再構成する。

将来的には全問題をアップロード予定。そのため、トップページを記事一覧、各問題を個別ページとして管理する。

GitHub リポジトリと公開URL。

- Repository: https://github.com/o-chan-1998/AtCoder
- GitHub Pages: https://o-chan-1998.github.io/AtCoder/

## 禁止事項

既存の学習用画像を、公開用ページへそのままアップロードしない。

理由は、学習用データと公開用の清書版を明確に分けるため。

公開記事で図解が必要な場合は、次のいずれかの形で清書版を作る。

- HTML/CSS で簡単な図解を作る
- 公開用として新しく作成した画像だけを使う
- 文章や表で説明できる場合は画像にしない

難易度の数字や難易度表示には一切触れない。

理由は、難易度自体がヒントになり、学習の妨げになるため。

## 記事の基本構成

1問につき1記事を基本とする。

記事には次の要素を入れる。

- 問題リンク
- 問題の要約
- 考察
- 解法方針
- 図解または文章による補足
- 実装の注意点
- コード
- つまずきポイント
- まとめ

公開記事で特に重視すること。

- 何を見抜く問題だったか
- なぜその解法でよいか
- 実装でどこに注意するか

## 問題文の扱い

`001.md` に問題文がある場合でも、公開記事では問題文全文の転載は避ける。

公開記事には、AtCoder の問題ページへのリンクと、自分の言葉による要約を載せる。

## コードの扱い

学習用の `sample.py` はファイル入力形式になっているため、公開記事では必要に応じて標準入力版に直す。

ローカル検証用のファイル入力版は、学習用ディレクトリに残す。

公開記事には、読者が AtCoder にそのまま提出しやすい形のコードを載せることを優先する。

## サイト構成の方針

公開用サイトは、既存の `D` / `E` ディレクトリとは分離して `docs` ディレクトリで管理する。

GitHub Pages の公開元は、`master` ブランチの `/docs` に設定済み。

現在の構成。

```txt
C:\AtCoder
  D\
  E\
  docs\
    index.html
    styles.css
    problems\
      abc276-e\
        index.html
      abc307-e\
        index.html
      abc322-e\
        index.html
      abc354-e\
        index.html
```

`docs/index.html` は問題一覧トップページとする。

各問題の記事は `docs/problems/{contest}-{problem}/index.html` に置く。

例。

```txt
docs/problems/abc276-e/index.html
docs/problems/abc307-e/index.html
docs/problems/abc322-e/index.html
docs/problems/abc354-e/index.html
```

公開URLの例。

```txt
https://o-chan-1998.github.io/AtCoder/
https://o-chan-1998.github.io/AtCoder/problems/abc276-e/
```

`D` / `E` は `.gitignore` に追加し、誤って GitHub にアップロードしない。

## 技術選定の現時点方針

現在は静的 HTML/CSS で試作している。

Markdown ベースで記事を書ける構成にする案として Astro は引き続き候補。

ただし、トライアンドエラーで進めるため、必要に応じて方針は変更する。

## 運用ルール

方針、構成、技術選定、記事テンプレート、公開対象に変更があった場合は、この引継書を更新する。

作業の途中で判断を変えた場合も、後から経緯が追えるように、この引継書へ反映する。

## 作成済みの試作

`docs/index.html` を、問題一覧トップページに変更した。

`docs/problems/abc276-e/index.html` に、ABC276 E - Round Trip のサンプル記事を移動した。

`docs/problems/abc307-e/index.html` に、ABC307 E - Distinct Adjacent の記事を追加した。

`docs/problems/abc322-e/index.html` に、ABC322 E - Product Development の記事を追加した。

`docs/problems/abc354-e/index.html` に、ABC354 E - Remove Pairs の記事を追加した。

`docs/styles.css` に、公開ページ用のスタイルを作成した。

当初は `docs/assets/abc276-e/` に理解用画像の一部をコピーしていたが、既存画像は公開しない方針に変更したため削除した。

現在の試作では、既存画像の代わりに HTML/CSS で作った簡易図解を掲載している。

また、学習用の `E/276/sample.py` をそのまま掲載せず、AtCoder に提出しやすい標準入力版コードとして掲載している。

## 次に検討すること

- Astro を使うか、現在の静的 HTML/CSS 構成のまま進めるか
- 次に公開する問題を `D` / `E` のどちらから選ぶか
- 1問分の記事テンプレートを作るか
- 公開用に新しく作る画像や図解を、どのようなルールで管理するか
