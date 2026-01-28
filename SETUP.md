# 開発環境セットアップ

<!--
📖 このファイルについて
========================
実務で必須となる開発環境のセットアップ手順を説明するドキュメントです。
自動セットアップと手動セットアップの両方を用意しています。
-->

## 🚀 自動セットアップ（オプション）

```bash
bash scripts/setup.sh
# ↑ スクリプトで自動インストール
#   Node.js, Gemini CLI, GitHub CLI, mmcp を一括セットアップ
```

> 手動でインストールする場合は下記を参照

<!--
💡 引用ブロック（>）について
===========================
> で始まる行は「引用」として表示されます。
注意書きや補足情報を目立たせるために使います。
-->

---

## 📦 手動セットアップ

### 1. Node.js（nvm経由）

<!--
💡 nvmとは？（Node Version Manager）
====================================
Node.jsのバージョンを管理するツールです。
プロジェクトごとに異なるNode.jsバージョンを使い分けられます。
-->

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash
# ↑ curlコマンドでnvmのインストールスクリプトを取得し、bashで実行
#   curl: URLからデータを取得するコマンド
#   -o-: 出力を標準出力へ（ファイルに保存しない）
#   | bash: 取得したスクリプトをbashで実行

source ~/.bashrc
# ↑ bashの設定ファイルを再読み込み
#   nvmコマンドを現在のターミナルで使えるようにする
#   ※ Zshの場合は source ~/.zshrc

nvm install --lts
# ↑ Node.jsのLTS（長期サポート）版をインストール
#   --lts: Long Term Support版（安定版、本番環境推奨）
```

### 2. Gemini CLI（無料）

<!--
💡 Gemini CLIとは？
==================
GoogleのAI「Gemini」をコマンドラインから使うツールです。
ターミナル上でAIにコードの質問や作成を依頼できます。
-->

```bash
npm install -g @google/gemini-cli
# ↑ npm (Node Package Manager) でGemini CLIをインストール
#   npm: Node.jsのパッケージ管理ツール
#   install: パッケージをインストール
#   -g: グローバルインストール（システム全体で使用可能）
#       -gなしだと現在のプロジェクト内のみにインストール
#   @google/gemini-cli: パッケージ名（@組織名/パッケージ名の形式）
```

> **APIキー不要** - 初回起動時にGoogleアカウントでログインするだけで利用可能

### 3. GitHub CLI

<!--
💡 GitHub CLIとは？
==================
GitHubをコマンドラインから操作できるツールです。
リポジトリ作成、Issue管理、PR作成などをターミナルから実行できます。
-->

```bash
# Linux/WSL2の場合
sudo apt install gh
# ↑ sudo: 管理者権限でコマンドを実行
#   apt: Debian/Ubuntu系Linuxのパッケージマネージャー
#   install: パッケージをインストール
#   gh: GitHub CLIのパッケージ名

# Macの場合
brew install gh
# ↑ brew: macOS用パッケージマネージャー（Homebrew）
#   Homebrewを使ってインストール

# 認証（初回のみ）
gh auth login
# ↑ GitHubアカウントとCLIを連携
#   ブラウザが開いてGitHubにログインを求められます
#   認証後、ghコマンドでGitHub操作が可能になります
```

### 4. MCP管理ツール（オプション）

<!--
💡 MCPとは？（Model Context Protocol）
=====================================
AIツールが外部サービス(GitHub, ブラウザ, APIなど)と連携するためのプロトコルです。
mmcpはMCPサーバーの設定を管理するツールです。
-->

```bash
npm install -g mmcp
# ↑ mmcpをグローバルインストール

mmcp agents add gemini-cli
# ↑ mmcpにGemini CLIを登録
#   agents: AIエージェント（Gemini CLIなど）を管理

mmcp add context7 -- npx -y @upstash/context7-mcp
# ↑ Context7 MCPサーバーを追加
#   Context7: 最新のライブラリドキュメントを取得するサービス
#   npx: パッケージを一時的にダウンロードして実行
#   -y: 確認プロンプトに自動でyes

mmcp apply
# ↑ 設定を適用
#   各AIエージェントの設定ファイルに反映されます
```

---

## ✅ 動作確認

```bash
node --version    # v20.x.x と表示されればOK
# ↑ Node.jsのバージョンを確認

gemini --version  # Gemini CLI と表示されればOK
# ↑ Gemini CLIのバージョンを確認

