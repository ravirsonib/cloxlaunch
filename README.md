# CLOX pre-launch

Public marketing site for CLOX, an Australia-first full-load freight marketplace. The site collects early-access interest from senders, carriers, and investors before launch.

The app lives in [`web/`](web/).

## Stack

- [Next.js](https://nextjs.org/) 15 (App Router) and React 19
- TypeScript, Tailwind CSS
- Zustand, TanStack Query, Axios
- i18next (English, Hindi, Punjabi)
- Zod and React Hook Form
- Serwist (production service worker / PWA)

## Setup

Requires Node.js 22.

```bash
cd web
cp .env.example .env.local
npm install
npm run dev
```

Open [http://localhost:3000](http://localhost:3000). Next.js uses port 3000 unless you pass another port (`npx next dev -p 5173`). Set `SITE_URL` in `.env.local` to the URL you actually serve.

## Scripts

Run these from `web/`:

| Script | What it does |
| --- | --- |
| `npm run dev` | Development server |
| `npm run build` | Production build, including the service worker |
| `npm run start` | Serve the production build |
| `npm run lint` | TypeScript check (`tsc --noEmit`) |

## Environment

Copy `web/.env.example` to `web/.env.local`.

| Variable | Purpose |
| --- | --- |
| `SITE_URL` | Canonical site URL (SEO, sitemap, metadata) |
| `NEXT_PUBLIC_APP_NAME` | Display name (the UI brand stays CLOX) |
| `NEXT_PUBLIC_DEFAULT_LOCALE` | Default locale (`en`) |
| `API_BASE_URL` | Nest API base, server-only (default `http://localhost:3000/v1`) |
| `NEXT_PUBLIC_API_BASE_URL` | Optional browser fallback; prefer same-origin `/api/leads/*` |
| `AI_PROVIDER` | Site guide provider: `mock`, `openai`, or `anthropic` |
| `AI_MODEL` | Model name when a real provider is selected |
| `OPENAI_API_KEY` / `ANTHROPIC_API_KEY` | Provider keys (server-only) |

## Routes

Localized pages use `en`, `hi`, or `pa`. `/` redirects to `/en`.

| Path | Page |
| --- | --- |
| `/{locale}` | Home |
| `/{locale}/registry` | Pre-launch registry |
| `/{locale}/partner/eoi` | Carrier expression of interest |
| `/{locale}/investors` | Investor interest |
| `/{locale}/privacy` | Privacy |
| `/{locale}/terms` | Terms |
| `/offline` | Offline fallback |

Lead forms post to `/api/leads/registry`, `/api/leads/eoi`, and `/api/leads/investor`. The site guide uses `/api/chat`. Discovery files: `/llms.txt`, `/llms-full.txt`, `/sitemap.xml`, `/robots.txt`.
