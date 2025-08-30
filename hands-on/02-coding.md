# 02-coding: Next.js + TypeScript + Tailwind でデザインから実装へ（Figma 支給）

この演習では、Figma のデザインデータを前提に、Next.js（App Router）+ TypeScript + Tailwind CSS で静的ページを構築します。AI コーディングツールを活用しながら、再現度高く実装するテクニックを学ぶワークショップです。

## 目的

- デザインを忠実に再現するために必要なテクニックやツールを学びます。
- セマンティック HTML と a11y を踏まえたページ骨子を、AI と協調して効率よく構築します。
- レスポンシブ（モバイルファースト）で破綻しない CSS 設計を、Tailwind のユーティリティで表現します。

## 所要時間 / 成果物

- 所要時間: 30 分
- 成果物:
  - Next.js アプリ雛形（App Router）とコンテキスト+セットアップ

## セットアップ

Next.js アプリ雛形（App Router）の雛形を作成します。

```
npx create-next-app@latest workshop-starter-kit --typescript --eslint --app
```

## 教材

- https://www.figma.com/community/file/1460259841530177202

## 事前にセットアップしておくと良いもの

- Figma
  - Figma Devモードが使える方は、MCP設定をONにしておいてください。
    - https://help.figma.com/hc/ja/articles/32132100833559-Dev-Mode-MCP%E3%82%B5%E3%83%BC%E3%83%90%E3%83%BC%E5%88%A9%E7%94%A8%E3%82%AC%E3%82%A4%E3%83%89
- Serena
  - https://github.com/oraios/serena
- Vibe Kanban（可能なら）
  - https://www.vibekanban.com/

## コンテキストをセットアップ

コンテキストをセットアップしないと、十分な性能を発揮しないので

- claudeは`/init`を実行するとコードを読み込んで`CLAUDE.md`を作成してくれます。
- cursorは`/init`を実行するとコードを読み込んで`CURSOR.md`を作成してくれます。
- codexは`/init`を実行するとコードを読み込んで`CODEX.md`を作成してくれます。

---

## 実装ケース（Heroセクション）

### 教材

- https://www.figma.com/community/file/1460259841530177202

### Step.1

```
@app/page.tsxに以下FigmaファイルをMCP経由で読み込んで、デザインを忠実に再現して。

https://www.figma.com/design/xxxx
```

### Step.2

```
この仕様に合わせて、レスポンシブサイトを作りたい。
以下がモバイルで表示された際のデザイン。このデザインを忠実に再現しつつ、すでに実装済みのサイトと整合性を合わせて実装して

https://www.figma.com/design/xxxx
```

### EX Figma Rawで再現する

https://www.figma.com/community/plugin/1491678546144854232/figma-raw-export-design-data-for-ai-llm-agents

```
これはFigmaから書き出したサイト構造を示したJSON、これをもとに、ウェブサイトのデザインを忠実に再現して
```

### ポイント

- デスクトップ、モバイルそれぞれでレイヤー名をできるだけ揃える
- オートレイアウト活用する

## 実装ケース（LPサイト全体）

### 教材

- https://www.figma.com/community/file/1460259841530177202
