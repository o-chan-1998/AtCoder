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
- `matplotlib` や、必要に応じて `networkx` で公開用の図を新規生成する
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

問題によっては、実装より考察が本質になる。その場合はコード説明を増やすより、状態定義、言い換え、遷移式が出る理由を濃く書く。

抽象的な状態遷移が読みにくい場合は、先に小さい具体例を置き、図でケース分けを見せてから一般式へ戻る。

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
      abc268-d\
        index.html
      abc276-e\
        index.html
      abc307-e\
        index.html
      abc308-d\
        index.html
      abc322-e\
        index.html
      abc338-d\
        index.html
      abc354-e\
        index.html
      abc436-d\
        index.html
```

`docs/index.html` は問題一覧トップページとする。

トップページには、運用方針や試作状況を説明する領域を置かない。公開ページとして必要な見出しと記事一覧だけにする。

記事一覧は、問題数が増えても追いやすいようにカード型ではなく、問題種別ごとの表形式で管理する。

D問題、E問題などの種別が増えた場合は、同じ形式のセクションを追加する。

各問題の記事は `docs/problems/{contest}-{problem}/index.html` に置く。

問題本編とは別に、派生学習や比較用の補助ページを作る場合は `docs/notes/{topic}/index.html` に置く。

派生ページの作りは、`docs/notes/linear-vs-cycle-coloring/index.html` と同じ形式を基本とする。

派生ページを作る場合は、必ず次の相互リンクを置く。

- 問題本編から派生ページへのリンク
- 派生ページから関連する問題本編への戻りリンク

問題本編側のリンクは、関連する考察段落の直後に補足ボックスとして置く。

派生ページ側のリンクは、冒頭の目的説明または末尾のまとめに置く。

例。

```txt
docs/problems/abc276-e/index.html
docs/problems/abc307-e/index.html
docs/problems/abc322-e/index.html
docs/problems/abc354-e/index.html
docs/problems/abc268-d/index.html
docs/problems/abc308-d/index.html
docs/problems/abc338-d/index.html
docs/problems/abc436-d/index.html
docs/notes/linear-vs-cycle-coloring/index.html
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

`docs/index.html` を、問題一覧トップページに変更した。現在はD問題とE問題の表形式一覧にしている。

`docs/problems/abc276-e/index.html` に、ABC276 E - Round Trip のサンプル記事を移動した。

`docs/problems/abc307-e/index.html` に、ABC307 E - Distinct Adjacent の記事を追加した。

ABC307 E は、コーディングより考察が本質の問題として、状態圧縮と遷移式の導出を厚めに書く方針に変更した。

ABC307 E には、`matplotlib` / `networkx` で新規生成した公開用図を複数追加した。

生成スクリプトは `docs/scripts/make_abc307_e_figures.py`、出力先は `docs/assets/abc307-e/`。

ABC307 E の `same` / `diff` の遷移説明は、`M = 4`、基準色を赤とする具体例の図を挟んでから一般式へ進む形に変更した。

この説明では、`same` / `diff` を色そのものではなく「並べ方の個数を入れる箱」として説明する。

遷移は「直前の色で候補を消す」「選んだ色が基準色かどうかで箱に振り分ける」の2段階として説明する。

さらに、超初心者向けの別観点として `docs/scripts/visual_005.py` を追加し、次のPNGを生成した。

- `docs/assets/abc307-e/beginner-anchor-color.png`
- `docs/assets/abc307-e/beginner-boxes-not-colors.png`
- `docs/assets/abc307-e/beginner-two-questions.png`
- `docs/assets/abc307-e/beginner-formula-from-boxes.png`

`visual_###.py` を新規作成する場合は、既存ファイル名を上書きせず、同名があれば続きの連番を振る。

GitHub Pagesの記事作成のために作ったPythonコードは、ローカル生成用の作業ファイルとして扱い、Git管理対象から外す。

`.gitignore` に `docs/scripts/`、`visual_*.py`、`**/visual_*.py` を追加済み。

別の例で理解を固めるため、`docs/scripts/visual_006.py` を追加し、`M = 5`、基準色を紫とするPNGを生成した。

- `docs/assets/abc307-e/beginner-m5-sort-sequences.png`
- `docs/assets/abc307-e/beginner-m5-same-branch.png`
- `docs/assets/abc307-e/beginner-m5-diff-branch.png`
- `docs/assets/abc307-e/beginner-m5-final-goal.png`

