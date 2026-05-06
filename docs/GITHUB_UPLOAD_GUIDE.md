# GitHub へのアップロード完全ガイド

このドキュメントでは、Job Compass プロジェクトを GitHub にアップロードする手順を説明します。

---

## 📋 前提条件

以下がインストール済みであることを確認してください：

```bash
# Git がインストール済みか確認
git --version

# Node.js がインストール済みか確認
node --version
npm --version
```

未インストールの場合：
- **Git**: https://git-scm.com/
- **Node.js**: https://nodejs.org/

---

## 🔑 Step 1: GitHub アカウント設定

### 1.1 GitHub に登録（未登録の場合）

```
https://github.com に アクセス
→ 「Sign up」をクリック
→ メールアドレス・パスワード設定
→ メール確認完了
```

### 1.2 GitHub Personal Access Token を生成

現在の GitHub では **Password 認証が廃止**されているため、Personal Access Token が必要です。

```
1. https://github.com/settings/tokens に アクセス
2. 「Generate new token」をクリック
3. 「Generate new token (classic)」を選択
4. Token 説明: "Job Compass MVP"
5. 有効期限: 90 days または No expiration
6. Scopes を選択:
   ☑ repo (すべてを選択)
   ☑ workflow
7. 「Generate token」をクリック
8. Token をコピーしておく（今後使用）
```

---

## 🔧 Step 2: Git の初期設定

**初めて Git を使用する場合のみ**

```bash
# ユーザー名設定
git config --global user.name "Your Name"

# メールアドレス設定
git config --global user.email "your-email@example.com"

# 設定確認
git config --global --list
```

---

## 📁 Step 3: ローカルプロジェクト構成

Job Compass プロジェクトのフォルダ構成を以下のようにしてください：

```
crowdworks/（プロジェクトフォルダ）
├── README.md
├── .gitignore
├── docs/
│   ├── Job_Compass_Design.md
│   ├── MVP_IMPLEMENTATION_GUIDE.md
│   ├── GOOGLE_APPS_SCRIPT_CODES.md
│   ├── MVP_DAILY_CHECKLIST.md
│   └── GITHUB_UPLOAD_GUIDE.md
├── src/
│   └── （後で追加）
├── .github/
│   └── ISSUE_TEMPLATE/
│       └── FEATURE_REQUEST.md
└── LICENSE（オプション）
```

### 3.1 フォルダ構成作成

```bash
# プロジェクトフォルダを作成（未作成の場合）
mkdir crowdworks
cd crowdworks

# docs フォルダを作成
mkdir -p docs .github/ISSUE_TEMPLATE src

# すべてのドキュメントを docs に配置
# MVP_IMPLEMENTATION_GUIDE.md → docs/
# GOOGLE_APPS_SCRIPT_CODES.md → docs/
# MVP_DAILY_CHECKLIST.md → docs/
# Job_Compass_Design.md → docs/
```

---

## 📝 Step 4: README.md を作成

`crowdworks/README.md` を以下の内容で作成：

