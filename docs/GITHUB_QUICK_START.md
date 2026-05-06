# GitHub アップロード クイックガイド

Job Compass プロジェクトを GitHub にアップロードするための最短手順です。

---

## 🚀 最速版（3ステップ）

### ステップ1: スクリプト実行

**Mac / Linux ユーザー**:
```bash
# スクリプトに実行権限を付与
chmod +x github_upload.sh

# スクリプトを実行
./github_upload.sh
```

**Windows ユーザー**:
```bash
# コマンドプロンプトで実行
github_upload.bat
```

### ステップ2: 情報入力

スクリプトから以下の情報を聞かれます：

```
GitHub ユーザー名: [あなたのGitHubユーザー名を入力]
リポジトリ名: [デフォルト: crowdworks]
```

### ステップ3: 確認＆完了

```
✓ アップロード成功！
リポジトリ URL: https://github.com/[ユーザー名]/crowdworks
```

---

## 📋 事前準備（初回のみ）

### 1. Git をインストール

- **Mac**: `brew install git`
- **Windows**: https://git-scm.com/download/win
- **Linux**: `apt install git` または `yum install git`

### 2. GitHub アカウント作成

- https://github.com に アクセス
- 「Sign up」をクリック
- メールアドレス・パスワード設定

### 3. Personal Access Token 生成

```
1. https://github.com/settings/tokens にアクセス
2. 「Generate new token (classic)」をクリック
3. Token 説明: "Job Compass"
4. Scopes: repo (すべて選択)
5. 「Generate token」をクリック
6. Token をコピーして保存（重要！）
```

---

## 🖥️ 詳細版（コマンド手動実行）

スクリプト実行が難しい場合、以下のコマンドを **順番に** 実行してください。

### 1. Git 初期設定

```bash
# ユーザー名設定
git config --global user.name "あなたの名前"

# メールアドレス設定
git config --global user.email "your-email@example.com"

# 確認
git config --global --list
```

### 2. リポジトリ初期化

```bash
# プロジェクトフォルダに移動
cd crowdworks

# Git リポジトリ初期化
git init

# ステータス確認
git status
```

### 3. ファイルをステージ

```bash
# すべてのファイルをステージ
git add .

# ステージ内容確認
git status
```

### 4. 初回コミット

```bash
git commit -m "Initial commit: Job Compass project setup

- Add comprehensive project documentation
- Add MVP implementation guide
- Add Google Apps Script code collection
- Add daily checklist for 2-week development
- Add GitHub upload guide
- Setup project structure"
```

### 5. ブランチ設定

```bash
# ブランチ名を確認
git branch

# master ブランチを main に変更（必要な場合）
git branch -M main
```

### 6. リモートリポジトリ設定

```bash
# GitHub にリポジトリを新規作成（ブラウザで）
# https://github.com/new
# Repository name: crowdworks
# Public / Private: Public
# 「Create repository」

# リモート設定
git remote add origin https://github.com/[ユーザー名]/crowdworks.git

# 確認
git remote -v
```

### 7. プッシュ

```bash
# GitHub にプッシュ
git push -u origin main

# ユーザー名・パスワード（またはToken）を入力
Username: [GitHubユーザー名]
Password: [Personal Access Token]

# プッシュ完了確認
git log --oneline
```

### 8. ブラウザで確認

```
https://github.com/[ユーザー名]/crowdworks
にアクセスしてファイルが表示されているか確認
```

---

## 🔍 よくあるエラーと解決方法

### エラー: "fatal: not a git repository"

**原因**: crowdworks フォルダに `.git` ディレクトリがない

**解決**:
```bash
cd crowdworks
git init
```

### エラー: "error: pathspec 'main' did not match"

**原因**: ブランチが `master` になっている

**解決**:
```bash
git branch -M main
git push -u origin main
```

### エラー: "fatal: could not read from remote repository"

**原因**: リモートリポジトリが設定されていない

