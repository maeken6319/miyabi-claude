# miyabi-claude

Miyabi自律型開発フレームワークのテストプロジェクト

## 概要

このプロジェクトは、[Miyabi](https://github.com/ShunsukeHayashi/Miyabi)フレームワークを使用した自律型開発環境のデモンストレーションです。AIエージェントによる自動的なIssue処理、コード生成、PR作成を実現します。

## 特徴

- 🤖 **6つのAIエージェント** - Issue分析からデプロイまで自動化
- 📊 **ラベルベース状態管理** - 53個のラベルで進捗を可視化
- 🔄 **自動Issue→PRパイプライン** - 手動コーディング不要
- 🕷️ **Water Spider Agent** - システム全体を巡回監視

## インストール

### 前提条件

- Node.js v18以上
- Git
- GitHub CLI (`gh`)
- GitHub アカウント

### セットアップ

1. **リポジトリをクローン**

```bash
git clone https://github.com/maeken6319/miyabi-claude.git
cd miyabi-claude
```

2. **GitHub認証**

```bash
gh auth login
```

3. **環境変数を設定**

`.env`ファイルを作成：

```bash
GITHUB_TOKEN=$(gh auth token)
```

オプション（AI機能を使用する場合）：

```bash
ANTHROPIC_API_KEY=your_api_key_here
```

## 基本的な使い方

### ステータス確認

```bash
npx miyabi status
```

または、ラッパースクリプトを使用：

```bash
./run-miyabi.sh status
```

### Issueを作成

```bash
gh issue create --title "タスクのタイトル" --body "タスクの説明"
```

### エージェントを実行

**Issue分析：**
```bash
./run-miyabi.sh agent run issue -i <issue番号>
```

**コード生成：**
```bash
./run-miyabi.sh agent run codegen -i <issue番号>
```

**全体調整：**
```bash
./run-miyabi.sh agent run coordinator -i <issue番号>
```

### 自動モード

システムを自動監視させる：

```bash
./run-miyabi.sh auto
```

ドライラン（シミュレーション）：

```bash
./run-miyabi.sh auto --dry-run
```

## プロジェクト構造

```
miyabi-claude/
├── .claude/              # Claude Code設定
│   ├── agents/          # AIエージェント定義
│   ├── commands/        # カスタムコマンド
│   └── settings.json    # 設定ファイル
├── .github/
│   └── workflows/       # GitHub Actions（14個のワークフロー）
├── run-miyabi.sh        # Miyabi実行用ラッパースクリプト
├── CLAUDE.md            # Claude Codeコンテキストファイル
└── README.md            # このファイル
```

## 利用可能なエージェント

- **coordinator** - タスク統括・並列実行制御
- **codegen** - コード生成
- **review** - コード品質チェック
- **issue** - Issue分析・ラベリング
- **pr** - Pull Request管理
- **deploy** - デプロイ自動化
- **mizusumashi** - Water Spider Agent（巡回監視）

## ラベル体系

プロジェクトは53個のラベルで状態管理されます：

### 状態ラベル
- 📥 `state:pending` - 処理待ち
- 🔍 `state:analyzing` - 分析中
- 🏗️ `state:implementing` - 実装中
- 👀 `state:reviewing` - レビュー中
- ✅ `state:done` - 完了

### タイプラベル
- 🐛 `type:bug` - バグ修正
- ✨ `type:feature` - 新機能
- 📚 `type:docs` - ドキュメント
- ♻️ `type:refactor` - リファクタリング

### 優先度ラベル
- 📊 `priority:P0-Critical` - 最優先
- ⚠️ `priority:P1-High` - 高優先度
- 📊 `priority:P2-Medium` - 中優先度
- 📊 `priority:P3-Low` - 低優先度

## トラブルシューティング

### GITHUB_TOKENエラー

```bash
# GitHub CLIのトークンを使用
export GITHUB_TOKEN=$(gh auth token)
```

または、`.env`ファイルに追加してください。

### システムヘルスチェック

```bash
npx miyabi doctor
```

## 参考リンク

- [Miyabi公式リポジトリ](https://github.com/ShunsukeHayashi/Miyabi)
- [Miyabi npm package](https://www.npmjs.com/package/miyabi)
- [GitHub Issues](https://github.com/maeken6319/miyabi-claude/issues)

## 開発状況

現在の状態はGitHub Issuesページで確認できます：
https://github.com/maeken6319/miyabi-claude/issues

---

**Miyabi** - Beauty in Autonomous Development
