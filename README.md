# Acme Dashboard — Next.js App Router

A full-stack financial dashboard built while following the [Next.js App Router course](https://nextjs.org/learn). It manages invoices and customers for a fictional company called Acme, backed by a PostgreSQL database.

## Tech Stack

| Layer | Technology |
|---|---|
| Framework | Next.js (App Router) |
| Language | TypeScript |
| Styling | Tailwind CSS |
| Database | PostgreSQL (`postgres` driver) |
| Auth | NextAuth.js v5 (beta) |
| Validation | Zod |
| Icons | Heroicons |

## Features

- **Dashboard overview** — summary cards (total invoices, customers, paid/pending amounts) and a revenue chart
- **Invoices** — paginated table with full-text search, create/edit forms, and paid/pending status badges
- **Customers** — searchable table showing per-customer invoice totals
- **Authentication** — login/logout via NextAuth with bcrypt-hashed passwords
- **Database seeding** — one-request seed endpoint at `/seed`

## Project Structure

```
nextjs-dashboard/
├── app/
│   ├── dashboard/
│   │   ├── overview/     # Revenue chart + summary cards
│   │   ├── invoices/     # Invoice list, create, edit
│   │   └── customers/    # Customer table
│   ├── lib/
│   │   ├── data.ts       # All database queries
│   │   ├── definitions.ts# Shared TypeScript types
│   │   ├── utils.ts      # Formatting helpers
│   │   └── placeholder-data.ts
│   ├── ui/               # Reusable components (forms, tables, nav, skeletons)
│   ├── seed/route.ts     # GET /seed — seeds the database
│   └── query/route.ts    # GET /query — ad-hoc SQL endpoint
├── public/               # Static assets
└── .env.example          # Required environment variables
```

## Getting Started

### 1. Prerequisites

- Node.js 18+
- pnpm
- A PostgreSQL database (e.g. Vercel Postgres)

### 2. Environment Variables

Copy `.env.example` to `.env.local` and fill in the values:

```bash
cp .env.example .env.local
```

```env
POSTGRES_URL=
POSTGRES_USER=
POSTGRES_HOST=
POSTGRES_PASSWORD=
POSTGRES_DATABASE=

AUTH_SECRET=        # openssl rand -base64 32
AUTH_URL=http://localhost:3000/api/auth
```

### 3. Install & Run

```bash
cd nextjs-dashboard
pnpm install
pnpm dev
```

The app runs at [http://localhost:3000](http://localhost:3000).

### 4. Seed the Database

With the dev server running, visit:

```
http://localhost:3000/seed
```

This creates the `users`, `customers`, `invoices`, and `revenue` tables and populates them with placeholder data.

## Database Schema

| Table | Key Columns |
|---|---|
| `users` | `id`, `name`, `email`, `password` (bcrypt) |
| `customers` | `id`, `name`, `email`, `image_url` |
| `invoices` | `id`, `customer_id`, `amount`, `status`, `date` |
| `revenue` | `month`, `revenue` |

## Scripts

```bash
pnpm dev      # Start dev server (Turbopack)
pnpm build    # Production build
pnpm start    # Start production server
```