```markdown
# Job Compass

## 概要

クラウドワークス初心者向けの案件分析ツール。AIを活用して、安全で効率的な案件選びをサポートします。

## 特徴

- **スコアリング機能**: 案件を100点満点で評価
- **地雷案件チェック**: AIが危険な案件を自動検出
- **応募文自動生成**: テンプレート付き
- **ジャンル別分析**: 相場情報を可視化
- **月5万円シミュレーター**: 目標達成の現実性を判定

## プロジェクト構成

```
docs/
├── Job_Compass_Design.md           # 完全設計書
├── MVP_IMPLEMENTATION_GUIDE.md     # 実装ガイド（2週間で完成）
├── GOOGLE_APPS_SCRIPT_CODES.md     # JavaScript コード集
├── MVP_DAILY_CHECKLIST.md          # 日ごとのチェックリスト
└── GITHUB_UPLOAD_GUIDE.md          # このファイル
```

## クイックスタート

### MVP（Googleスプレッドシート版）を開始する

1. `docs/MVP_IMPLEMENTATION_GUIDE.md` を読む
2. Googleスプレッドシートを新規作成
3. Day 1 のタスクを実行開始

```bash
# ガイドを読む
cat docs/MVP_IMPLEMENTATION_GUIDE.md
```

### 実装について

#### Phase 0: Googleスプレッドシート版（2週間）
- ノーコード・ローコードで仮説検証
- ユーザーフィードバック収集
- MVP テスト実施

#### Phase 1: Webアプリ化（4-6週間）
- Next.js + React でフロント構築
- Node.js + Express でバック構築
- PostgreSQL でデータ管理
- Claude API で AI機能実装

## ドキュメント

- **設計書**: `docs/Job_Compass_Design.md`
  - プロジェクト全体の詳細設計
  - 機能仕様書
  - ユーザーペルソナ
  - 収益化戦略

- **実装ガイド**: `docs/MVP_IMPLEMENTATION_GUIDE.md`
  - Googleスプレッドシート版の実装方法
  - 2週間スケジュール
  - ステップバイステップの手順

- **コード集**: `docs/GOOGLE_APPS_SCRIPT_CODES.md`
  - JavaScript コード
  - 関数実装例
  - 使用方法

- **チェックリスト**: `docs/MVP_DAILY_CHECKLIST.md`
  - 日ごとのタスク
  - テスト方法
  - 成功指標

## ターゲット

- クラウドワークス初心者
- 副業初心者
- 月5万円の副業収入を目指す人

## ユーザーペルソナ

1. **副業初心者の会社員** - 平日は忙しい、土日は自由
2. **主婦・主夫** - ブランク明けで自信がない
3. **フリーランス志望の学生** - スキル習得と稼ぎを両立したい
4. **AI活用に興味がある企業員** - ChatGPT/Claude で副業
5. **失業中の人** - 月10万円を稼ぎたい

## 主な機能

### MVP（Googleスプレッドシート版）
- ✓ ジャンル別分析
- ✓ スコアリング機能（100点満点）
- ✓ 地雷案件チェック
- ✓ 応募文テンプレート（6種類）
- ✓ 月5万円シミュレーター
- ✓ ダッシュボード（KPI表示）

### Phase 1（Webアプリ版）で追加
- ユーザー認証（Google ログイン）
- 応募文AI自動生成（Claude API）
- 応募履歴管理
- 進捗追跡
- 実績管理

## 技術スタック

### MVP（Googleスプレッドシート版）
- Google スプレッドシート
- Google Apps Script（JavaScript）

### Phase 1（Webアプリ版）予定
- **フロント**: Next.js 14 + React 18 + Tailwind CSS
- **バック**: Node.js + Express
- **DB**: PostgreSQL + Prisma
- **認証**: NextAuth.js
- **AI**: Claude API
- **ホスティング**: Vercel + Render

## 開発ロードマップ

### Week 1-2: MVP 作成
- [ ] Googleスプレッドシート版完成
- [ ] ユーザーテスト実施（10人）
- [ ] フィードバック反映

### Week 3-4: Webアプリ化
- [ ] 環境構築
- [ ] API開発
- [ ] フロント開発

### Week 5-6: スケーリング
- [ ] AI機能追加
- [ ] パフォーマンス最適化
- [ ] セキュリティ監査

### Month 2-3: マーケティング
- [ ] 有料版リリース準備
- [ ] ユーザー獲得
- [ ] PR活動

## 使用方法

### 1. MVP を試す

```bash
# リポジトリをクローン
git clone https://github.com/[あなたのユーザー名]/crowdworks.git
cd crowdworks

