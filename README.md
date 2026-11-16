# Made by Karin

> 🚧 **Work in progress.** The project is set up and the shop is being built step by step.

An online shop for my pottery business. Every piece is handmade, many of them one of a kind.
It's a real shop that I'll use, and a full-stack portfolio project.

## Planned stack

| Layer | Choice |
|---|---|
| Framework | Next.js (App Router), TypeScript (strict) |
| Styling / UI | Tailwind CSS, shadcn/ui |
| Languages | next-intl (Slovenian first, German later) |
| Database | PostgreSQL with Prisma |
| Auth | Better Auth |
| Payments | Stripe Checkout and webhooks |
| Forms | Zod and React Hook Form |
| Images | Cloudinary |
| Email | Resend and React Email |
| Testing | Vitest, React Testing Library, Storybook, Playwright |
| CI | GitHub Actions |
| Hosting | Hetzner (Docker) |

## Key decisions

- **Stock for unique pieces.** Every product has a stock number: a one-of-a-kind piece has stock 1.
- **Stock reservation.** Stock is reserved when checkout starts and released if the Stripe
  session expires, so a unique piece can't be sold twice.
- **Guest checkout.** Orders store the customer's email and an optional user ID. Guest orders
  are linked to the account when someone signs up with the same email.
- **Shipping.** Pošta Slovenije delivery, or free local pickup, through Stripe Checkout.

## Run it locally

```bash
npm install
npm run dev        # http://localhost:3000
npm run typecheck  # TypeScript check
npm run lint
```

## Progress

The full build plan, with what's done and what's next, is in [`PLAN.md`](PLAN.md).