gh --version      # gh version x.x.x と表示されればOK
# ↑ GitHub CLIのバージョンを確認
```

<!--
💡 コマンドの --version オプション
==================================
ほとんどのCLIツールは --version オプションでバージョンを確認できます。
インストールが成功したかどうかの確認に便利です。
エラーが出る場合はインストールに問題がある可能性があります。
-->

---

## 📝 VS Code設定（Python用）

<!--
💡 settings.jsonとは？
=====================
VS Codeの設定ファイルです。
ワークスペースごと、またはユーザー全体で設定を保存できます。
Ctrl+Shift+P → "Open Settings (JSON)" で開けます。
-->

`settings.json`:
```json
{
  "[python]": {
    "editor.formatOnSave": true,
    "editor.defaultFormatter": "charliermarsh.ruff"
  }
}
```

<!--
💡 上記設定の説明
================
"[python]": Python言語の設定
"editor.formatOnSave": true → 保存時に自動フォーマット
"editor.defaultFormatter": フォーマットに使用する拡張機能
  "charliermarsh.ruff": Ruff（高速なPythonリンター/フォーマッター）
-->

---

## 🎭 Playwright MCP（オプション）

<!--
💡 Playwright MCPとは？
======================
LLMからブラウザを操作できるMCPサーバーです。
AIにブラウザテストやWebスクレイピングを依頼できます。
-->

```bash
mmcp add playwright -- npx -y @playwright/mcp@latest
# ↑ Playwright MCPサーバーを追加
#   ブラウザ操作をAIに委譲できるようになります

mmcp apply
# ↑ 設定を適用
```

> 使用例: Gemini CLIで「playwrightでYahoo Japanを開いて」と指示

---

## 📋 cc-sdd（仕様駆動開発ツール）

<!--
💡 cc-sdd / 仕様駆動開発とは？
============================
AIコーディングでドキュメントを重視する開発手法です。
仕様書（スペック）を先に生成し、それに基づいてコードを生成します。
Amazon Kiroと互換性があるOSSツールです。
-->

```bash
# プロジェクトディレクトリで実行
npx cc-sdd@latest --gemini --lang ja
# ↑ cc-sddをGemini CLI用にセットアップ
#   --gemini: Gemini CLI向け設定
#   --lang ja: 日本語でドキュメント生成
```

### 仕様駆動開発の流れ

```bash
# 1. 既存ファイルから初期ドキュメント生成
/kiro:steering

# 2. 新規開発の仕様を生成
/kiro:spec-init シンプルなチャットアプリ
# ↑ AIがガイドに従って仕様ドキュメントを生成

# 3. タスク実装
/kiro:spec-impl task.mdをもとに順に実装してください
```

> 生成されたドキュメントは `.kiro/steering/` に保存されます

---

## 📊 GitHub Project連携

<!--
💡 GitHub Projectとは？
======================
GitHubのプロジェクト管理機能です。
Issues、PRをカンバンやガントチャートで管理できます。
ghコマンドで操作できるためAIコーディングと相性が良いです。
-->

```bash
# GitHub Project操作の権限を追加
gh auth refresh -s project
# ↑ ghコマンドでProjectを操作するための権限を付与

# タスクをIssuesに登録（Gemini CLIで実行）
# 例: @tasks.md をGitHubのissueにghコマンドで登録してください

# スケジュール設定（Gemini CLIで実行）
# 例: すべてのissuesにStart dateとTarget dateを設定してください
#     プロジェクトURL: https://github.com/users/xxx/projects/xxx/
```

---

## 🔍 AIコードレビュー

<!--
💡 AIコードレビューについて
==========================
コード生成が高速化した分、レビューの重要性が増しています。
AIを「レビュワーの追加」として活用し、抜け漏れを防止します。
-->

### GitHub Copilotでレビュー

PRを開くとGitHub Copilotが自動でレビューコメントを付けます。
設定方法: https://docs.github.com/ja/copilot/using-github-copilot/code-review

### Gemini CLIでレビュー

```bash
# Gemini CLI上で実行
以下のPull Requestをレビューしてください
https://github.com/xxx/xxx/pull/1
```

> **推奨**: 複数のAIツールで多角的にレビューすることで品質向上

---

## 📚 参考リンク

- [AIコーディング実践環境の構築方法【2025年12月】](https://zenn.dev/mkj/articles/bf59c4c86d98a8) - 参考記事
- [TIS株式会社 AIコーディングガイドライン](https://github.com/Fintan-contents/gai-dev-guide)
- [cc-sdd公式ドキュメント](https://github.com/karaage0703/cc-sdd)
- [Best Practices for AI Coding](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering)
