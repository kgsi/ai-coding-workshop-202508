# AI コーディング・ワークショップ運用ガイド

## リポジトリの目的

- 本リポジトリは、AI を活用してウェブサイトのコーディングを効率的かつ高品質に行うためのワークショップ（講義・スライド・ハンズオン）の作成・配布・運用のための共同作業スペースです。
- 主な成果物は Markdown ベースのスライド（`slide/`）とハンズオン資料（`hands-on/`）です。ビルドは不要で、エディタでのプレビュー前提で運用します。
- 既定の言語は日本語です（コード、コマンド、識別子は英語）。詳細は付録の言語ポリシーをご参照ください。

## Web コーディング品質基準（本ワークショップの前提）

- セマンティック HTML: 見出し階層（`h1` は1ページ1つ）、`header/nav/main/section/article/aside/footer` の適切な利用。
- アクセシビリティ: 画像の代替テキスト、フォームのラベル、ランドマーク、キーボード操作、色コントラストの配慮。
- レスポンシブ: モバイルファーストのレイアウトとブレークポイント設計、相対単位（`rem/%`）の活用。
- パフォーマンス基本: 画像最適化、不要なライブラリを避ける、CSS の適切な分割（必要に応じて）。
- CSS 設計: シンプルな BEM 風命名、ユーティリティ最小限、デザイントークン（色・間隔・フォントサイズ）の変数化。
- ファイル構成（静的サイト想定）: `example/` 配下に `index.html`, `styles/`, `images/` を配置（相対パス参照）。

## スライド作成ガイド（slide/）

- ディレクトリ: `slide/` に配置します。章立てや順序が分かるように数値プレフィックスを付けます。
- ファイル命名: `NN-title.md`（例: `01-begin.md`, `02-ai-coding-tools-slides.md`）。
- 構成ルール:
  - 1ファイル1つの H1 見出し（タイトル）にします。
  - セクションは H2（`##`）から始め、箇条書き中心で要点を簡潔にまとめます。
  - スピーカーノートは HTML コメント（`<!-- note: ～ -->`）または「Note:」行で補足します。
- アセット/画像:
  - 画像は `slide/` 配下に相対パスで配置し、`![代替テキスト](./img.png)` のように参照します。
  - 画面キャプチャは 1600px 幅程度を目安にし、PNG/JPEG を最適化してください。
  - 出典/ライセンスが必要な場合はスライド末尾に明記します。
- スライド基本セクション例:
  - 目的（ねらい）/ 観客にとっての価値
  - 今日のゴール / 成果物
  - 背景 / コンテキスト（なぜ今これが必要か）
  - 実演デモ手順（手元で再現できるステップ）
  - ベストプラクティス / よくある落とし穴
  - まとめ / 次のアクション / 参考リンク
- 品質チェック:
  - フォーマットは Prettier 準拠です（`npx prettier --check .`）。
  - 長文は短い箇条書きに分割し、1項目は1文程度を目安にします。

## 資料（ハンズオン）作成ガイド（hands-on/）

- ディレクトリ: `hands-on/` に配置します。順序がある場合は数値プレフィックスで並べます。
- ファイル命名: `NN-topic.md`（例: `01-setup.md`, `02-coding.md`, `03-mcp.md`）。
- 最低限含めるセクション:
  - 目的: この演習で何ができるようになるか
  - 前提: 環境要件・想定スキル・事前準備
  - 所要時間: おおよその目安（例: 15 分）
  - 成果物: 最終的に得られるファイルや知識
  - 手順: 番号付きステップで具体的に記述
  - 実行方法（How to run）: 実行コマンド・確認方法を明記
  - 検証: 成功判定（期待する出力・スクリーンショット）
  - トラブルシュート: 典型的な失敗と対処
  - 次へ: 関連演習や応用課題
- 雛形（コピーして利用ください）:

  ```markdown
  # タイトル（H1・1ファイル1つ）

  ## 目的

  - この演習で身につくこと

  ## 前提 / 準備

  - 必要なツール、バージョン、セットアップ

  ## 所要時間 / 成果物

  - 所要時間: 15 分 / 成果物: 〜

  ## 手順

  1. ステップ1
  2. ステップ2

  ## 実行方法（How to run）

  - コマンド: `...`
  - 確認: 期待する出力は ...

  ## 検証

  - チェックリスト / スクリーンショット

  ## トラブルシュート

  - 症状A: 対処...

  ## 次へ

  - 関連演習 / 応用
  ```

## 作業ワークフロー（スライド/資料共通）

