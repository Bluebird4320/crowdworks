# 🧭 Job Compass - クラウドワークス案件分析ツール

**クラウドワークス初心者が、安全＆効率的に案件を選べるセカンドスクリーン**

## 📌 プロジェクト概要

「Job Compass」は、クラウドワークスの案件を分析・評価し、初心者が地雷案件を避けながら最適な案件を見つけるためのツールです。

### 🎯 解決する問題
- ❌ 案件が多すぎて選べない
- ❌ 低単価案件や地雷案件の見分けがつかない
- ❌ 相場感がわからない
- ❌ 応募文が書けない
- ❌ 月いくら稼げるか不透明

### ✨ 提供する価値
✅ **相場の見える化** - ジャンル別の平均報酬・中央値を表示  
✅ **地雷案件検出** - AI が危険キーワードを自動検出  
✅ **スコアリング機能** - 100点満点で案件を評価  
✅ **応募文自動生成** - テンプレート＆AI で時間短縮  
✅ **月5万円シミュレーター** - 現実的な収入予測

---

## 🚀 開発ロードマップ

### Phase 0: MVP（Googleスプレッドシート版）
**期間：Week 1-2** | **ステータス：📋 準備中**

- [ ] Input シート
- [ ] Dashboard シート
- [ ] ジャンル分析シート
- [ ] リスク判定機能
- [ ] 応募文テンプレート

👉 [詳細はこちら](./docs/phase0-google-sheets.md)

### Phase 1: Webアプリ化
**期間：Week 3-8** | **ステータス：🔄 次フェーズ**

- [ ] PostgreSQL + API 構築
- [ ] Next.js フロント開発
- [ ] Google ログイン認証
- [ ] Claude API 統合

👉 [詳細はこちら](./docs/phase1-webapp.md)

### Phase 2: AI 機能強化
**期間：Week 9-12** | **ステータス：🔄 次フェーズ**

- [ ] 応募文改善提案
- [ ] プロフィール改善提案
- [ ] 個人化されたおすすめ案件

### Phase 3: マネタイズ
**期間：Month 4+** | **ステータス：🔄 次フェーズ**

- [ ] 有料版（Pro/Premium）
- [ ] オンライン講座
- [ ] テンプレート販売

---

## 📁 ディレクトリ構成

```
crowdworks-compass/
├── 📄 README.md                          # このファイル
├── 📋 docs/
│   ├── 設計書.md                         # 完全な設計書
│   ├── phase0-google-sheets.md           # MVP ガイド
│   ├── phase1-webapp.md                  # Webアプリ ガイド
│   ├── database-schema.md                # DB スキーマ
│   └── api-specification.md              # API 仕様書
├── 📊 phase0-google-sheets/
│   ├── template.md                       # スプシ構成図
│   ├── formulas.md                       # 計算式一覧
│   └── setup-guide.md                    # セットアップガイド
├── 🌐 phase1-webapp/
│   ├── next.js-template/                 # Next.js プロジェクト
│   ├── api-server/                       # Express API サーバー
│   └── database/                         # DB マイグレーション
├── 🎨 design/
│   ├── color-palette.md                  # カラー設計
│   ├── ui-components.md                  # UI コンポーネント
│   └── wireframes/                       # ワイヤーフレーム
├── 🧪 tests/
│   ├── unit/                             # ユニットテスト
│   └── integration/                      # 統合テスト
└── .github/
    ├── workflows/                        # CI/CD パイプライン
    └── ISSUE_TEMPLATE/                   # Issue テンプレート
```

---

## 🛠 技術スタック

### Phase 0（MVP）
- **Google スプレッドシート** - ノーコード開発
- **Google Apps Script** - 計算・自動化

### Phase 1（Webアプリ）
| レイヤー | 技術 |
|---------|------|
| **フロント** | Next.js 14 + React 18 + Tailwind CSS |
| **バック** | Node.js + Express |
| **DB** | PostgreSQL + Prisma ORM |
| **認証** | NextAuth.js (Google OAuth) |
| **AI** | Claude API (Anthropic) |
| **ホスティング** | Vercel (フロント) + Render (バック) |

---

## 📖 ドキュメント

| ドキュメント | 説明 |
|----------|------|
| [設計書](./docs/設計書.md) | 完全な仕様書・設計書 |
| [MVP ガイド](./docs/phase0-google-sheets.md) | Googleスプシ版のセットアップ |
| [Webアプリ ガイド](./docs/phase1-webapp.md) | Webアプリの開発手順 |
| [DB スキーマ](./docs/database-schema.md) | データベース設計 |
| [API 仕様](./docs/api-specification.md) | REST API 仕様書 |

---

## 🎮 クイックスタート

