# GitBook Setup

このドキュメントはGitBookを使用して構築されています。GitBookは高品質なドキュメントを簡単に作成・維持できるドキュメントプラットフォームです。

## バージョン情報

GitBook CLI バージョン 3.2.3 を使用しています。これはGitBook CLIツールの最後の安定版です。GitBookはその後SaaSモデルに移行しましたが、CLIは自己ホスト型ドキュメントのために広く使用されています。

## インストール

GitBook CLIをインストールし、ドキュメントをローカルでセットアップするには、以下の手順に従ってください：

### 前提条件

- [Node.js](https://nodejs.org/) (v10.x または v12.x 推奨、新しいバージョンはGitBook CLIとの互換性に問題がある場合があります)
  - v10.24.1は快適に動作することを保証します
- npm (Node.jsに付属)

### GitBook CLIのインストール

```bash
# GitBook CLIをグローバルにインストール
npm install -g gitbook-cli@2.3.2

# インストールの確認
gitbook --version
# 表示されるはず: CLI version: 2.3.2 および GitBook version: 3.2.3
```

### リポジトリのクローン

```bash
git clone https://github.com/sunriselayer/docs.git
cd docs
```

### 依存関係のインストール

```bash
# package.jsonから依存関係をインストール
npm install

# GitBookプラグインのインストール
gitbook install
```

## ローカルサーバーの起動

ドキュメントをローカルでプレビューするには：

```bash
# GitBookサーバーを起動
gitbook serve

# ポートを指定する場合
gitbook serve --port 4000
```

ドキュメントは `http://localhost:4000` (または指定したポート) で利用可能になります。

## 静的ファイルのビルド

本番デプロイメント用の静的ファイルをビルドするには：

```bash
# ブックをビルド
gitbook build

# 出力は_bookディレクトリに配置されます
```

## 設定

GitBookの設定は `book.json` ファイルに保存されており、プラグイン、テーマ設定、その他の設定が定義されています。

### 現在の設定

現在のプロジェクトでは、以下の `book.json` 設定を使用しています：

```json
{
  "plugins": [
    "page-treeview",
    "atoc",
    "hints",
    "tabs",
    "tabs2",
    "katex"
  ],
  "pluginsConfig": {
    "page-treeview": {
      "copyright": ""
    }
  }
}
```

### プラグインの説明

- **page-treeview**: ページ内の見出し構造をツリービューとして表示します
- **atoc**: 自動的に目次を生成します
- **hints**: ヒント、警告、情報などの注意書きを追加するためのブロックを提供します
- **tabs**: タブ付きコンテンツを作成できます
- **tabs2**: 追加のタブ機能を提供します
- **katex**: 数学式のレンダリングに KaTeX を使用します

## ディレクトリ構造

```
.
├── book.json           # GitBook設定
├── README.md           # ドキュメントのホームページ
├── SUMMARY.md          # ドキュメントの構造/サイドバー
├── learn/              # 学習リソース
│   ├── README.md       # セクションの概要ページ
│   └── ...
├── build/              # ビルド手順
├── node/               # ノードガイド
└── ...
```

## トラブルシューティング

GitBook CLIで問題が発生した場合：

1. **エラー: 'ebook-convert'のインストールが必要です**:
   - これはPDF/ePubファイルを生成する場合にのみ必要です
   - Calibreを https://calibre-ebook.com/download からインストールしてください

2. **新しいNode.jsバージョンでのエラー**:
   - nvmを使用してNode.js v12.xに切り替えることを検討してください
   - 代替手段: Dockerを使用してコンテナでGitBookを実行する

3. **gitbook serve中のENOENTエラー**:
   - `_book` および `.gitbook` ディレクトリを削除して再実行してみてください

## 貢献

ドキュメントに貢献する際は：

1. 変更用の新しいブランチを作成する
2. 編集を行う
3. `gitbook serve` でローカルでテストする
4. 変更をコミットしてプルリクエストを作成する

マージ後、CI/CDパイプラインが自動的にドキュメントの変更をビルドしてデプロイします。