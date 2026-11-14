# Made by Karin — Build Plan

E-commerce site for my pottery business. Real shop **and** a portfolio project for React / Next.js / TypeScript roles.

## Stack

| Layer | Choice |
|---|---|
| Framework | Next.js (App Router) + TypeScript (strict) |
| Styling / UI | Tailwind CSS + shadcn/ui |
| i18n | next-intl (`sl` now, `de` later) |
| Database | PostgreSQL + Prisma (local: Docker Compose) |
| Auth | Better Auth |
| Payments | Stripe Checkout + webhooks |
| Validation / forms | Zod + React Hook Form |
| Images | Cloudinary |
| Email / newsletter | Resend + React Email (Resend Audiences) |
| Testing | Vitest + React Testing Library, Storybook, Playwright |
| CI | GitHub Actions |
| Hosting | Hetzner (Docker) — done last |

## Key decisions

- **Stock:** every product has a `stock` number. One-of-a-kind = stock 1, batch items = stock N.
- **Language:** Slovenian by default, no URL prefix (`localePrefix: "as-needed"`). German (`/de`) added for Austria later.
- **Guest checkout:** orders store the customer email and an *optional* user ID. Guest orders get linked when someone signs up with the same email.
- **Shipping:** Pošta Slovenije delivery + free local pickup (Stripe Checkout shipping options).
- **Stock reservation:** stock is reserved when checkout starts and released if the Stripe session expires, so a unique piece can't be sold twice.
- **NestJS:** deferred until the shop works.

---

## Phase 0 — Project setup
- [x] Create project with `create-next-app` (TS, Tailwind, ESLint, App Router, `src/`)
- [x] TypeScript strict + `noUncheckedIndexedAccess`, `typecheck` script
- [x] Prettier (+ Tailwind plugin, eslint-config-prettier), `format` script
- [x] Git + GitHub repo
- [ ] shadcn/ui (installed, needs commit)
- [ ] next-intl with `sl` locale
- [ ] Install Docker, Postgres via Docker Compose
- [ ] Prisma connected to Postgres
- [ ] Fix `.gitignore` so `.env.example` is committed (`!.env.example`)
- [ ] Vitest + React Testing Library
- [ ] Storybook
- [ ] Playwright
- [ ] GitHub Actions CI (lint, typecheck, test)
- [ ] README with project description and setup steps

## Phase 1 — Product catalogue
- [ ] Prisma models: `Product` (name, slug, description, priceCents, stock, weightGrams, isUnique, status), `Category`, `ProductImage`
- [ ] Seed script with fake pottery
- [ ] Pages: home, shop (category filter), product detail with gallery
- [ ] Cloudinary images with `next/image`
- [ ] Sold unique pieces stay visible as "Sold"
- [ ] Storybook stories: ProductCard, Gallery, PriceTag, …

## Phase 2 — Auth + admin dashboard
- [ ] Better Auth (email/password), `role` on user (`ADMIN` / `CUSTOMER`)
- [ ] Protect `/admin` (proxy **and** every Server Action)
- [ ] Admin product CRUD, Cloudinary image upload, stock editing
- [ ] Shared Zod schemas for forms + server

## Phase 3 — Cart + checkout ⭐
- [ ] DB cart linked to a cookie (works for guests)
- [ ] Stripe Checkout session with shipping options (post / pickup)
- [ ] Stock reservation in a DB transaction; Stripe session expires after 30 min
- [ ] Webhooks: `checkout.session.completed` → order PAID; `checkout.session.expired` → release stock
- [ ] Local webhook testing with Stripe CLI
- [ ] Order confirmation email (customer + me)
- [ ] Playwright e2e: add to cart → pay with test card → success page

## Phase 4 — Order management (admin)
- [ ] Order list with status filter
- [ ] Statuses: `PAID → PACKED → SHIPPED` / `READY_FOR_PICKUP → COMPLETED`, plus `CANCELLED` / `REFUNDED`
- [ ] "Shipped" email with tracking number, "Ready for pickup" email

## Phase 5 — Customer accounts
- [ ] Sign up, log in, reset password
- [ ] "My orders" page, guest orders linked by email
- [ ] Saved address pre-fills checkout

## Phase 6 — Blog + newsletter
- [ ] Blog with MDX files (maybe DB + admin editor later)
- [ ] Newsletter signup with double opt-in (GDPR), Resend Audiences
- [ ] Optional "subscribe" checkbox at checkout (unticked by default)

## Phase 7 — Legal + polish (before launch)
- [ ] Terms of sale, privacy policy, returns (EU 14-day withdrawal), shipping info, legal notice
- [ ] Cookie banner only if analytics need it (Plausible / Umami don't)
- [ ] SEO: metadata, sitemap, Open Graph images, Product structured data
- [ ] Accessibility audit + Lighthouse
- [ ] Error / empty / loading states, 404 page

## Phase 8 — Deploy to Hetzner (with boyfriend)
- [ ] Dockerfile (`output: "standalone"`)
- [ ] Docker Compose + Caddy (auto HTTPS) or Coolify
- [ ] Production Postgres with automatic daily backups
- [ ] Domain, live Stripe keys, live webhook endpoint
- [ ] Real test purchase + refund

## Phase 9 — Austria / EU
- [ ] German translation (`de` locale)
- [ ] Shipping zones + prices for Austria
- [ ] VAT: ⚠️ check with accountant first (Slovenian small-business limit; EU distance-selling €10,000 threshold → OSS)
- [ ] Maybe Stripe Tax

## Later ideas
NestJS API, wishlist, product reviews, custom order requests, workshop bookings.

---

## Job-hunt notes
- Small commits with clear messages (`feat:`, `fix:`, `chore:`, …)
- Write short decision notes in `docs/decisions/` (why I chose X over Y)
- Best interview stories: **stock reservation** and **Stripe webhooks**
