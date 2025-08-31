# 01-setup: AI コーディング環境セットアップ

このガイドは、本ワークショップの目的「AIを使ってウェブサイトのコーディングを効率的に、かつ品質高く行う」を達成するために、3つのツール（Claude Code、Cursor、Codex）を短時間で使い始めるためのセットアップ手順と、特に「コンテキストの整備」を重視した運用のコツをまとめたものです。インストールは最小限にし、精度に効く設定・使い方にフォーカスします。

## 目的

- Claude Code、Cursor、Codex、を最短で動かして使い始めれること

## 前提 / 準備

- エディタは VS Code または Cursor をインストール可能であること。
- Claude Code、Cursor、Codexが利用できるようになっていること。

## 所要時間 / 成果物

- 所要時間: 5-10分
- 成果物:
  - AI コーディング環境が三者とも起動・対話可能
  - リポジトリと Web 品質基準のコンテキストが各ツールに供給された状態
  - 動作確認チェックリストがパス

## セットアップ

- このワークショップではCursor、Claude Code、Codexを切り替えつつ、使い方実演してきます。
- 基本的に好きなツールを選んで頂いてOKです。
- CLIを使う場合は、nodeのインストールを済ませておいてください。
  - 時間の都合、node環境の構築ができていない方は、簡易なCursor環境がおすすめです。

### Cursor

- [Cursor](https://cursor.com/)をインストールしてください。できれば有料プラン（Pro）がおすすめです。
- なおCursorはCLIを使うことも可能です。CLIの場合は`cursor`コマンドで使うことができます。
  - [Cursor CLI](https://www.cursor.com/docs/guide/cli)
- なお、Cursor CLIは講師の使い込みが不足しているので、今回のハンズオンでは使用しません。

```
curl https://cursor.com/install -fsS | bash
```

### Claude Code

- [Claude Code](https://claude.ai/chat/2025-08-28)をインストールしてください。インストール可能な方は以下コマンドでインストールしてください。
- Claude Codeは**Proプラン**以上が必要です。
  - [ProまたはMaxプランでClaude Codeを使用する](11145838-pro%E3%81%BE%E3%81%9F%E3%81%AFmax%E3%83%97%E3%83%A9%E3%83%B3%E3%81%A7claude-code%E3%82%92%E4%BD%BF%E7%94%A8%E3%81%99%E3%82%8B)

```
# Claude Codeをインストール
npm install -g @anthropic-ai/claude-code

# プロジェクトに移動
cd your-awesome-project

# Claudeでコーディングを開始
claude

# 初回使用時にログインを求められます
```

### Codex

- OpenAI[Codex](https://openai.com/codex/)をインストールしてください。
- なお、CodexはIDEで使うことも可能です。Cursorの場合は拡張機能をインストールすることで使うことができます。
  - [Codex IDE extension](https://developers.openai.com/codex/ide)
- Codexは**Plusプラン**以上が必要です。
  - [Using Codex with your ChatGPT plan](https://help.openai.com/en/articles/11369540-using-codex-with-your-chatgpt-plan)

```
# Codexをインストール
npm i -g @openai/codex

# プロジェクトに移動
cd your-awesome-project

# Claudeでコーディングを開始
codex

# 初回使用時にログインを求められます
```

## 次へ

- `hands-on/02-coding.md`: コーディング実習

以上で、Claude Code / Cursor / Codex を用いた「Web コーディングに最適化した」セットアップが完了します。以降の演習では、静的サイトの作成を効率よく進めていくワークショップに進みます。
