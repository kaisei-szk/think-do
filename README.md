# Think Do! - 学習コーチングサービス LP

## Project Overview
- **Name**: Think Do!
- **Goal**: 筑波大学医学類生による受験コーチングサービスのランディングページ
- **Features**: 
  - 「自考力」をコンセプトにしたLP
  - 問い合わせフォーム（D1データベース保存）
  - レスポンシブデザイン

## URLs
- **Preview**: https://3000-ic7mu15knnugql7s9pnmn-b32ec7bb.sandbox.novita.ai
- **API Health**: https://3000-ic7mu15knnugql7s9pnmn-b32ec7bb.sandbox.novita.ai/api/health

## Tech Stack
- **Backend**: Hono (Cloudflare Workers)
- **Frontend**: HTML + TailwindCSS (CDN) + Vanilla JavaScript
- **Database**: Cloudflare D1 (SQLite)
- **Icons**: Font Awesome 6.4.0

## Data Architecture

### inquiries テーブル
| Column | Type | Description |
|--------|------|-------------|
| id | INTEGER | PRIMARY KEY AUTOINCREMENT |
| name | TEXT | お名前 (必須) |
| email | TEXT | メールアドレス (必須) |
| grade | TEXT | 学年 (必須) |
| message | TEXT | お問い合わせ内容 |
| created_at | DATETIME | 作成日時 |

## API Endpoints

### POST /api/inquiries
問い合わせを送信
```json
{
  "name": "筑波太郎",
  "email": "test@example.com",
  "grade": "高校3年生",
  "message": "数学が苦手です"
}
```

### GET /api/inquiries
全ての問い合わせを取得（管理用）

### GET /api/health
ヘルスチェック

## Development

### ローカル開発
```bash
# 依存関係インストール
npm install

# ビルド
npm run build

# D1マイグレーション適用
npm run db:migrate:local

# 開発サーバー起動
npm run dev:sandbox
# または PM2で起動
pm2 start ecosystem.config.cjs
```

### デプロイ（Cloudflare Pages）
```bash
# 1. D1データベース作成（初回のみ）
npx wrangler d1 create thinkdo-production
# wrangler.jsonc の database_id を更新

# 2. 本番マイグレーション
npm run db:migrate:prod

# 3. デプロイ
npm run deploy
```

## Project Structure
```
webapp/
├── src/
│   └── index.tsx          # Honoメインアプリ（APIルート + HTMLレンダリング）
├── migrations/
│   └── 0001_initial_schema.sql  # D1マイグレーション
├── public/
│   └── static/            # 静的ファイル
├── dist/                  # ビルド出力
├── ecosystem.config.cjs   # PM2設定
├── wrangler.jsonc         # Cloudflare設定
├── package.json
├── tsconfig.json
├── vite.config.ts
└── README.md
```

## Sections
1. **Hero** - メインビジュアル＋キャッチコピー
2. **Concept** - 「自考力」の哲学
3. **Management** - 戦略＋モチベーション管理
4. **Features** - 筑波大医学類生の指導メソッド
5. **Story** - 代表メッセージ
6. **Pricing** - 料金プラン（3段階）
7. **Contact** - 問い合わせフォーム

## Pricing Plans
| Plan | Price | Features |
|------|-------|----------|
| ライト戦略コース | ¥14,800/月 | 月1回面談、月次計画、教材選定 |
| 自考力養成コース | ¥29,800/月 | 週1回面談、LINE相談無制限、思考コーチング |
| 徹底マネジメントコース | ¥49,800/月 | 日次管理、60分面談、添削、優先対応 |

## Deployment Status
- **Platform**: Cloudflare Pages
- **Status**: ✅ Development Ready
- **Last Updated**: 2024-12-20