- ブランチ作成: `feat/slides-<topic>` や `docs/hands-on-<topic>` などで作業します。
- 追加/編集: `slide/` または `hands-on/` に Markdown とアセットを追加します。
- 整形: `npx prettier -w .` を実行して体裁を統一します。
- PR 作成: 変更概要、対象ファイル、スクリーンショット（見た目変更時）を添付し、`npx prettier --check .` が通ることを確認します。
- 命名/コミット: Conventional Commits を使用します（例: `docs(slide): 02-xxx を追加`）。

## AI エージェントへの指示テンプレート（例）

- スライド構成案: 「このアウトライン案を 5〜7 枚構成に再整理し、各枚に3つの bullet（成果に直結する要点）で提案してください。制約: 1ファイル1H1、画像は相対パス、言語は日本語です。」
- スライド原稿の推敲: 「以下のスライド原稿を簡潔な箇条書きに直し、重複を削減しつつ、デモ手順を明確化してください。Prettier 準拠の Markdown にしてください。」
- 画像/図の指示: 「このセクションに合う図の構成（要素、矢印、ラベル文言）をテキストで指示してください。作図はエディタの Markdown 画像として差し込める想定で。」
- ハンズオン検証の明確化: 「手順ごとの成功判定（期待出力）を追加し、トラブルシュートを3件以上提案してください。」
- 参照統一: 「相対リンクとファイル命名を既存ルールに合わせて点検・修正してください。」
- Web コーディング（骨子→実装）: 「この要件とサイトマップを基に、セマンティック HTML のアウトラインを作り、続けて BEM 命名の CSS を伴うモバイルファーストの静的ページを提案してください。制約: アクセシビリティ配慮、相対リンク、画像は `example/images/`、1ページ1つの `h1`。」
- 品質照合: 「生成した HTML/CSS を、AGENTS.md の『Web コーディング品質基準』と照合し、不足箇所を列挙・修正してください。」

## 付録: Repository Guidelines

### Project Structure & Module Organization

- Root docs: `README.md` (workshop overview), `PROGRAM.md` (agenda/spec), `deck.md` (slide deck meta).
- Folders: `guide/` and `slide/` reserved for workshop materials; add Markdown or assets as needed.
- Tooling: `package.json` with `prettier` dependency and `package-lock.json`. No build system or runtime code.

### Build, Test, and Development Commands

- Install tools: `npm ci` (uses `package-lock.json`).
- Format all files: `npx prettier -w .`
- Check formatting (CI-friendly): `npx prettier --check .`
- Preview docs: open Markdown in your editor; no build step required.

### Coding Style & Naming Conventions

- Markdown: use ATX headings (`#`, `##`), one H1 per file; wrap lines naturally.
- Lists: 2-space indentation for sub-items; keep bullets concise.
- Filenames: lowercase-kebab-case for new docs (e.g., `session-notes.md`).
- Links/Assets: prefer relative paths within the repo; place images under `slide/` or `guide/`.
- Formatting: Prettier is the source of truth; configure via `.prettierrc.js` if needed.

### 言語ポリシー（日本語で返答）

- 既定: すべてのドキュメント、Issue/PR の説明、AI エージェントの出力は日本語（です・ます調）で記述・返答してください。
- 例外: コード、コマンド、識別子、Conventional Commits の型・スコープは英語を使用します。
- コミット例: `docs(readme): 事前準備を追記`（型は英語、本文は日本語可）。
- 英語併記が必要な場合は、日本語を先頭に置き、英語は任意で追記。

### Testing Guidelines

- No automated tests at this time. For exercises that include code, add a short “How to run” section in the same Markdown file and, if you introduce scripts, document them under a new `scripts` entry in `package.json`.

### Commit & Pull Request Guidelines

- Commits: follow Conventional Commits for clarity, e.g., `docs(readme): clarify prerequisites` or `chore(prettier): format markdown`.
- PRs: include a concise description, scope (files/sections touched), screenshots for visual changes, and any follow-ups. Ensure `npx prettier --check .` passes.
- Small, focused PRs are preferred; link related issues or workshop tasks when applicable.

### Security & Configuration Tips

- Do not commit credentials or private API keys. `deck.md` may contain public IDs only.
- Keep large binaries out of the repo; link externally if needed.
- If adding third-party assets, confirm license and attribution in the doc where used.

### Maintainers & Support

- For structure changes (new sections, directories), propose via PR first.
- Questions: open an issue with context, intended outcome, and example snippets.
