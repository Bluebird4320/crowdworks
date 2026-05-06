# 📤 既存リポジトリへのファイルプッシュガイド

GitHub の既存リポジトリ（`crowdworks`）にファイルをプッシュするための手順です。

---

## 🔧 セットアップ手順

### ステップ1：ローカルでリポジトリをクローン

```bash
# リポジトリをクローン
git clone https://github.com/Bluebird4320/crowdworks.git
cd crowdworks

# ブランチ確認
git branch -a
```

### ステップ2：必要なフォルダを作成

```bash
# プロジェクト用のフォルダ構造を作成
mkdir -p docs
mkdir -p phase0-google-sheets
mkdir -p phase1-webapp/{next.js-frontend,express-backend,database}
mkdir -p .github/workflows
mkdir -p .github/ISSUE_TEMPLATE
mkdir -p tests/{unit,integration}
mkdir -p design/wireframes

# フォルダが作成されたか確認
ls -la
```

### ステップ3：ファイルをコピー

ダウンロードした以下のファイルをリポジトリのルートにコピーしてください：

```bash
# ルートディレクトリにコピー
cp 00_START_HERE.md crowdworks/
cp README.md crowdworks/
cp GITHUB_SETUP_GUIDE.md crowdworks/docs/
cp phase0-setup-guide.md crowdworks/docs/
cp phase1-webapp-guide.md crowdworks/docs/
cp IMPLEMENTATION_CHECKLIST.md crowdworks/docs/
cp FEATURE_REQUEST_TEMPLATE.md crowdworks/.github/ISSUE_TEMPLATE/
cp LICENSE crowdworks/
cp .gitignore crowdworks/

# 確認
cd crowdworks
ls -la
```

### ステップ4：Git に追加してコミット

```bash
# ステージング
git add .

# コミット（意味のあるメッセージを付ける）
git commit -m "Initial commit: Job Compass project setup

- Add comprehensive project documentation
- Add Phase 0 MVP setup guide
- Add Phase 1 Webapp development guide
- Add implementation checklist
- Add GitHub templates and configuration"

# ログで確認
git log --oneline | head -5
```

### ステップ5：GitHub にプッシュ

```bash
# main ブランチにプッシュ
git push origin main

# または develop ブランチを使う場合
git push origin develop

# 成功確認
git log --oneline -1
```

---

## ✅ プッシュ成功の確認

### GitHub ウェブで確認

```
1. https://github.com/Bluebird4320/crowdworks にアクセス
2. ファイルが表示されているか確認
3. README.md がデフォルト表示されているか確認
```

### コマンドで確認

```bash
# リモートの状態確認
git status

# プッシュされたコミットを確認
git log --oneline --all | head -10

# リモートブランチ確認
git branch -r
```

---

## 🎯 次のステップ

### すぐにやること

```bash
# 1. GitHub Projects を作成
# → https://github.com/Bluebird4320/crowdworks/projects
# → New Project → Automation

# 2. Branch protection rule を設定
# → Settings → Branches → Add rule
#   Branch: main
#   ✓ Require a pull request before merging

# 3. 最初のユーザーテストを開始
# → phase0-setup-guide.md に従う
```

### Week 1 にやること

```bash
# Phase 0 MVP を構築
1. Google スプレッドシートを作成
2. 各シートをセットアップ
3. ダミーデータを入力
4. テストユーザー 10人を招待
```

### Week 2-3 にやること

```bash
# ユーザーテストを実施
1. テストシナリオを実行
2. フィードバックを収集
3. 改善リストを作成
4. バグ修正
```

---

## 📋 チェックリスト

- [ ] リポジトリをクローン
- [ ] フォルダ構造を作成
- [ ] ファイルをコピー
- [ ] `git add .` を実行
- [ ] コミット作成
- [ ] GitHub にプッシュ
- [ ] GitHub ウェブで確認
- [ ] README が表示されている
- [ ] GitHub Projects を作成
- [ ] Branch protection を設定

---

## ❓ よくある質問

### Q: main ブランチでなく develop を使いたい場合は？

```bash
# develop ブランチを作成
git checkout -b develop

# ファイルを追加
git add .
git commit -m "..."

# GitHub にプッシュ
git push -u origin develop

# 確認
git branch -a
```

### Q: プッシュに失敗した場合は？

```bash
# まず最新を取得
git pull origin main

# 競合がある場合は解決
# ファイルを編集

# 再度プッシュ
git push origin main
```

### Q: コミットメッセージを修正したい場合は？

```bash
# 直前のコミットメッセージを修正
git commit --amend -m "修正されたメッセージ"

# すでにプッシュされている場合
git push --force-with-lease origin main
```

### Q: ファイルを追加し忘れた場合は？

```bash
# ステージングに追加
git add forgotten-file.md

# 直前のコミットに追加
git commit --amend --no-edit

# プッシュ（すでにプッシュ済みの場合は force）
git push --force-with-lease origin main
```

---

## 📚 参考資料

### Git コマンドチートシート

```bash
# クローン
git clone <url>

# ステータス確認
git status

# ステージング
git add .              # すべてのファイル
git add file.md        # 特定のファイル

# コミット
git commit -m "message"
git commit --amend     # 直前のコミットを修正

# プッシュ
git push origin main
git push origin develop

# プル
git pull origin main

# ログ
git log --oneline
git log --graph --all --oneline

# ブランチ
git branch              # ローカル
git branch -r           # リモート
git checkout -b name    # 新規作成
git checkout name       # 切り替え
```

### GitHub UI での操作

```
ファイルをアップロード（GUI）：
1. リポジトリページ
2. 「Add file」→「Create new file」または「Upload files」
3. ファイルを選択
4. コミットメッセージを入力
5. 「Commit changes」

※ コマンドラインの方が便利です
```

---

## 🎉 成功！

プッシュが完了したら、以下を実施してください：

1. ✅ GitHub ページで README が表示されているか確認
2. ✅ すべてのファイルが表示されているか確認
3. ✅ GitHub Projects を作成
4. ✅ Phase 0 MVP を開始（Google スプシ版）

---

**質問や問題が発生した場合は、遠慮なくお知らせください！** 🙏

次のステップ：[Phase 0 セットアップガイド](./phase0-setup-guide.md)
