# 03-mcp: Figma MCP 連携ハンズオン（単独 / デザインシステム併用）

Figma のデザインデータを MCP（Model Context Protocol）対応ツールから取得し、AI によるコーディングを品質高く進める演習です。まずは Figma MCP 単独での連携を体験し、次に Figma MCP とデザインシステム MCP（以下 DS MCP）を併用して、設計トークン/コンポーネント規約に沿った実装へ発展させます。

## 目的

- Figma MCPとSmartHR UI ComponentのMCPを併用して、デザインシステムのトークンとコンポーネント規約に準拠したコード生成を実現します。

## 所要時間 / 成果物

- 所要時間: 30 分
- 成果物:
  - Next.js アプリ雛形（App Router）のセットアップ
  - Figma MCPとSmartHR UI ComponentのMCPを併用して、デザインシステムのトークンとコンポーネント規約に準拠したコード生成を実現

```
npx create-next-app@latest workshop-starter-kit --typescript --eslint --app
```

## 前提 / 準備

- Claude Desktop（MCP クライアント）または MCP 対応エージェント環境
- Figma アカウントと個人アクセストークン（Personal Access Token）
- 対象 Figma ファイルの File Key（URL に含まれる英数 ID）
- （併用パターン用）デザインシステム MCP（トークン/コンポーネント仕様を提供する MCP サーバー）
- 本リポジトリ（AGENTS.md の品質基準を参照）

## 所要時間 / 成果物

- 所要時間: 45–70 分
- 成果物:
  - パターンA（単独）: Figma から取得した情報に基づくセマンティック HTML/CSS 骨子
  - パターンB（併用）: DS トークン反映済みの Tailwind/スタイル設定とコンポーネント実装

## 手順A: MCP サーバーの設定（Figma / DS）

1. 設定ファイルの場所（例: Claude Desktop）
   - macOS: `~/Library/Application Support/Claude/claude_desktop_config.json`
   - Windows: `%APPDATA%/Claude/claude_desktop_config.json`
   - Linux: `~/.config/Claude/claude_desktop_config.json`
2. `mcpServers` に Figma MCP / DS MCP を登録

   例（ワークショップ配布の実行コマンド名を前提）：

   ```json
   {
     "mcpServers": {
       "figma": {
         "command": "figma-mcp",
         "args": [],
         "env": {
           "FIGMA_ACCESS_TOKEN": "<your-figma-token>",
           "FIGMA_FILE_KEY": "<file-key>"
         }
       },
       "design-system": {
         "command": "ds-mcp",
         "args": [],
         "env": {
           "DS_NAME": "Acme",
           "DS_TOKENS_PATH": "/absolute/path/to/tokens.json"
         }
       }
     }
   }
   ```

3. クライアントを再起動して認識を確認（MCP ツール一覧に `figma`, `design-system` が表示されること）

注意: 実際のコマンド名や環境変数は、配布物の README に従ってください。API トークンは個人情報のため、漏洩しないように管理します。

## 手順B: パターンA（Figma MCP 単独）

目的: Figma の情報を直接取得し、静的サイトの骨子（セマンティック HTML + Tailwind クラス案）へ落とし込みます。

1. デザイン情報の取得
   - ツール例: フレーム一覧、ページ一覧、コンポーネント一覧、ノード検索、アセット書き出し（PNG/SVG）
   - 依頼テンプレ:

     ```
     目的: LP の Hero/Features/CTA をコーディングします。まず Figma から対象フレームの情報を取得してください。
     指定: ページ名/フレーム名 = "Landing/Hero"
     取得: レイアウト（幅/余白/グリッド）、テキスト（内容/サイズ/行間/ウェイト）、カラー、画像アセット
     書き出し: 画像は `public/images/` 前提、用途と alt 文言案も併記
     ```