**解決**:
```bash
git remote add origin https://github.com/[ユーザー名]/crowdworks.git
git push -u origin main
```

### エラー: "fatal: remote origin already exists"

**原因**: リモートがすでに設定されている

**解決**:
```bash
git remote remove origin
git remote add origin https://github.com/[ユーザー名]/crowdworks.git
git push -u origin main
```

### エラー: "403 Forbidden" または "Invalid credentials"

**原因**: Personal Access Token が無効または期限切れ

**解決**:
```bash
# 認証キャッシュをクリア
git credential-osxkeychain erase
# （Windows: git credential-manager erase）

# 新しい Token で再入力
git push -u origin main
```

---

## ✅ アップロード完了チェック

ブラウザで `https://github.com/[ユーザー名]/crowdworks` にアクセスして、以下を確認：

```
✓ README.md が表示されている
✓ docs/ フォルダが表示されている
✓ .gitignore が表示されている
✓ 複数のコミットが表示されている（git log）
✓ 「main」ブランチが表示されている
```

---

## 🔄 今後の更新手順

### ファイルを編集した後

```bash
# ファイルをステージ
git add .

# コミット
git commit -m "Update: [変更内容を簡潔に記述]"

# プッシュ
git push origin main
```

### ブランチを分けて開発する場合

```bash
# 新しいブランチを作成
git checkout -b feature/webapp-phase1

# ファイルを編集

# コミット
git commit -m "Add: Webアプリの基本設定"

# ブランチをプッシュ
git push origin feature/webapp-phase1

# GitHub で Pull Request を作成
```

---

## 📚 参考資料

### GitHub 関連
- [GitHub スタートガイド](https://docs.github.com/ja/get-started)
- [Git コマンド一覧](https://git-scm.com/book/ja/v2)
- [GitHub Personal Access Token](https://docs.github.com/ja/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)

### プロジェクト関連
- [設計書](docs/Job_Compass_Design.md)
- [MVP実装ガイド](docs/MVP_IMPLEMENTATION_GUIDE.md)
- [チェックリスト](docs/MVP_DAILY_CHECKLIST.md)

---

## 🎯 次のステップ

```
1. ✓ GitHub にアップロード完了
2. README を ブラウザで確認
3. 友人・知人にリンク共有
4. MVP（Googleスプレッドシート版）を2週間で完成
5. Twitter / クラウドワークス コミュニティで告知
```

---

## 💡 Tips

### GitHub Pages でドキュメント公開

```bash
# GitHub Settings → Pages → Source: docs/
# 自動的に https://[username].github.io/crowdworks で公開

# docs/index.md を作成
cat > docs/index.md << 'EOF'
# Job Compass ドキュメント

- [設計書](Job_Compass_Design.md)
- [MVP実装ガイド](MVP_IMPLEMENTATION_GUIDE.md)
- [Google Apps Script](GOOGLE_APPS_SCRIPT_CODES.md)
EOF
```

### リポジトリをテンプレート化

```
Settings → Template repository にチェック
→ 他のユーザーがこのリポジトリをテンプレートとして使用可能
```

### Issue テンプレート設定

`.github/ISSUE_TEMPLATE/` に Markdown ファイルを配置
→ 自動的にテンプレートが提示される

---

## 🆘 サポート

**問題が発生した場合**:

1. エラーメッセージ全体をコピー
2. 上記の「よくあるエラー」で確認
3. GitHub 公式ドキュメントで検索
4. このプロジェクトの Issues で報告（オプション）

---

## 📞 質問・フィードバック

**この ガイドについての質問がある場合**:

- GitHub Issues で報告
- Twitter で @[ユーザー名] に連絡
- Email で contact@jobcompass.dev に連絡

---

**これで、Job Compass は GitHub で公開される準備が整いました！** 🚀

**さらに詳細は `GITHUB_UPLOAD_GUIDE.md` を参照してください。**
