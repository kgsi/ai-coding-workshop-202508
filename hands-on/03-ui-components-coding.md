# 003-ui-components-coding: コンポーネントの再現・画面実装

Figma のデザインデータを MCP（Model Context Protocol）対応ツールから取得し、AI によるコーディングを品質高く進める演習です。まずは Figma MCP 単独での連携を体験し、次に Figma MCP とデザインシステム MCP（以下 DS MCP）を併用して、設計トークン/コンポーネント規約に沿った実装へ発展させます。

## 目的

- Figma MCPとSmartHR UI ComponentのMCPを併用して、デザインシステムのトークンとコンポーネント規約に準拠したコード生成を実現します。
- コンポーネントがすでに用意されているような大規模設計においては、コンポーネントを使い、画面構築することがほとんどです。
- MCPをただ利用するだけでは、コンポーネントと判断できず、AIが独自実装してしまうことも少なくありません。
- そのため、Figma MCPを通して画面情報を取得し再現を試みつつ、別で用意したUIコンポーネントの情報を取得するMCPサーバーを利用することで、忠実な再現を試みます。

### 参考

- [社内デザインシステムをMCPサーバー化したらUI実装が爆速になった](https://zenn.dev/ubie_dev/articles/f927aaff02d618)
- [Figma MCPとCode Connectで実装効率を向上させる方法](https://buildersbox.corp-sansan.com/entry/2025/07/23/100000)
  - この中で`Figma Code Connect`が使われているが、利用はビジネスプランとエンタープライズプランのみなので、今回は割愛します。

## 所要時間 / 成果物

- 所要時間: 15〜20 分
- 成果物:
  - Next.js アプリ雛形（App Router）のセットアップ
  - Figma MCPとSmartHR UI ComponentのMCPを併用して、デザインシステムのトークンとコンポーネント規約に準拠したコード生成を実現

## 教材

- [実演・教材用Figmaファイル（.fig）](https://drive.google.com/file/d/1mPtndp0TVcwwNb1mrjj-pASIGsdNm6MU/view?usp=sharing)
  - ダウンロードしてお手元にコピーしてください。
  - `ui-layout`、`hero-mobile`、`lp-site`の3つを使います。

## セットアップ

### Next.jsアプリ雛形の作成

[02-coding.md](02-coding.md)で作成したNext.jsアプリ雛形をそのまま使用しても問題ありません。

```
npx create-next-app@latest workshop-starter-ui --typescript --eslint --app
```

### SmartHR UI をインストール

このハンズオンではUIコンポーネントに[SmartHR UI](https://smarthr-ui.com/)を使用します。

```
npm install smarthr-ui
```

#### [Tips]SmartHR UIを選定した理由

- オープンソースで無料で使用できるUIコンポーネントで、業務アプリケーションの活用に適している
- ドキュメントが公式サイトで手厚く揃っている
- 講師がSmartHR UIを使用しているので、ハンズオンでも使用するのが楽

### UIコンポーネントを動作させるページを作成

- SmartHR UIを使えるページを作成します。
- `app/layout.tsx`の先頭に以下のコードを貼り付けてください。

```jsx
import "smarthr-ui/smarthr-ui.css";
```

- `app/ui-coding/page.tsx`にページを作成して、以下のコードを貼り付けてください。
- Buttonだけ表示されたら成功です。

```jsx
"use client";

import { Button, ThemeProvider, createTheme, IntlProvider } from "smarthr-ui";

const theme = createTheme();

export default function UICodingPage() {
  return (
    <IntlProvider locale="ja">
      <ThemeProvider theme={theme}>
        <Button>ボタンラベル</Button>
      </ThemeProvider>
    </IntlProvider>
  );
}
```

### SmartHR UI用 MCPサーバのインストール

- [smarthr-ui-mcp-server](https://github.com/kgsi/smarthr-ui-mcp-server)
  - SmartHR UIのMCPサーバーを使用することで、SmartHR UIのコンポーネントをMCP経由で取得できます。
- 各ツールエディタでMCPサーバーの起動を確認してください。
- なお、当MCPサーバーは講師個人で管理作成しているもので、ワークショップ後の利用は自己責任でお願いします。

```
# リポジトリをクローン
gh repo clone kgsi/smarthr-ui-mcp-server

# ディレクトリを作成
mkdir smarthr-ui-mcp-server
cd smarthr-ui-mcp-server

# 依存パッケージをインストール
npm install

# サーバーをビルド
 npm run build

# MCPサーバーを起動
npm run start
```

## 実装ケース（画面やコンポーネント配置の再現）

- コンポーネント情報取得用MCPを起動しつつ、FigmaファイルをMCP経由で読み込んで、デザインを忠実に再現してみましょう。

### 教材

- https://www.figma.com/community/file/978607227374353992/smarthr-ui

### やりかた

基本的なデザインの再現をしてみましょう。これも一度に全部渡すのではなく、部分部分で指示していきましょう。

```text:sample-prompt
@app/page.tsxに以下FigmaファイルをMCP経由で読み込んで、デザインを忠実に再現して。

{DevモードでコピーしたFigmaの参照リンク}
```

### ポイント

- 実際のコンポーネント名と、Figma上での名前を極力揃えていることで、画面とコンポーネントの一致確率を高められます。
- Figma上のコンポーネントが解除されていると、コンポーネントを使う確率が極端に下がり、精度が甘くなります。
  - そのため、コンポーネントは極力解除せずに使うことがおすすめですが、解除しないと使えないことも多々あります。
- `CLAUDE.md`や`AGENTS.md`などの指示書への記述はもちろん、デザインシステムのドキュメントを参照するやり方もより精度を上げれます。
