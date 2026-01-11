# Danbi AI - AI 기반 다국어 학습 플랫폼 / AI-Powered Multilingual Learning Platform

> **Language / 언어**: [한국어](#한국어) | [English](#english)

---

## 한국어

# Danbi AI - AI 기반 다국어 학습 플랫폼

AI 기반 다국어 플래시카드 학습 서비스. SM-2 알고리즘과 OpenAI GPT-4o mini를 사용한 효율적인 학습 플랫폼입니다.

## 주요 기능

- 🤖 **AI 생성 기능**: OpenAI GPT-4o mini를 사용한 자동 카드 생성
- 📚 **SM-2 알고리즘**: 과학적으로 증명된 간격 반복 학습법
- 🎴 **인터랙티브한 학습**: 아름다운 UI와 부드러운 애니메이션
- 📊 **통계 대시보드**: 학습 진행 상황과 복습 통계 확인
- 💳 **구독 서비스**: Free/Standard 플랜 지원
- 🌙 **다크 모드**: 라이트/다크 테마 지원
- 📱 **모바일 최적화**: 반응형 디자인
- 🌍 **다국어 지원**: 한국어, 일본어, 영어 UI 지원

## 기술 스택

- **프레임워크**: Next.js 16 (App Router)
- **UI**: React 19, shadcn/ui, Tailwind CSS
- **데이터베이스**: Supabase (PostgreSQL)
- **인증**: Supabase Auth
- **AI**: OpenAI GPT-4o mini
- **애니메이션**: Framer Motion
- **폼**: React Hook Form + Zod
- **테마**: next-themes
- **다국어**: next-intl

## 시작하기

### 필수 요구사항

- Node.js 18+
- pnpm (권장) 또는 npm/yarn
- Supabase 계정
- OpenAI API 키
- Stripe 계정

### 1. 저장소 클론

```bash
git clone <repository-url>
cd danbi-ai
```

### 2. 의존성 설치

```bash
pnpm install
```

### 3. 환경 변수 설정

`.env.local` 파일을 생성하고 다음 환경 변수를 설정하세요:

```env
# Supabase
NEXT_PUBLIC_SUPABASE_URL=your_supabase_project_url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key
SUPABASE_SERVICE_ROLE_KEY=your_supabase_service_role_key

# OpenAI
OPENAI_API_KEY=your_openai_api_key

# Stripe
STRIPE_SECRET_KEY=your_stripe_secret_key
STRIPE_WEBHOOK_SECRET=your_stripe_webhook_secret
STRIPE_PRICE_ID=your_stripe_price_id
```

자세한 내용은 [환경 변수 문서](#환경-변수)를 참조하세요.

### 4. 데이터베이스 설정

Supabase 대시보드에서 다음 마이그레이션 파일을 순서대로 실행하세요:

1. `supabase/migrations/001_create_profiles.sql`
2. `supabase/migrations/002_create_decks.sql`
3. `supabase/migrations/003_create_cards.sql`
4. `supabase/migrations/004_add_stripe_subscriptions.sql`
5. `supabase/migrations/005_add_last_ai_deck_generation.sql`
6. `supabase/migrations/006_add_cards_deck_review_index.sql`
7. `supabase/migrations/007_add_language_support.sql`
8. `supabase/migrations/008_fix_learning_languages_default.sql`
9. `supabase/migrations/009_add_deck_ui_language.sql`

또는 Supabase CLI를 사용:

```bash
supabase db push
```

### 5. 개발 서버 실행

```bash
pnpm dev
```

브라우저에서 [http://localhost:3000](http://localhost:3000)을 열어주세요.

## 환경 변수

### 필수 환경 변수

| 변수명                          | 설명                              | 획득 방법                                               |
| ------------------------------- | --------------------------------- | ------------------------------------------------------- |
| `NEXT_PUBLIC_SUPABASE_URL`      | Supabase 프로젝트의 URL           | Supabase 대시보드 > Settings > API                      |
| `NEXT_PUBLIC_SUPABASE_ANON_KEY` | Supabase 익명 키                  | Supabase 대시보드 > Settings > API                      |
| `SUPABASE_SERVICE_ROLE_KEY`     | Supabase 서비스 역할 키           | Supabase 대시보드 > Settings > API                      |
| `OPENAI_API_KEY`                | OpenAI API 키                     | [OpenAI Platform](https://platform.openai.com/api-keys) |
| `STRIPE_SECRET_KEY`             | Stripe Secret Key (서버 사이드용) | Stripe 대시보드 > Developers > API keys                 |
| `STRIPE_WEBHOOK_SECRET`         | Stripe Webhook Signing Secret     | Stripe 대시보드 > Developers > Webhooks                 |
| `STRIPE_PRICE_ID`               | Stripe Price ID (구독 가격 ID)    | Stripe 대시보드 > Products > Prices                     |

### 환경 변수 설정 예시

`.env.local` 파일:

```env
# Supabase Configuration
NEXT_PUBLIC_SUPABASE_URL=https://xxxxx.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
SUPABASE_SERVICE_ROLE_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...

# OpenAI Configuration
OPENAI_API_KEY=sk-...

# Stripe Configuration
STRIPE_SECRET_KEY=sk_test_xxxxx
STRIPE_WEBHOOK_SECRET=whsec_xxxxx
STRIPE_PRICE_ID=price_xxxxx
```

⚠️ **중요**: `.env.local` 파일은 Git에 커밋하지 마세요. `.gitignore`에 포함되어 있습니다.

## 프로젝트 구조

```
danbi-ai/
├── src/
│   ├── app/                    # Next.js App Router
│   │   ├── (auth)/            # 인증 관련 페이지
│   │   ├── (dashboard)/       # 대시보드 관련 페이지
│   │   └── api/              # API Routes
│   ├── components/            # React 컴포넌트
│   │   ├── ui/               # shadcn/ui 컴포넌트
│   │   ├── auth/             # 인증 컴포넌트
│   │   ├── deck/             # 덱 컴포넌트
│   │   ├── card/             # 카드 컴포넌트
│   │   ├── study/            # 학습 세션 컴포넌트
│   │   └── stats/            # 통계 컴포넌트
│   └── lib/                   # 유틸리티와 라이브러리
│       ├── supabase/         # Supabase 설정과 쿼리
│       ├── sm2/              # SM-2 알고리즘 구현
│       ├── ai/               # OpenAI 통합
│       └── utils/            # 유틸리티 함수
├── supabase/
│   └── migrations/           # 데이터베이스 마이그레이션
└── public/                   # 정적 파일
```

## 빌드와 배포

### 프로덕션 빌드

```bash
pnpm build
```

### 프로덕션 서버 실행

```bash
pnpm start
```

### Vercel에 배포

1. [Vercel](https://vercel.com)에 프로젝트를 가져오기
2. 환경 변수 설정
3. 배포

자세한 내용은 [Next.js deployment documentation](https://nextjs.org/docs/app/building-your-application/deploying)을 참조하세요.

## 라이선스

이 프로젝트는 프라이빗 프로젝트입니다.

## 지원

문제가 발생한 경우, Issue를 생성해주세요.

---

## English

# Danbi AI - AI-Powered Multilingual Learning Platform

An AI-powered multilingual flashcard learning service. An efficient learning platform using the SM-2 algorithm and OpenAI GPT-4o mini.

## Key Features

- 🤖 **AI Generation**: Automatic card generation using OpenAI GPT-4o mini
- 📚 **SM-2 Algorithm**: Scientifically proven spaced repetition learning method
- 🎴 **Interactive Learning**: Beautiful UI with smooth animations
- 📊 **Statistics Dashboard**: Track learning progress and review statistics
- 💳 **Subscription Service**: Free/Standard plan support
- 🌙 **Dark Mode**: Light/Dark theme support
- 📱 **Mobile Optimized**: Responsive design
- 🌍 **Multilingual Support**: Korean, Japanese, and English UI support

## Tech Stack

- **Framework**: Next.js 16 (App Router)
- **UI**: React 19, shadcn/ui, Tailwind CSS
- **Database**: Supabase (PostgreSQL)
- **Authentication**: Supabase Auth
- **AI**: OpenAI GPT-4o mini
- **Animation**: Framer Motion
- **Forms**: React Hook Form + Zod
- **Theme**: next-themes
- **Internationalization**: next-intl

## Getting Started

### Prerequisites

- Node.js 18+
- pnpm (recommended) or npm/yarn
- Supabase account
- OpenAI API key
- Stripe account

### 1. Clone Repository

```bash
git clone <repository-url>
cd danbi-ai
```

### 2. Install Dependencies

```bash
pnpm install
```

### 3. Environment Variables

Create a `.env.local` file and set the following environment variables:

```env
# Supabase
NEXT_PUBLIC_SUPABASE_URL=your_supabase_project_url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key
SUPABASE_SERVICE_ROLE_KEY=your_supabase_service_role_key

# OpenAI
OPENAI_API_KEY=your_openai_api_key

# Stripe
STRIPE_SECRET_KEY=your_stripe_secret_key
STRIPE_WEBHOOK_SECRET=your_stripe_webhook_secret
STRIPE_PRICE_ID=your_stripe_price_id
```

For more details, refer to the [Environment Variables](#environment-variables) section.

### 4. Database Setup

Run the following migration files in order from the Supabase dashboard:

1. `supabase/migrations/001_create_profiles.sql`
2. `supabase/migrations/002_create_decks.sql`
3. `supabase/migrations/003_create_cards.sql`
4. `supabase/migrations/004_add_stripe_subscriptions.sql`
5. `supabase/migrations/005_add_last_ai_deck_generation.sql`
6. `supabase/migrations/006_add_cards_deck_review_index.sql`
7. `supabase/migrations/007_add_language_support.sql`
8. `supabase/migrations/008_fix_learning_languages_default.sql`
9. `supabase/migrations/009_add_deck_ui_language.sql`

Or use Supabase CLI:

```bash
supabase db push
```

### 5. Run Development Server

```bash
pnpm dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

## Environment Variables

### Required Environment Variables

| Variable Name                   | Description                          | How to Obtain                                           |
| ------------------------------- | ------------------------------------ | ------------------------------------------------------- |
| `NEXT_PUBLIC_SUPABASE_URL`      | Supabase project URL                 | Supabase Dashboard > Settings > API                     |
| `NEXT_PUBLIC_SUPABASE_ANON_KEY` | Supabase anonymous key               | Supabase Dashboard > Settings > API                     |
| `SUPABASE_SERVICE_ROLE_KEY`     | Supabase service role key            | Supabase Dashboard > Settings > API                     |
| `OPENAI_API_KEY`                | OpenAI API key                       | [OpenAI Platform](https://platform.openai.com/api-keys) |
| `STRIPE_SECRET_KEY`             | Stripe Secret Key (server-side)      | Stripe Dashboard > Developers > API keys                |
| `STRIPE_WEBHOOK_SECRET`         | Stripe Webhook Signing Secret        | Stripe Dashboard > Developers > Webhooks                |
| `STRIPE_PRICE_ID`               | Stripe Price ID (subscription price) | Stripe Dashboard > Products > Prices                    |

### Environment Variables Example

`.env.local` file:

```env
# Supabase Configuration
NEXT_PUBLIC_SUPABASE_URL=https://xxxxx.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
SUPABASE_SERVICE_ROLE_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...

# OpenAI Configuration
OPENAI_API_KEY=sk-...

# Stripe Configuration
STRIPE_SECRET_KEY=sk_test_xxxxx
STRIPE_WEBHOOK_SECRET=whsec_xxxxx
STRIPE_PRICE_ID=price_xxxxx
```

⚠️ **Important**: Do not commit the `.env.local` file to Git. It is included in `.gitignore`.

## Project Structure

```
danbi-ai/
├── src/
│   ├── app/                    # Next.js App Router
│   │   ├── (auth)/            # Authentication pages
│   │   ├── (dashboard)/       # Dashboard pages
│   │   └── api/              # API Routes
│   ├── components/            # React components
│   │   ├── ui/               # shadcn/ui components
│   │   ├── auth/             # Authentication components
│   │   ├── deck/             # Deck components
│   │   ├── card/             # Card components
│   │   ├── study/            # Study session components
│   │   └── stats/            # Statistics components
│   └── lib/                   # Utilities and libraries
│       ├── supabase/         # Supabase setup and queries
│       ├── sm2/              # SM-2 algorithm implementation
│       ├── ai/               # OpenAI integration
│       └── utils/            # Utility functions
├── supabase/
│   └── migrations/           # Database migrations
└── public/                   # Static files
```

## Build and Deployment

### Production Build

```bash
pnpm build
```

### Run Production Server

```bash
pnpm start
```

### Deploy to Vercel

1. Import project to [Vercel](https://vercel.com)
2. Set environment variables
3. Deploy

For more details, refer to the [Next.js deployment documentation](https://nextjs.org/docs/app/building-your-application/deploying).

## License

This project is a private project.

## Support

If you encounter any issues, please create an Issue.