ABC307 E の派生学習として、直線の場合と円環の場合を比較する補助ページ `docs/notes/linear-vs-cycle-coloring/index.html` を追加した。

ABC307 E 本編と補助ページは相互リンクする。

`docs/problems/abc322-e/index.html` に、ABC322 E - Product Development の記事を追加した。

`docs/problems/abc354-e/index.html` に、ABC354 E - Remove Pairs の記事を追加した。

`docs/problems/abc268-d/index.html` に、ABC268 D - Unique Username の記事を追加した。

`docs/problems/abc264-d/index.html` に、ABC264 D - "redocta".swap(i,i+1) の記事を追加した。

`docs/problems/abc308-d/index.html` に、ABC308 D - Snuke Maze の記事を追加した。

`docs/problems/abc338-d/index.html` に、ABC338 D - Island Tour の記事を追加した。

`docs/problems/abc356-d/index.html` に、ABC356 D - Masked Popcount の記事を追加した。

`docs/problems/abc436-d/index.html` に、ABC436 D - Teleport Maze の記事を追加した。

`docs/problems/abc267-e/index.html` に、ABC267 E - Erasing Vertices 2 の記事を追加した。

`docs/problems/abc298-e/index.html` に、ABC298 E - Unfair Sugoroku の記事を追加した。

`D/436` は `001.md` と `sample.py` が Teleport Maze、`study_02.md` / `study_15.md` が別問題のサイクル分解メモになっていたため、公開記事は `001.md` / `sample.py` / `trace001.md` に合わせて Teleport Maze として作成した。

`docs/styles.css` に、公開ページ用のスタイルを作成した。

`github-pages-authoring-guide.md` に、記事作成時の手順、テンプレート、公開前チェック、Git管理の注意を整理した。

当初は `docs/assets/abc276-e/` に理解用画像の一部をコピーしていたが、既存画像は公開しない方針に変更したため削除した。

現在の試作では、既存画像の代わりに HTML/CSS で作った簡易図解を掲載している。

また、学習用の `E/276/sample.py` をそのまま掲載せず、AtCoder に提出しやすい標準入力版コードとして掲載している。

## 次に検討すること

- Astro を使うか、現在の静的 HTML/CSS 構成のまま進めるか
- 次に公開する問題を選ぶ
- 1問分の記事テンプレートを作るか
- 公開用に新しく作る画像や図解を、どのようなルールで管理するか

## 2026-07-22 作業終了時点のメモ

`git pull` は実行済み。結果は `Already up to date.`。

本日の変更はローカルに残しており、まだ commit / push していない。

未commitの主な変更。

- `.gitignore`
  - `docs/scripts/` をGit管理対象外に追加
  - `visual_*.py` と `**/visual_*.py` をGit管理対象外に追加
- `docs/index.html`
  - トップページをカード型から、問題種別ごとの表形式へ変更
  - 試作状況を説明する領域は削除済み
- `docs/styles.css`
  - 表形式一覧、記事内図、補足リンク、比較パネル用のスタイルを追加
- `docs/problems/abc307-e/index.html`
  - 考察を大幅に拡充
  - 超初心者向けの見方を追加
  - `M = 4`、基準色を赤とする説明図を追加
  - 別観点として `M = 5`、基準色を紫とする説明図を追加
  - 直線と円環を比較する派生ページへのリンクを追加
- `docs/notes/linear-vs-cycle-coloring/index.html`
  - ABC307 E の派生学習ページとして追加
  - ABC307 E 本編と相互リンク済み
- `docs/assets/abc307-e/`
  - ABC307 E 用の公開用PNGを追加

Git管理対象外としてローカルに残すもの。

- `docs/scripts/make_abc307_e_figures.py`
- `docs/scripts/visual_005.py`
- `docs/scripts/visual_006.py`

次回再開時の注意。

- Python生成コードは記事作成用のローカル作業ファイルなのでpushしない
- 公開するのは生成済みPNGとHTML/CSS/引継書
- 既存の学習用画像は引き続き公開しない
- 難易度表示には引き続き触れない
- pushする前に、`docs` 配下の表示確認と `git status --short` の確認を行う