# ドキュメントを読む
cat docs/MVP_IMPLEMENTATION_GUIDE.md
```

### 2. Googleスプレッドシート版を開始

1. [Googleスプレッドシート](https://sheets.google.com) にアクセス
2. 新規スプレッドシート作成
3. `docs/MVP_IMPLEMENTATION_GUIDE.md` のDay 1 タスクを実行

### 3. フィードバック・改善提案

Issues や Pull Request で、改善提案やバグ報告をお待ちしています。

## FAQ

### Q: どのくらいの期間で完成する？

A: MVP（Googleスプレッドシート版）は2週間で完成します。
Webアプリ化は4-6週間の予定です。

### Q: プログラミングできないけど使える？

A: はい！MVP は Googleスプレッドシート版なので、
プログラミング知識は不要です。
Webアプリ版から本格的な開発が始まります。

### Q: 本当に月5万円稼げる？

A: 正しい案件選びができれば、可能性は十分あります。
設計書に詳細な分析が記載されています。

### Q: 貢献できる？

A: はい！Issues や Pull Request で貢献できます。
詳細は CONTRIBUTING.md を参照してください（準備中）。

## ライセンス

このプロジェクトは MIT ライセンスの下で公開されています。
詳細は LICENSE ファイルを参照してください。

## 連絡先

- Twitter: [@not_job_compass](https://twitter.com/) （準備中）
- Email: contact@jobcompass.dev （準備中）
- Issues: https://github.com/[あなたのユーザー名]/crowdworks/issues

## 謝辞

- クラウドワークス初心者の皆様へ
- フィードバックをくださるすべてのユーザーへ

---

**開発を始めましょう！** 🚀
```

---

## 🔐 Step 5: .gitignore を作成

`crowdworks/.gitignore` を以下の内容で作成：

```
# Node.js
node_modules/
npm-debug.log
yarn-error.log
.pnpm-debug.log

# IDE
.vscode/
.idea/
*.swp
*.swo
*~
.DS_Store

# Environment
.env
.env.local
.env.*.local

# Build
dist/
build/
*.tsbuildinfo

# Cache
.cache/
.eslintcache

# Logs
logs/
*.log

# OS
Thumbs.db

# Temporary files
temp/
tmp/
*.tmp

# Next.js
.next/
out/

# Prisma
prisma/dev.db
prisma/dev.db-journal

# Phase 1 関連ファイル（MVP では不要）
# src/
# public/
```

---

## 🚀 Step 6: GitHub にアップロード

### 6.1 ローカルで Git 初期化

```bash
# プロジェクトフォルダに移動
cd crowdworks

# Git リポジトリを初期化
git init

# すべてのファイルをステージ
git add .

# 初回コミット
git commit -m "Initial commit: Job Compass project setup

- Add comprehensive project documentation
- Add MVP implementation guide
- Add Google Apps Script code collection
- Add daily checklist for 2-week development
- Add GitHub upload guide
- Setup project structure"

# Git の状態確認
git status
```

### 6.2 GitHub に新規リポジトリを作成

```
1. https://github.com/new にアクセス
2. Repository name: crowdworks
3. Description: AI-powered job analyzer for Crowdworks beginners
4. Public / Private: Public 推奨（オープンソース）
5. README: チェック不要（ローカルで作成済み）
6. .gitignore: 選択不要（ローカルで作成済み）
7. License: MIT 推奨
8. 「Create repository」をクリック
```

### 6.3 リモートリポジトリを設定

```bash
# リモートリポジトリを追加
git remote add origin https://github.com/[あなたのユーザー名]/crowdworks.git

# ブランチ名を main に変更（デフォルトが master の場合）
git branch -M main

# リモートにプッシュ
git push -u origin main
```

### 6.4 Personal Access Token を使用する場合

```bash
# パスワード入力時に Token を使用
git push -u origin main

# パスワード入力（ターミナルで表示）
Username: [あなたのGitHubユーザー名]
Password: [Personal Access Token をペースト]
```

---

## ✅ Step 7: GitHub でのアップロード確認

```
1. https://github.com/[あなたのユーザー名]/crowdworks にアクセス
2. ファイルが正しくアップロードされているか確認
   - README.md が表示されている ✓
   - docs/ フォルダが表示されている ✓
   - .gitignore が表示されている ✓
3. コミットログが表示されている ✓
```

---

## 📋 Step 8: GitHub を活用する

### Issue テンプレート作成

`.github/ISSUE_TEMPLATE/FEATURE_REQUEST.md` を作成：