2. セマンティック HTML 骨子の生成
   - 依頼テンプレ:

     ```
     AGENTS.md の「Web コーディング品質基準」に従い、Hero/Features/CTA を HTML 骨子化してください。
     制約: h1 はページに一つ、ランドマーク遵守、モバイルファースト、コントラスト 4.5:1 以上
     出力: section ごとに HTML と Tailwind クラスの提案、a11y 配慮点
     ```

3. 実装と確認
   - `example/index.html` または Next.js の `app/page.tsx` に反映
   - Live Preview で見た目・読み上げ・フォーカスを確認

4. 成功判定（チェックリスト）
   - 見出し階層とランドマークが妥当
   - Figma のタイポ/余白が概ね反映
   - 画像が適切な alt で表示（Hero は `priority` 相当の扱い）

## 手順C: パターンB（Figma MCP + デザインシステム MCP）

目的: DS トークン/コンポーネント規約に準拠した実装を、Figma 情報にマッピングして生成します。

1. DS トークンの登録（Tailwind or CSS 変数）
   - 依頼テンプレ:

     ```
     DS MCP から取得できる tokens.json（color/space/typography/radius/breakpoints）を確認し、
     tailwind.config.ts の theme.extend にマッピングしてください。既存クラスとの重複回避も提案。
     併せて、globals.css のベーススタイル（見出し/本文/リンク/フォーカス）を提示してください。
     ```

2. コンポーネント規約へマッピング
   - 依頼テンプレ:

     ```
     Figma の Hero/Feature セクション要素を、DS のコンポーネント（Section, Heading, Text, Button, Card）に
     対応付けてください。アクセシビリティ要件と Prop 設計（variant/size）も提案。
     出力: `@/components/*` の TSX 例と使用例（app/page.tsx の抜粋）。
     ```

3. 差分検証（Figma → DS 反映のずれ）
   - 依頼テンプレ:

     ```
     DS トークンに無い色/余白/フォントサイズの使用箇所を列挙し、近似値または新規トークン追加の提案を出してください。
     Figma の命名と DS の命名（BEM/variant）の整合性もレポートしてください。
     ```

4. 成功判定（チェックリスト）
   - Tailwind/変数に DS トークンが反映されている
   - `components/*` が DS 規約（命名/props/a11y）に従う
   - Figma との差分が整理され、追加課題が洗い出されている

## 実行方法（How to run）

- MCP 構成: 設定ファイルに `figma` と `design-system` を登録 → クライアント再起動
- 接続確認: MCP ツール一覧で両方が使用可能になっていることを確認
- アセット書き出し: 画像は `public/images/` に保存（Next.js は `public/` 直下参照）
- ページ起動（Next.js の場合）: `npm run dev` → `http://localhost:3000`

## 検証（チェックリスト）

- Figma MCP からページ/フレーム/コンポーネント情報を取得できる
- 画像/アイコンの書き出しが成功し、alt 文言案が用意できた
- セマンティック HTML + Tailwind の骨子が生成できた
- DS トークンが tailwind.config.ts/globals.css に反映された
- DS コンポーネント規約で TSX を実装し、画面で確認できた

## トラブルシュート

- 認証エラー: トークンの権限/期限、対象ファイルの閲覧権限を確認
- ツールが表示されない: MCP 設定ファイルのパス/JSON 構文/再起動を確認
- 取得結果が足りない: Figma のフレーム名/階層/公開設定を見直し、精密な指定で再実行
- DS との不整合: トークン命名の揺れを一覧化し、変換テーブル（alias）を提示して再生成

## 次へ

- 画像の最適化（WebP 化、`next/image` の `sizes`/`priority` 設計）
- コンポーネントの Storybook 化と VRT 導入
- 自動差分チェック（Figma → 実装のレグレッション検知）

補足: すべてのプロンプトで、必ず `AGENTS.md` の「Web コーディング品質基準」を冒頭に再掲し、セマンティック/アクセシビリティ/レスポンシブ要件が満たされているかを自己点検させてください。
