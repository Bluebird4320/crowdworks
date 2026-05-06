# 🌐 Phase 1：Webアプリ版 開発ガイド

**期間：Week 3-12 | ステータス：次フェーズ**

Phase 0 の MVP テストが終了した後、Webアプリ化を進めます。

---

## 📋 目次

1. [技術スタック](#技術スタック)
2. [プロジェクト構成](#プロジェクト構成)
3. [セットアップ手順](#セットアップ手順)
4. [実装タイムライン](#実装タイムライン)
5. [API 仕様](#api-仕様)
6. [DB スキーマ](#db-スキーマ)
7. [デプロイ方法](#デプロイ方法)

---

## 🛠 技術スタック

| レイヤー | 技術 | 理由 |
|---------|------|------|
| **フロント** | Next.js 14 + React 18 | SSR/SSG、高速ビルド |
| **スタイル** | Tailwind CSS | 高速開発、レスポンシブ |
| **バック** | Node.js + Express | 軽量、非同期処理対応 |
| **言語** | TypeScript | 型安全性、開発効率 |
| **DB** | PostgreSQL | スケーラビリティ、信頼性 |
| **ORM** | Prisma | 型安全、マイグレーション簡単 |
| **認証** | NextAuth.js | Google OAuth 対応 |
| **AI** | Claude API | 高精度テキスト生成 |
| **ホスティング** | Vercel (フロント) | 自動デプロイ、エッジ機能 |
| **ホスティング** | Render (バック) | PostgreSQL ホスティング |

---

## 📁 プロジェクト構成

```
crowdworks-compass/
├── 📄 README.md
├── 📋 docs/
│   ├── 設計書.md
│   ├── phase0-google-sheets.md
│   ├── phase1-webapp.md（このファイル）
│   ├── database-schema.md
│   └── api-specification.md
│
├── 🌐 phase1-webapp/
│   │
│   ├── 🎨 next.js-frontend/
│   │   ├── app/
│   │   │   ├── page.tsx                    # ホーム
│   │   │   ├── dashboard/
│   │   │   │   ├── page.tsx                # ダッシュボード
│   │   │   │   ├── layout.tsx
│   │   │   │   └── (components)/
│   │   │   ├── categories/
│   │   │   │   ├── page.tsx                # ジャンル分析
│   │   │   │   └── [id]/
│   │   │   ├── jobs/
│   │   │   │   ├── page.tsx                # 案件一覧
│   │   │   │   └── [id]/
│   │   │   │       └── page.tsx            # 案件詳細
│   │   │   ├── apply/
│   │   │   │   └── page.tsx                # 応募文生成
│   │   │   ├── settings/
│   │   │   │   └── page.tsx                # 設定
│   │   │   ├── api/
│   │   │   │   └── auth/
│   │   │   │       └── [...nextauth]/
│   │   │   │           └── route.ts        # NextAuth 設定
│   │   │   └── layout.tsx
│   │   │
│   │   ├── 🧩 components/
│   │   │   ├── Navbar.tsx
│   │   │   ├── Sidebar.tsx
│   │   │   ├── Cards/
│   │   │   │   ├── KPICard.tsx
│   │   │   │   ├── JobCard.tsx
│   │   │   │   └── ScoreCard.tsx
│   │   │   ├── Charts/
│   │   │   │   ├── TrendChart.tsx
│   │   │   │   ├── DistributionChart.tsx
│   │   │   │   └── CategoryChart.tsx
│   │   │   └── Forms/
│   │   │       ├── JobFilterForm.tsx
│   │   │       └── ApplyForm.tsx
│   │   │
│   │   ├── 🔧 lib/
│   │   │   ├── api.ts                      # API クライアント
│   │   │   ├── auth.ts                     # 認証ロジック
│   │   │   ├── utils.ts                    # ユーティリティ
│   │   │   └── constants.ts                # 定数
│   │   │
│   │   ├── 🎨 styles/
│   │   │   ├── globals.css
│   │   │   └── variables.css
│   │   │
│   │   ├── .env.example
│   │   ├── .env.local（環境変数）
│   │   ├── package.json
│   │   ├── tsconfig.json
│   │   ├── tailwind.config.js
│   │   └── next.config.js
│   │
│   │
│   ├── 🖥️ express-backend/
│   │   ├── src/
│   │   │   ├── index.ts                    # メインエントリ
│   │   │   ├── config/
│   │   │   │   ├── database.ts             # DB 接続
│   │   │   │   └── env.ts                  # 環境変数
│   │   │   ├── routes/
│   │   │   │   ├── jobs.ts                 # 案件 API
│   │   │   │   ├── categories.ts           # ジャンル API
│   │   │   │   ├── scoring.ts              # スコアリング API
│   │   │   │   ├── risk.ts                 # リスク判定 API
│   │   │   │   ├── apply.ts                # 応募文生成 API
│   │   │   │   ├── users.ts                # ユーザー API
│   │   │   │   └── auth.ts                 # 認証 API
│   │   │   ├── controllers/
│   │   │   │   ├── jobController.ts
│   │   │   │   ├── categoryController.ts
│   │   │   │   ├── scoringController.ts
│   │   │   │   └── userController.ts
│   │   │   ├── services/
│   │   │   │   ├── jobService.ts
│   │   │   │   ├── scoringService.ts
│   │   │   │   ├── riskService.ts
│   │   │   │   ├── applyService.ts
│   │   │   │   └── claudeService.ts        # Claude API 連携
│   │   │   ├── middleware/
│   │   │   │   ├── auth.ts                 # 認証ミドルウェア
│   │   │   │   ├── errorHandler.ts         # エラーハンドリング
│   │   │   │   └── logger.ts               # ロギング
│   │   │   ├── utils/
│   │   │   │   ├── validators.ts
│   │   │   │   └── helpers.ts
│   │   │   └── types/
│   │   │       ├── user.ts
│   │   │       ├── job.ts
│   │   │       ├── score.ts
│   │   │       └── api.ts
│   │   │
│   │   ├── prisma/
│   │   │   └── schema.prisma                # Prisma スキーマ
│   │   │
│   │   ├── migrations/
│   │   │   └── 001_init.sql
│   │   │
│   │   ├── .env.example
│   │   ├── .env（環境変数）
│   │   ├── package.json
│   │   ├── tsconfig.json
│   │   └── Dockerfile
│   │
│   │
│   └── 🗄️ database/
│       ├── schema.sql                      # DB スキーマ
│       ├── migrations/
│       │   ├── 001_users_table.sql
│       │   ├── 002_jobs_table.sql
│       │   ├── 003_scoring_table.sql
│       │   └── 004_applications_table.sql
│       └── seeds/
│           └── dev-data.sql                # テストデータ
│
├── 🧪 tests/
│   ├── unit/
│   │   ├── scoring.test.ts
│   │   ├── risk.test.ts
│   │   └── apply.test.ts
│   └── integration/
│       ├── auth.test.ts
│       ├── jobs.test.ts
│       └── api.test.ts
│
└── .github/
    └── workflows/
        ├── test.yml                        # 自動テスト
        └── deploy.yml                      # 自動デプロイ
```

---

## 🔧 セットアップ手順

### ステップ1：リポジトリのクローン

```bash
# GitHub からクローン
git clone https://github.com/Bluebird4320/crowdworks-compass.git
cd crowdworks-compass

# Node.js バージョン確認（18 以上推奨）
node --version
npm --version
```

### ステップ2：PostgreSQL 設定（Render）

```bash
# Render にサインアップ
→ https://render.com

# 新規 PostgreSQL データベース作成
1. Render ダッシュボード
2. 「New +」→「PostgreSQL」
3. 名前：crowdworks-compass
4. 無料プラン選択
5. 接続文字列をコピー

# 環境変数に保存（後で使用）
DATABASE_URL="postgresql://..."
```

### ステップ3：Webアプリ（Next.js）セットアップ

```bash
cd phase1-webapp/next.js-frontend

# 依存関係をインストール
npm install

# 環境変数を設定
cp .env.example .env.local

# .env.local を編集
NEXT_PUBLIC_API_URL=http://localhost:3001
NEXTAUTH_SECRET=<secret-key-here>
NEXTAUTH_URL=http://localhost:3000
GOOGLE_CLIENT_ID=<from-google-console>
GOOGLE_CLIENT_SECRET=<from-google-console>

# 開発サーバー起動
npm run dev

# ブラウザで http://localhost:3000 にアクセス
```

### ステップ4：バックエンド（Express）セットアップ

```bash
cd phase1-webapp/express-backend

# 依存関係をインストール
npm install

# 環境変数を設定
cp .env.example .env

# .env を編集
DATABASE_URL=postgresql://...
CLAUDE_API_KEY=<your-claude-api-key>
NODE_ENV=development
PORT=3001

# Prisma マイグレーション
npx prisma migrate dev --name init

# 開発サーバー起動
npm run dev

# サーバーが http://localhost:3001 で起動
```

### ステップ5：Claude API キー取得

```
1. Anthropic Console にアクセス
   → https://console.anthropic.com

2. API キーを取得
3. .env に設定
   CLAUDE_API_KEY=sk-ant-...
```

### ステップ6：Google OAuth 設定

```
1. Google Cloud Console
   → https://console.cloud.google.com

2. 新規プロジェクト作成

3. OAuth 2.0 認証情報作成
   - アプリケーションタイプ：Web アプリケーション
   - リダイレクト URI：http://localhost:3000/api/auth/callback/google

4. クライアント ID とクライアントシークレットを取得

5. .env.local に設定
   GOOGLE_CLIENT_ID=...
   GOOGLE_CLIENT_SECRET=...
```

---

## ⏱️ 実装タイムライン

### Week 3-4：基盤構築

**Week 3**
```
Day 1-2：
- GitHub リポジトリ作成
- 基本フォルダ構造作成
- npm パッケージセットアップ
- ESLint/Prettier 設定

Day 3-4：
- PostgreSQL セットアップ
- Prisma スキーマ定義
- DB マイグレーション実行

Day 5：
- 開発環境の動作確認
- テストコマンド実行
```

**Week 4**
```
Day 1-2：
- Next.js ページ構造構築
- Express サーバー立ち上げ
- CORS 設定

Day 3-4：
- NextAuth.js セットアップ
- Google OAuth テスト
- ログイン/ログアウト UI

Day 5：
- 全体動作確認
- バグ修正
```

### Week 5-7：API & フロント実装

**Week 5：認証 & ユーザー機能**
```
- GET /api/users/profile
- PATCH /api/users/profile
- GET /api/users/preferences
- ユーザープロフィール画面
- 設定画面
```

**Week 6：案件機能**
```
- GET /api/jobs（一覧取得）
- GET /api/jobs/:id（詳細取得）
- POST /api/jobs/filter（フィルタ）
- 案件一覧画面
- 案件詳細画面
- フィルタ UI
```

**Week 7：ジャンル分析**
```
- GET /api/categories（カテゴリ一覧）
- GET /api/categories/:id/analysis
- ジャンル分析画面
- グラフ表示
```

### Week 8-10：AI 機能

**Week 8：スコアリング**
```
- POST /api/jobs/:id/score
- スコアリングロジック実装
- スコア表示 UI
- リスク判定ロジック
```

**Week 9：応募文生成**
```
- POST /api/messages/generate
- Claude API 統合
- 応募文生成画面
- テンプレート UI
```

**Week 10：テスト & 最適化**
```
- ユニットテスト
- 統合テスト
- パフォーマンステスト
- バグ修正
```

### Week 11-12：デプロイ

**Week 11：本番環境準備**
```
- Vercel デプロイ設定
- Render バックエンド デプロイ
- SSL/TLS 設定
- 本番環境テスト
```

**Week 12：ローンチ**
```
- マーケティング準備
- ユーザー招待
- 初期ユーザーテスト
- バグ修正・改善
```

---

## 🔌 API 仕様

### 認証エンドポイント

```typescript
// GET /api/auth/session
// ログイン中のユーザー情報を取得
Response: {
  user: {
    id: string;
    email: string;
    name: string;
    image?: string;
  }
}

// POST /api/auth/signin
// ログイン（NextAuth が自動で処理）

// POST /api/auth/signout
// ログアウト
```

### 案件エンドポイント

```typescript
// GET /api/jobs?page=1&limit=20
Response: {
  jobs: Job[];
  total: number;
  page: number;
}

// GET /api/jobs/:id
Response: Job

// GET /api/jobs?category=ライティング&risk=low&beginner=true
// フィルタ対応

// POST /api/jobs/:id/bookmark
// ブックマーク追加

// DELETE /api/jobs/:id/bookmark
// ブックマーク削除
```

### スコアリングエンドポイント

```typescript
// POST /api/jobs/:id/score
Request: { /* 案件情報 */ }
Response: {
  score: number;           // 0-100
  rank: "S" | "A" | "B" | "C" | "D";
  breakdown: {
    reward: number;
    clientTrust: number;
    beginnerFriendly: number;
    risk: number;
    continuing: number;
    skillMatch: number;
    clarity: number;
  }
}
```

### 地雷案件チェック

```typescript
// POST /api/risk-check
Request: {
  title: string;
  description: string;
}
Response: {
  riskLevel: "low" | "medium" | "high";
  riskScore: number;      // 0-100
  keywords: string[];     // 検出された危険キーワード
  message: string;        // 警告メッセージ
}
```

### 応募文生成

```typescript
// POST /api/messages/generate
Request: {
  jobId: string;
  templateType: "beginner" | "sincere" | "ai" | "continuing" | "short" | "junior";
  userSkills: string[];
}
Response: {
  message: string;
  editableMessage: string;
}
```

詳細は [api-specification.md](./api-specification.md) を参照。

---

## 🗄️ DB スキーマ

```prisma
model User {
  id        String   @id @default(cuid())
  email     String   @unique
  name      String?
  image     String?
  skills    String[] @default([])
  experience_level  String  @default("beginner")
  monthly_goal      Int     @default(50000)
  available_hours   Int     @default(20)
  
  jobs      SavedJob[]
  applications Application[]
  messages  GeneratedMessage[]
  
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
}

model Job {
  id                String   @id @default(cuid())
  cloudworksJobId   String?
  title             String
  categoryId        String
  clientId          String
  description       String?
  rewardMin         Int
  rewardMax         Int?
  rewardType        String   // "固定" | "時給" | "応募型"
  estimatedHours    Int?
  isBeginnerOk      Boolean  @default(false)
  isContinuing      Boolean  @default(false)
  riskLevel         String   // "低" | "中" | "高"
  riskScore         Int      // 0-100
  matchingScore     Int?     // 0-100
  
  category   Category @relation(fields: [categoryId], references: [id])
  client     Client   @relation(fields: [clientId], references: [id])
  savedJobs  SavedJob[]
  
  postedDate DateTime
  createdAt  DateTime @default(now())
  updatedAt  DateTime @updatedAt
}

model Category {
  id             String   @id @default(cuid())
  name           String   @unique
  description    String?
  avgReward      Int?
  medianReward   Int?
  beginnerOkRate Decimal?
  continuingRate Decimal?
  riskRate       Decimal?
  difficulty     Int?     // 1-5
  
  jobs Job[]
  
  createdAt DateTime @default(now())
}

model Client {
  id           String   @id @default(cuid())
  cloudworksId String?
  name         String
  rating       Decimal? // 0-5
  positiveRate Decimal?
  totalContracts Int?
  trustScore   Int?     // 0-100
  
  jobs Job[]
  
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
}

model SavedJob {
  id        String   @id @default(cuid())
  userId    String
  jobId     String
  
  user User @relation(fields: [userId], references: [id], onDelete: Cascade)
  job  Job  @relation(fields: [jobId], references: [id], onDelete: Cascade)
  
  savedAt DateTime @default(now())
  
  @@unique([userId, jobId])
}

model Application {
  id        String   @id @default(cuid())
  userId    String
  jobId     String
  status    String   // "draft" | "sent" | "accepted" | "rejected"
  message   String?
  result    String?  // "採用" | "不採用"
  
  user User @relation(fields: [userId], references: [id], onDelete: Cascade)
  
  appliedAt   DateTime @default(now())
  evaluatedAt DateTime?
  
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
}

model GeneratedMessage {
  id           String   @id @default(cuid())
  userId       String
  jobId        String
  templateType String
  content      String
  
  user User @relation(fields: [userId], references: [id], onDelete: Cascade)
  
  createdAt DateTime @default(now())
}
```

詳細は [database-schema.md](./database-schema.md) を参照。

---

## 🚀 デプロイ方法

### フロント（Vercel）

```bash
# 1. Vercel に接続
npm install -g vercel
vercel login

# 2. デプロイ
cd phase1-webapp/next.js-frontend
vercel

# 3. 環境変数を設定
# Vercel ダッシュボード > Settings > Environment Variables
# 必要な変数：
# - NEXT_PUBLIC_API_URL
# - NEXTAUTH_SECRET
# - NEXTAUTH_URL
# - GOOGLE_CLIENT_ID
# - GOOGLE_CLIENT_SECRET

# 4. デプロイ完了
# → https://your-project.vercel.app
```

### バック（Render）

```bash
# 1. Render にサインアップ
→ https://render.com

# 2. 新規 Web Service 作成
- GitHub リポジトリ連携
- リポジトリ：crowdworks-compass
- ルートディレクトリ：phase1-webapp/express-backend

# 3. 環境変数を設定
# Render ダッシュボル > Environment
# 必要な変数：
# - DATABASE_URL（PostgreSQL 接続文字列）
# - CLAUDE_API_KEY
# - NODE_ENV=production
# - PORT=3001（自動設定）

# 4. デプロイ完了
# → https://your-api.onrender.com
```

### CI/CD パイプライン

```yaml
# .github/workflows/deploy.yml
name: Deploy

on:
  push:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          node-version: '18'
      - run: npm install
      - run: npm run test

  deploy:
    needs: test
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - run: npm run build
      - run: vercel --prod --token ${{ secrets.VERCEL_TOKEN }}
```

---

## 📊 成功指標

```
【Webアプリ完成のチェック】
✅ ユーザー数：50人以上
✅ 本番環境で安定稼働（99% uptime）
✅ ページロード時間：< 3秒
✅ API レスポンス時間：< 500ms
✅ 基本機能全実装
✅ セキュリティ監査クリア
```

---

## 🎯 次のステップ

### Phase 2 以降

```
Week 13-16：AI 機能強化
- プロフィール改善提案
- 応募文改善提案
- 個人化されたおすすめ案件

Week 17-24：マーケティング・マネタイズ
- 有料版リリース
- ユーザー数 500 人達成
- 月収 50 万円達成
```

詳細は設計書の [開発ロードマップ](./設計書.md#18-開発ロードマップ) を参照。

---

## 📚 参考資料

- [Next.js ドキュメント](https://nextjs.org/docs)
- [Prisma ドキュメント](https://www.prisma.io/docs/)
- [Claude API ドキュメント](https://docs.anthropic.com/)
- [Express ドキュメント](https://expressjs.com/)

---

**準備完了！🚀 Webアプリ開発を始めましょう！**
