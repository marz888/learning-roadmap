# Full-Stack TypeScript Roadmap for C/Python Developers

**Goal**: Go from C/Python background to productive full-stack TypeScript developer in ~6 weeks.
**Time commitment**: 4 hours/day.
**Primary framework**: Next.js 15 (App Router) with React 19.

---

## Table of Contents

1. [Stack Overview](#stack-overview)
2. [Daily Structure](#daily-structure)
3. [Week 1: JavaScript + React Fundamentals](#week-1-javascript--react-fundamentals)
4. [Week 2: TypeScript + React Patterns](#week-2-typescript--react-patterns)
5. [Week 3: Backend Fundamentals + Next.js](#week-3-backend-fundamentals--nextjs)
6. [Week 4: Full-Stack Skills](#week-4-full-stack-skills)
7. [Week 5: Build Your Own Project](#week-5-build-your-own-project)
8. [Week 6: Professional Polish](#week-6-professional-polish)
9. [Coursera Course Sequence](#coursera-course-sequence)
10. [Reference Resources](#reference-resources)
11. [Expectations and Pace](#expectations-and-pace)

---

## Stack Overview

- **Language**: TypeScript (strict mode)
- **Frontend**: React 19 with hooks and Server Components
- **Framework**: Next.js 15 (App Router)
- **Styling**: Tailwind CSS (+ shadcn/ui components)
- **Database**: PostgreSQL with Drizzle ORM (Prisma is the alternative)
- **Auth**: Auth.js (NextAuth v5) or Clerk
- **Validation**: Zod
- **Testing**: Vitest + Playwright
- **Deployment**: Vercel (frontend/API) + Neon or Supabase (database)

This is a mainstream, employable 2026 stack. Every piece reinforces the others.

---

## Daily Structure

Split each 4-hour day roughly:

- **1.5 hours**: structured learning (course videos, reading docs)
- **2 hours**: hands-on coding (exercises, building projects)
- **0.5 hour**: review, notes, reading other people's code

Push harder on building than watching — your C/Python background means you already know what a `for` loop is.

---

## Week 1: JavaScript + React Fundamentals

### Days 1–3: JavaScript deep dive

**Mornings (2h)**: Coursera's *Programming with JavaScript* (Meta). Watch at 1.5x, skip basics you know.

**Afternoons (2h)**: [javascript.info](https://javascript.info), chapters 2–8. Write code as you read.

Focus zones:
- Day 1: Closures and lexical scope
- Day 2: `this`, prototypes, classes
- Day 3: Promises, async/await, event loop (most important)

**Day 3 exercise**: Build a Node.js script that fetches from 3 public APIs in parallel using `Promise.all`, merges results, writes to JSON. No frameworks. Pure Node with built-in `fetch`.

### Days 4–5: Modern JS idioms + Node basics

Cover: destructuring, spread/rest, optional chaining, nullish coalescing, array methods (`map`/`filter`/`reduce`/`flatMap`), `Map`/`Set`, modules.

Setup: install `nvm`, Node 20+, learn `npm init`, `package.json`, scripts, `.gitignore`.

**Exercise**: Rewrite day-3 script as a proper npm project with CLI args, ESM (`"type": "module"`), and npm scripts.

### Days 6–7: React fundamentals

Start Coursera's *React Basics* (Meta) or use [react.dev tutorial](https://react.dev/learn).

Focus on:
- Function components only (ignore class components)
- JSX
- Props and state (`useState`)
- Effects (`useEffect`) — understand when NOT to use it
- Event handling, lists and keys, conditional rendering

**Day 7 exercise**: Todo app with React + Vite (`npm create vite@latest`). Plain JS, no TS yet. Features: add, delete, toggle complete, filter by status. Local state only.

**Week 1 milestone**: Can read React code and explain component rendering, state updates, and when effects fire.

---

## Week 2: TypeScript + React Patterns

### Days 8–10: TypeScript from zero to working

**Day 8**: [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/intro.html) — "The Basics" through "Everyday Types" and "Narrowing". Set up a TS project from scratch: `npm i -D typescript @types/node`, write `tsconfig.json` with `strict: true`, compile and run.

**Day 9**: Handbook — "Functions", "Object Types", "Type Manipulation" (at least Generics and Keyof). Work through [Matt Pocock's Beginner's TypeScript](https://www.totaltypescript.com/tutorials/beginners-typescript) — free, ~70 exercises.

**Day 10**: Advanced bits — discriminated unions, type narrowing (`typeof`/`in`/custom guards), utility types (`Partial`, `Pick`, `Omit`, `Record`, `ReturnType`), `as const`, `satisfies`.

### Days 11–12: React + TypeScript

Rewrite the todo app in TypeScript. Reference: [React TypeScript Cheatsheet](https://react-typescript-cheatsheet.netlify.app).

Learn:
- Typing props with interfaces
- Event handler types (`React.ChangeEvent<HTMLInputElement>`, etc.)
- Generic components
- `useState` with explicit types
- `useReducer` for complex state (your C background helps here)

### Days 13–14: React hooks deep dive + forms

Cover: `useReducer`, `useContext`, `useMemo`, `useCallback`, `useRef`, custom hooks. Know when NOT to use `useMemo`/`useCallback`.

**Exercise**: Multi-step form with validation (name, email, preferences, confirmation). Use `useReducer` for form state. Type everything strictly. No form library yet.

**Week 2 milestone**: Can build a typed React app from scratch with proper state management.

---

## Week 3: Backend Fundamentals + Next.js

### Days 15–16: HTTP, REST, and raw Node

Before Next.js hides everything, build a minimal HTTP server with Node's `http` module, then the same with Fastify.

Understand:
- Request/response lifecycle
- HTTP methods, status codes, headers
- JSON body parsing
- URL parameters vs query strings vs body
- CORS
- Middleware pattern

**Exercise**: REST API for notes with Fastify + TypeScript. Endpoints: `GET /notes`, `GET /notes/:id`, `POST /notes`, `PATCH /notes/:id`, `DELETE /notes/:id`. In-memory storage. Validate with Zod. Write a test script.

### Days 17–18: SQL and PostgreSQL

Review: schema design, primary/foreign keys, joins, indexes, transactions, `EXPLAIN`.

Install Postgres locally or use [Neon](https://neon.tech) free tier. Learn [Drizzle ORM](https://orm.drizzle.team) — modern TypeScript-first ORM.

**Exercise**: Connect Fastify API to Postgres via Drizzle. Migrate from in-memory. Add `users` table; relate notes to users.

### Days 19–21: Next.js App Router

Start the [Next.js learn course](https://nextjs.org/learn) — ~8 hours of focused work.

Cover:
- App Router file conventions (`page.tsx`, `layout.tsx`, `loading.tsx`, `error.tsx`)
- Server Components vs Client Components (`"use client"`) — core mental model
- Route handlers (API routes)
- Server Actions
- Data fetching in Server Components
- Dynamic routes and route groups

**Mental model**: Server Components run on server only; Client Components are interactive, run in browser. Server Components can be async and fetch data directly. Unlike anything in C/Python — takes a day or two to click.

**Day 21 exercise**: Rebuild notes app as Next.js app. UI in Server Components where possible, Client Components only for interactivity. Use Server Actions for mutations.

**Week 3 milestone**: Understand the request lifecycle browser → Next.js server → database → back. Can explain where each piece of code runs.

---

## Week 4: Full-Stack Skills

### Days 22–23: Styling with Tailwind

Learn [Tailwind CSS](https://tailwindcss.com). Actually read the docs. Focus on flexbox/grid utilities, responsive prefixes, dark mode, `@apply`.

Recommended: [shadcn/ui](https://ui.shadcn.com) — copy-paste components on Radix UI + Tailwind.

### Days 24–25: Authentication

Pick one:
- **Auth.js (NextAuth v5)**: free, flexible, more setup. Better for understanding auth deeply.
- **Clerk**: paid (has free tier), drop-in. Better for shipping fast.

Learn: sessions vs JWTs, OAuth flow, password hashing (bcrypt/argon2), CSRF, protecting routes/endpoints, auth middleware.

**Exercise**: Add auth to notes app. Users sign up, log in, see only their own notes. Protect server actions and API routes.

### Days 26–28: Data fetching patterns and caching

Next.js caching is powerful and confusing. Learn:
- Static vs dynamic rendering
- `cache()`, `unstable_cache`, `revalidatePath`, `revalidateTag`
- Streaming with Suspense
- Optimistic updates with `useOptimistic`
- Form state with `useActionState`
- Loading and error boundaries

Also learn **TanStack Query (React Query)** for client-side data fetching.

**Exercise**: Add to notes app — search (server-side), pagination, tags, optimistic UI for CRUD, loading/error states.

**Week 4 milestone**: Real, styled, authenticated full-stack app with good UX.

---

## Week 5: Build Your Own Project

Stop following tutorials. Pick something ambitious but finishable in ~1 week.

Requirements:
- At least 3 database tables with relationships
- Authentication
- At least one external API integration
- Non-trivial UI (forms, lists, detail views)
- Deployed to production

### Project ideas

- **Personal analytics dashboard**: connects to GitHub, RSS, cloud provider; visualizes activity
- **Self-hosted bookmark manager**: tagging, search, browser extension
- **Code snippet manager**: syntax highlighting, search, sharing
- **Markdown knowledge base**: full-text search and backlinks (mini-Obsidian)
- **Rate-limited API gateway**: proxies other APIs with auth and logging (plays to systems background)

Ship it. Deploy to Vercel + Neon (free tiers). Optionally buy a domain.

### Learn as needed

- Environment variables and secrets (`.env.local`, `process.env`, Zod validation)
- Database migrations in production
- Error monitoring (Sentry free tier)
- Analytics (Vercel Analytics or Plausible)
- SEO basics (metadata API, sitemap)

---

## Week 6: Professional Polish

### Days 36–37: Testing

- **Unit tests**: Vitest — faster, better DX than Jest. Test utilities and business logic, not UI.
- **Component tests**: React Testing Library with Vitest. Cover key components.
- **End-to-end tests**: [Playwright](https://playwright.dev). Cover 2–3 critical user flows.

Aim for confidence, not coverage.

### Days 38–39: Performance and production

Diagnose and fix:
- Bundle size (Next.js bundle analyzer)
- Lighthouse scores, Core Web Vitals
- Database query performance (`EXPLAIN`, indexes, N+1 queries)
- Caching strategies (React cache, Next.js cache, HTTP cache)
- Image optimization (`next/image`)

Run Lighthouse on your project. Fix what it flags.

### Days 40–42: Read real code + CI/CD

- Read source of a medium-sized TS/Next.js project. Suggestions: [cal.com](https://github.com/calcom/cal.com), [dub.co](https://github.com/dubinc/dub), [documenso](https://github.com/documenso/documenso). Notice patterns.
- GitHub Actions: run tests on push, deploy on merge to main.
- Write a README with screenshots and live demo link.

**Week 6 milestone**: Portfolio-ready project. Understand the full lifecycle from code to production.

---

## Coursera Course Sequence

Your subscription is most valuable for weeks 1–2 and early week 3.

1. **Week 1**: *Programming with JavaScript* (Meta) + start *React Basics* (Meta)
2. **Week 2**: Finish *React Basics*, start *Advanced React* (Meta). Skip Jest-heavy testing sections — we use Vitest.
3. **Week 3+**: Coursera has weaker coverage of Next.js, Drizzle, and modern patterns. Switch to official docs, [Matt Pocock](https://www.totaltypescript.com), [Theo's videos](https://www.youtube.com/@t3dotgg), and [Lee Robinson's content](https://leerob.com).

Note: Meta's *Full-Stack Engineer* certificate uses Django for backend, not Node — less useful for this plan.

---

## Reference Resources

Bookmark these:

- [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/intro.html) — authoritative
- [React docs](https://react.dev) — excellent new docs
- [Next.js docs](https://nextjs.org/docs) — dense but complete
- [Drizzle docs](https://orm.drizzle.team/docs/overview) — clean
- [Total TypeScript](https://www.totaltypescript.com) — free and paid TS content
- [javascript.info](https://javascript.info) — best JS reference
- [Patterns.dev](https://patterns.dev) — design patterns in modern JS

---

## Expectations and Pace

### After 6 weeks at 4h/day, you'll be:

- **Confident**: writing TypeScript, building Next.js apps, designing schemas, shipping features
- **Competent**: with production concerns — testing, deployment, auth, caching
- **Not yet expert**: at performance optimization, accessibility, complex state management, large-scale architecture

Expertise comes from 6–12 months of real work. This plan gets you to the point where you can contribute to a real codebase, interview for jobs, or build your own products.

### A note on pace

4 hours/day is a lot of focused learning. Some days you'll hit a wall — TypeScript generics, Server Components, or Postgres performance might each eat a full day. Normal. Treat the plan as a guide, not a contract. If you need 10 weeks instead of 6, you're still moving fast.

---

## Milestone Checklist

- [ ] Day 7: Can write non-trivial JS with Promises and array methods without reference
- [ ] Day 14: Can set up a TypeScript project from scratch and write typed code
- [ ] Day 21: Made framework choice; built hello-world-plus Next.js app
- [ ] Day 28: Full-stack app with auth, DB, styling, good UX
- [ ] Day 35: Deployed personal project live on the internet
- [ ] Day 42: Can read most open-source TS code; have tests and CI/CD

---

*Roadmap generated 2026-04-16. Stack and tool versions current as of this date; check for newer versions when starting.*
