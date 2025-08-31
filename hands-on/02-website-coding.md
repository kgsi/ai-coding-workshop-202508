# 02-website-coding: Next.js + TypeScript + Tailwind でデザインから実装へ（Figma 支給）

この演習では、Figmaのデザインデータを前提に、Next.js（App Router）+ TypeScript + Tailwind CSS で静的ページを構築します。AI コーディングツールを活用しながら、再現度高く実装するテクニックを学ぶワークショップです。

## 目的

- デザインを忠実に再現するために必要なテクニックやツールを学びます。
- セマンティック HTML と a11y を踏まえたページ骨子を、AI と協調して効率よく構築します。
- レスポンシブ（モバイルファースト）で破綻しない CSS 設計を、Tailwind のユーティリティで表現します。

## デザインデータからの実装方法

- デザインデータからの画面再現、実装については大きく分けると以下の方法があります。
  - デザインデータからコードを取得して再現する（Figma Dev、Figma Plugin、MCP...）
  - 目検でデザインを再現する（職人がデザインデータから再現する）
- 旧来は目検で再現して実装する方法が主流でしたが、Figma Plugin（Animaなど）の進化に伴い、デザインデータからの実装が主流になっています。
- AIの進化で、画像からの再現、更にMCPを経由した実装もできるようになりました。
  - 今回は主にFigma MCPを経由したシームレスな実装方法について実演します。

## 所要時間 / 成果物

- 所要時間: 30分
- 成果物:
  - Next.js アプリ雛形（App Router）とコンテキスト+セットアップ
  - LPサイトの再現やMCPの使い方を知れる

## セットアップ

Next.js アプリ雛形（App Router）の雛形を作成します。

```bashs
npx create-next-app@latest workshop-starter-coding --typescript --eslint --app
```

## 教材

- [実演・教材用Figmaファイル（.fig）](https://drive.google.com/file/d/1mPtndp0TVcwwNb1mrjj-pASIGsdNm6MU/view?usp=sharing)
  - ダウンロードしてお手元にコピーしてください。
  - `hero`、`hero-mobile`、`lp-site`の3つを使います。
- [HPワイヤーフレーム・デザインテンプレート](https://www.figma.com/community/file/1460259841530177202)
  - 有志がアップしている日本語のデザインテンプレートです。
  -

## セットアップしておくと良いもの

- Figma MCP
  - Figma Devモードが使える方は、MCP設定をONにしておいてください。
    - https://help.figma.com/hc/ja/articles/32132100833559-Dev-Mode-MCP%E3%82%B5%E3%83%BC%E3%83%90%E3%83%BC%E5%88%A9%E7%94%A8%E3%82%AC%E3%82%A4%E3%83%89
  - 公式MCPを使えない場合は、`Framelink Figma MCP Server`を使ってください。ただし非公式プラグインではあるので、自己責任でお願いします。
    - [Framelink Figma MCP Server](https://github.com/GLips/Figma-Context-MCP)
- Serena
  - https://github.com/oraios/serena

## コンテキスト（指示書）をセットアップ

- 各ツールでのコンテキスト理解は重要です。
  - これらがないと十分な性能を発揮しないので、必ずセットアップしておいてください。
- 初期セットアップは以下で可能です。
  - claude
    - CLIで`/init`を実行すると`CLAUDE.md`を作成。
  - cursor
    - チャットコマンドで`/Generate Cursor Rules`を実行すると`{filename}.mdc`を`.cursor/rules`に作成。
  - codex
    - CLIで`/init`を実行するとコードを読み込んで`AGENTS.md`を作成。

--

## ワークショップ課題：Heroセクション

- Heroビジュアルの再現とレスポンシブ対応を試しましょう。

### Step.1

基本的なデザインの再現をしてみましょう。
既存のデザインを再現するには2つの方法があります。

```sample-prompt
@app/page.tsxに以下FigmaファイルをMCP経由で読み込んで、デザインを忠実に再現して。

{DevモードでコピーしたFigmaの参照リンク}
```

### Step.2

デザインをもとに実装したページをレスポンシブに対応させましょう。

```text:sample-prompt
この仕様に合わせて、レスポンシブサイトを作りたい。FigmaファイルをMCP経由で読み込み、モバイルで表示された際のデザインを再現して。忠実に再現しつつ、すでに実装済みのサイトと整合性を合わせて実装すること。

{DevモードでコピーしたFigmaの参照リンク}
```

### Ex. Figma Rawで再現する

- Figma RawというFigmaのデザインデータをJSONで書き出すプラグインを使う方法もあります。
  - [Figma Raw: Export Design Data for AI/LLM & Agents](https://www.figma.com/community/plugin/1491678546144854232/figma-raw-export-design-data-for-ai-llm-agents)
- 参考：[FigmaのデザインデータをAIに伝えるプラグイン「Figma Raw」を公開しました](https://note.com/_yyyyy/n/n2052fa7ba9db)

```text:sample-prompt
これはFigmaから書き出したサイト構造を示したJSON、これをもとに、ウェブサイトのデザインを忠実に再現して
```

### ポイント

- デスクトップ、モバイルそれぞれでレイヤー名をできるだけ揃える
- オートレイアウト活用する

## ワークショップ課題：LPサイト全体

- 応用編として、LPサイトのような情報量が多いページの再現をしましょう。
- ここからは時間いっぱい、AIと戯れて再現を試みてください。

### ポイント

- MCP経由でFigmaファイルを読み込むと大量のコンテキストを渡すことになります。
  - 一度に全部まとめて実装するとコンテキストが多すぎて実装が難しくなります。
- MCPの画像設定は`プレースホルダー画像を使用する`が無難。
  - 画像データはコンテキストを大量に消費するので、できるだけ少なくしましょう。

## さらなるクオリティ向上策

## まとめ

- コンテキストを細かく与えることが重要
  - 特にFigmaファイルや画像ファイルはコンテキストを大量に消費するので、分割指示が基本となります。
- コードは理解する必要が引き続きある
  - AIは自動生成してくれますが、出力されたアウトプットを根本理解しているわけではない、指示に従って出力されているだけです。
  - 品質に保証をもってくれるわけではありません。