```markdown
---
name: Feature Request
about: Suggest an idea for this project
title: '[FEATURE] '
labels: 'enhancement'
assignees: ''

---

## 説明

このフィーチャーについて簡潔に説明してください。

## 目的

なぜこの機能が必要なのか説明してください。

## 想定される利用例

具体的な使用例を提供してください。

## 代替案

検討した代替案があれば説明してください。

## 追加のコンテキスト

その他の背景情報を追加してください。
```

### GitHub Pages で ドキュメント公開（オプション）

```bash
# docs フォルダを GitHub Pages のソースに設定
# Settings → Pages → Source: docs/

# ドキュメントが自動的に公開される
# https://[あなたのユーザー名].github.io/crowdworks で アクセス可能
```

---

## 🔄 今後の更新方法

### コードを更新してプッシュ

```bash
# ファイルを編集

# 変更をステージ
git add .

# コミット
git commit -m "Update: [変更内容]"

# プッシュ
git push origin main
```

### ブランチを使用して開発

```bash
# 新しいブランチを作成
git checkout -b feature/webapp-phase1

# ファイルを編集

# コミット
git commit -m "Add: Webアプリ用の基本設定"

# ブランチをプッシュ
git push origin feature/webapp-phase1

# GitHub で Pull Request を作成
```

---

## 🆘 トラブルシューティング

### エラー: "Authentication failed"

**原因**: Personal Access Token の期限切れまたは間違い

**解決**:
```bash
# キャッシュをクリア
git credential-osxkeychain erase
# （Windows: git credential-manager erase）

# 再度 git push を実行
git push -u origin main
```

### エラー: "fatal: refusing to merge unrelated histories"

**原因**: ローカルと リモートの履歴が異なる

**解決**:
```bash
git pull origin main --allow-unrelated-histories
git push -u origin main
```

### ファイルが大きすぎてアップロード できない

**原因**: 100MB を超えるファイル

**対策**:
- 大きなファイルは .gitignore に追加
- Git LFS（Large File Storage）を使用
- Markdown に変換

---

## 📊 GitHub リポジトリの最適化

### 1. README を充実させる

- プロジェクト説明
- クイックスタート
- 機能一覧
- 技術スタック
- 開発ロードマップ

### 2. Issues を活用

- バグ報告
- 機能リクエスト
- ディスカッション

### 3. Wiki を設定（オプション）

```
Settings → Wiki → Create the first page
```

### 4. GitHub Actions で CI/CD を設定（Phase 1）

```yaml
# .github/workflows/test.yml
name: Tests

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-node@v2
      - run: npm install
      - run: npm test
```

---

## 🎯 公開後の PR 戦略

### 1. Twitter で告知

```
🚀 Job Compass MVP がついにGitHubで公開！

クラウドワークス初心者向けの案件分析ツール

✨ 特徴
- スコアリング機能（100点満点）
- 地雷案件チェック
- 応募文テンプレート
- 月5万円シミュレーター

📍 https://github.com/[username]/crowdworks

2週間で完成する実装ガイド付き！
```

### 2. クラウドワークス コミュニティで紹介

- 初心者向けコミュニティ
- ツール紹介コーナー
- 相互フォロー推奨

### 3. はてなブックマーク / Qiita に記事投稿

「クラウドワークス初心者が陥る罠と、それを避けるための AI ツール」

---

## 📝 チェックリスト - 全体

```
□ Git がインストール済み
□ GitHub アカウント作成
□ Personal Access Token 生成
□ ローカルプロジェクト構成作成
□ README.md 作成
□ .gitignore 作成
□ Git 初期化＆初回コミット
□ GitHub に新規リポジトリ作成
□ リモートリポジトリ設定
□ git push 実行
□ GitHub でアップロード確認
□ Issue テンプレート作成
□ Twitter で告知（オプション）
□ クラウドワークス コミュニティで紹介（オプション）
```

---

## 🚀 次のステップ

```
1. GitHub にアップロード完了
2. フィードバックを集める
3. MVP（Googleスプレッドシート版）を2週間で完成
4. Phase 1（Webアプリ化）を開始
5. ユーザーを増やす
6. 有料版をリリース
```

---

**これで、Job Compass は GitHub で公開される準備が整いました！** 🎉