### 🔧 Phase 0：Google スプレッドシート版を試す

```bash
# 1. テンプレートを開く
# Google Drive にアクセス → 新規スプレッドシート作成

# 2. setup-guide.md に従ってセットアップ
cat phase0-google-sheets/setup-guide.md

# 3. ダミーデータを入力してテスト
# → ジャンル分析、スコアリング、リスク判定が動作するか確認
```

### 💻 Phase 1：Webアプリを開発

```bash
# 1. リポジトリをクローン
git clone https://github.com/Bluebird4320/crowdworks-compass.git
cd crowdworks-compass

# 2. 環境構築
cd phase1-webapp/next.js-template
npm install

# 3. 環境変数を設定
cp .env.example .env.local
# .env.local を編集（DB URL、Claude API キーなど）

# 4. DB マイグレーション
npm run db:migrate

# 5. 開発サーバーを起動
npm run dev

# 6. ブラウザで http://localhost:3000 にアクセス
```

---

## 🎯 成功指標

### Phase 0（MVP）
- ✅ ユーザー数：10名以上
- ✅ 使用頻度：週1回以上
- ✅ 満足度：70点以上
- ✅ フィードバック：3件以上

### Phase 1（Webアプリ）
- ✅ ユーザー数：50人以上
- ✅ 本番環境で安定稼働
- ✅ 基本機能全実装

### Phase 2（マネタイズ）
- ✅ ユーザー数：500人以上
- ✅ 有料ユーザー：50人以上
- ✅ 月収：50万円以上

---

## 👥 ターゲットユーザー

1. **副業初心者の会社員** - 月5万円の副業収入を目指す
2. **主婦・主夫** - 月3万円の小遣い稼ぎ
3. **フリーランス志望の学生** - スキル習得＆稼ぎたい
4. **AI活用に興味がある人** - 効率化で稼ぎたい
5. **失業中の人** - 月10万円を稼ぎたい

---

## 📝 貢献ガイドライン

このプロジェクトへの貢献を歓迎します！

### 貢献方法
1. このリポジトリを Fork
2. フィーチャーブランチを作成 (`git checkout -b feature/amazing-feature`)
3. コミット (`git commit -m 'Add amazing feature'`)
4. ブランチにプッシュ (`git push origin feature/amazing-feature`)
5. Pull Request を作成

### コード規約
- JavaScript/TypeScript：ESLint + Prettier
- コミットメッセージ：`[Type] Description` (e.g., `[Feat] Add scoring feature`)
- ブランチ名：`feature/xxx` or `fix/xxx`

---

## ⚖️ ライセンス

このプロジェクトは **MIT ライセンス** の下で公開されています。  
詳細は [LICENSE](./LICENSE) ファイルを参照してください。

---

## 💬 サポート・質問

### Issue を報告する
- 🐛 バグ報告：[Bug Report テンプレート](.github/ISSUE_TEMPLATE/bug_report.md)
- 💡 機能要望：[Feature Request テンプレート](.github/ISSUE_TEMPLATE/feature_request.md)
- ❓ 質問：[Q&A テンプレート](.github/ISSUE_TEMPLATE/question.md)

### コミュニティ
- 📧 メール：[contact@example.com]
- 🐦 Twitter/X：[@jobcompass_app]
- 💬 Discord：[コミュニティサーバー]

---

## 🗺 ロードマップ（概要）

```
Month 1     → Google スプシ版 MVP
Month 2-3   → Webアプリ化（本番環境）
Month 4-6   → AI 機能強化＆マーケティング
Month 7-12  → 有料版＆スケーリング
Year 2+     → 企業向けサービス展開
```

詳細は [ROADMAP.md](./docs/ROADMAP.md) を参照してください。

---

## 📊 プロジェクト統計

| メトリクス | 値 |
|-----------|-----|
| 設計書ページ数 | 50+ ページ |
| 実装予定機能数 | 20+ 機能 |
| ターゲットユーザー | 初心者～中級者 |
| 開発期間 | 3ヶ月（MVP～本番） |
| 予想ユーザー数（Year 1） | 500～1,000人 |

---

## 🎓 参考資料

- [クラウドワークス 利用規約](https://crowdworks.jp/)
- [Claude API ドキュメント](https://docs.anthropic.com/)
- [Next.js 公式ドキュメント](https://nextjs.org/docs)
- [PostgreSQL チュートリアル](https://www.postgresql.org/docs/)

---

**最後に更新：** 2026年5月  
**バージョン：** 1.0  
**ステータス：** 📋 開発準備完了

---

**🚀 今すぐ開発を始めましょう！**  
[Phase 0 スタートガイド](./docs/phase0-google-sheets.md) →
