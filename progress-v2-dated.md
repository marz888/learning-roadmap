# Progress Tracker — Realistic Edition (v2, dated)

Daily checklist matching `combined-roadmap-v2.md`. Tick boxes as you go.

**Timeline**: 8 weeks • Mon–Fri • 5h/day (2.5h fullstack + 2.5h agents)
**Start date**: Friday 17 April 2026 • **Target end date**: Thursday 11 June 2026 (40 working days)

---

## Progress summary

- Days completed: **0 / 40**
- Milestones hit: **0 / 8**
- Rest days taken: **0 / 16** (aim for 2/week × 8 weeks)

---

## Week 1 — Foundations

### Day 1 — Fri 17 Apr
- [ ] **FS**: JS closures, lexical scope (Coursera + javascript.info)
- [ ] **AG**: API key + credit, install `anthropic`, first CLI that prints response + tokens

### Day 2 — Mon 20 Apr
- [ ] **FS**: JS `this`, prototypes, classes
- [ ] **AG**: Read prompt eng overview; build multi-turn chat CLI with history

### Day 3 — Tue 21 Apr
- [ ] **FS**: Promises, async/await, event loop — build parallel fetch script
- [ ] **AG**: Read CoT + XML tags + system prompts; write 5 progressive prompts for one task

### Day 4 — Wed 22 Apr
- [ ] **FS**: Destructuring, spread, optional chaining, array methods, Map/Set, modules
- [ ] **AG**: Read tool use docs; write the agent loop on paper

### Day 5 — Thu 23 Apr
- [ ] **FS**: Node + npm project setup; rewrite day-3 script properly
- [ ] **AG**: Implement `read_file` / `write_file` / `list_dir` tools (single-turn)

- [ ] 🏁 **Week 1 milestone**: comfortable with JS + Promises; first tool call working

### Weekend 1 — Sat 24 / Sun 25 Apr
- [ ] Actually rested

---

## Week 2 — React + the Agent Loop

### Day 6 — Fri 24 Apr
- [ ] **FS**: React basics — components, JSX, props, `useState`
- [ ] **AG**: Full agent loop — iterate until `end_turn`

### Day 7 — Mon 27 Apr
- [ ] **FS**: `useEffect`, events, lists, conditional rendering
- [ ] **AG**: Test agent on "add docstrings"; fix what breaks (this is v0)

### Day 8 — Tue 28 Apr
- [ ] **FS**: **Build todo app in React + Vite, plain JS**
- [ ] **AG**: Add `run_bash` (safe); first pass of "Building effective agents"

### Day 9 — Wed 29 Apr
- [ ] **FS**: Finish todo app; split into components
- [ ] **AG**: Add `grep`/`find`; sandbox agent to `./workspace`

### Day 10 — Thu 30 Apr
- [ ] **FS**: Review React rendering; add one more todo feature
- [ ] **AG**: Structured logging with `rich`; test on messy Python file

- [ ] 🏁 **Week 2 milestone**: todo app works; hand-rolled agent runs on real tasks

### Weekend 2 — Sat 01 / Sun 02 May
- [ ] Rested

---

## Week 3 — TypeScript + a Proper Agent

### Day 11 — Fri 01 May
- [ ] **FS**: TS — basics, everyday types, narrowing; TS project with `strict: true`
- [ ] **AG**: Prompt caching docs; add caching to system prompt + tools

### Day 12 — Mon 04 May
- [ ] **FS**: TS — functions, object types; Matt Pocock beginner tutorial
- [ ] **AG**: Measure cost before/after caching on 20-turn run

### Day 13 — Tue 05 May
- [ ] **FS**: TS — generics, keyof, utility types
- [ ] **AG**: Re-read "Building effective agents"; start refactoring agent

### Day 14 — Wed 06 May
- [ ] **FS**: TS — discriminated unions, type guards, `as const`, `satisfies`
- [ ] **AG**: Finish "proper" agent — clean prompt, 5–7 tools, sandboxed, logged

### Day 15 — Thu 07 May
- [ ] **FS**: **Rewrite todo app in TypeScript**
- [ ] **AG**: Test on 3 different coding tasks; note failures (data for evals)

- [ ] 🏁 **Week 3 milestone**: typed todo app; "proper" agent you're proud of

### Weekend 3 — Sat 08 / Sun 09 May
- [ ] Rested

---

## Week 4 — Next.js + Agent SDK

### Day 16 — Fri 08 May
- [ ] **FS**: Next.js learn course — App Router, file conventions
- [ ] **AG**: Agent SDK overview + quickstart; install + run bug-fix quickstart

### Day 17 — Mon 11 May
- [ ] **FS**: **Server vs Client Components** — the main new mental model
- [ ] **AG**: Compare hand-rolled vs SDK; note what you got for free

### Day 18 — Tue 12 May
- [ ] **FS**: Route handlers, Server Actions, data fetching, dynamic routes
- [ ] **AG**: Permissions guide; build read-only code reviewer (Read/Glob/Grep only)

### Day 19 — Wed 13 May
- [ ] **FS**: SQL + Postgres review; Neon free tier; Drizzle setup
- [ ] **AG**: MCP intro; install `mcp` SDK; start a simple MCP server

### Day 20 — Thu 14 May
- [ ] **FS**: **Build notes CRUD in Next.js** with Drizzle + Neon
- [ ] **AG**: Finish MCP server — `search_my_notes` + `summarize_commit`; wire into agent

- [ ] 🏁 **Week 4 milestone**: notes app in Next.js + Postgres; MCP agent working

### Weekend 4 — Sat 15 / Sun 16 May
- [ ] Rested

---

## Week 5 — Production Essentials

### Day 21 — Fri 15 May
- [ ] **FS**: Tailwind docs; install shadcn/ui
- [ ] **AG**: Eval guidance doc; design YAML test-case format

### Day 22 — Mon 18 May
- [ ] **FS**: **Restyle notes app** with Tailwind + shadcn
- [ ] **AG**: Build eval harness; 10 test cases running

### Day 23 — Tue 19 May
- [ ] **FS**: Auth.js — sessions, OAuth, password hashing; add signup/login
- [ ] **AG**: Tracing with JSONL + pretty-printer; instrument agent

### Day 24 — Wed 20 May
- [ ] **FS**: Finish auth — users see only own notes; protect routes
- [ ] **AG**: Grow evals to 25 cases; fix top 2 failure modes

### Day 25 — Thu 21 May
- [ ] **FS**: Next.js caching basics; `useOptimistic` for CRUD
- [ ] **AG**: Implement **prompt chaining** pattern on a real task

- [ ] 🏁 **Week 5 milestone**: auth'd styled notes app; 25-case eval harness

### Weekend 5 — Sat 22 / Sun 23 May
- [ ] Rested (halfway point — honest check-in below)

---

## Week 6 — Start Your Project

Project name: _______________________

### Day 26 — Fri 22 May
- [ ] **FS**: Scaffold Next.js + Drizzle + Neon; define schema; migrations
- [ ] **AG**: Plan agent feature — tools, success criteria, 5 eval cases

### Day 27 — Mon 25 May
- [ ] **FS**: Auth flow, base layout, shadcn components
- [ ] **AG**: Implement **orchestrator-workers** pattern

### Day 28 — Tue 26 May
- [ ] **FS**: Core CRUD — forms, server actions, route handlers
- [ ] **AG**: First agent endpoint — POST `/api/agent/run` with SSE streaming

### Day 29 — Wed 27 May
- [ ] **FS**: External API integration; error handling; loading states
- [ ] **AG**: Wire agent endpoint into client component; stream tokens into UI

### Day 30 — Thu 28 May
- [ ] **FS**: Env vars, Zod-validated `process.env`, Sentry
- [ ] **AG**: Authenticate agent endpoint; add `max_tokens` + early-abort caps

- [ ] 🏁 **Week 6 milestone**: project deployed (rough); first agent endpoint working

### Weekend 6 — Sat 29 / Sun 30 May
- [ ] Rested

---

## Week 7 — Build

### Day 31 — Fri 29 May
- [ ] **FS**: Feature 2
- [ ] **AG**: Upstash rate limiting; log user + prompt + tool calls + cost per run

### Day 32 — Mon 01 Jun
- [ ] **FS**: Feature 3; think about edge cases
- [ ] **AG**: 15 more eval cases for the integrated feature; run them

### Day 33 — Tue 02 Jun
- [ ] **FS**: Polish one rough area — loading/empty/error states
- [ ] **AG**: Refine system prompt from eval failures; measure improvement

### Day 34 — Wed 03 Jun
- [ ] **FS**: Lighthouse pass; fix top 3 flags; `next/image`
- [ ] **AG**: Trace inspection — 3 failed runs; fix or document

### Day 35 — Thu 04 Jun
- [ ] **FS**: DB perf — `EXPLAIN`, add indexes
- [ ] **AG**: Buffer day — catch up on slippage, or read aider source

- [ ] 🏁 **Week 7 milestone**: 3+ features + solid agent feature; both tested

### Weekend 7 — Sat 05 / Sun 06 Jun
- [ ] Rested

---

## Week 8 — Ship It

### Day 36 — Fri 05 Jun
- [ ] **FS**: Vitest — 10–15 unit tests on business logic (no UI tests)
- [ ] **AG**: Make eval report legible (someone else could read pass/fail + cost)

### Day 37 — Mon 08 Jun
- [ ] **FS**: Playwright — 2 end-to-end tests on critical flows
- [ ] **AG**: "Recent runs" page for logged-in user (good for demos)

### Day 38 — Tue 09 Jun
- [ ] **FS**: GitHub Actions CI — tests run on push
- [ ] **AG**: Design doc for agent feature in the README (2–3 paragraphs)

### Day 39 — Wed 10 Jun
- [ ] **FS**: Polished README — screenshots, live demo, architecture. Custom domain optional
- [ ] **AG**: Eval results in README; 2-minute Loom demo video

### Day 40 — Thu 11 Jun
- [ ] **FS**: **Ship announcement** — post somewhere or tell someone
- [ ] **AG**: Write up ONE hard-won lesson as blog/README section

- [ ] 🏁 **Week 8 milestone**: **deployed, tested, documented project with AI feature**

### Weekend 8 — Sat 12 / Sun 13 Jun
- [ ] Rested (celebrate — you shipped)

---

## Tracking data (update weekly)

### Week 1 (ending Thu 23 Apr)
- Hours actually worked: _____
- One thing learned: _____
- Anything to adjust? _____

### Week 2 (ending Thu 30 Apr)
- Hours actually worked: _____
- One thing learned: _____
- Anything to adjust? _____

### Week 3 (ending Thu 07 May)
- Hours actually worked: _____
- One thing learned: _____
- Anything to adjust? _____

### Week 4 (ending Thu 14 May)
- Hours actually worked: _____
- One thing learned: _____
- Anything to adjust? _____

### Week 5 (ending Thu 21 May — halfway, big check-in)
- Hours actually worked across weeks 1–5: _____
- Still sustainable? _____
- Any skipped content worth revisiting? _____
- Project idea locked in? _____

### Week 6 (ending Thu 28 May)
- Hours actually worked: _____
- Project progress vs plan: _____

### Week 7 (ending Thu 04 Jun)
- Hours actually worked: _____
- What's the riskiest thing still unshipped? _____

### Week 8 (ending Thu 11 Jun)
- Hours actually worked: _____
- What I'm most proud of: _____
- What I'd do differently: _____

---

## Rest day log

Tick every weekend day you genuinely rested:

- [ ] Sat 24 Apr  [ ] Sun 25 Apr (W1)
- [ ] Sat 01 May  [ ] Sun 02 May (W2)
- [ ] Sat 08 May  [ ] Sun 09 May (W3)
- [ ] Sat 15 May  [ ] Sun 16 May (W4)
- [ ] Sat 22 May  [ ] Sun 23 May (W5)
- [ ] Sat 29 May  [ ] Sun 30 May (W6)
- [ ] Sat 05 Jun  [ ] Sun 06 Jun (W7)
- [ ] Sat 12 Jun  [ ] Sun 13 Jun (W8)

If these boxes aren't getting ticked, the plan isn't working as designed — the rest is load-bearing.

---

## Emergency shortcuts (use sparingly)

If you're dangerously behind, cut in this order:

1. Cut week 7's refinement/polish days; ship rougher
2. Cut 1 of the 3 planned project features
3. Cut the blog post on day 40 (do it later)
4. Cut Playwright tests, keep Vitest only
5. Extend timeline by 1–2 weeks instead of cutting content

Never cut:
- Week 1 (foundations compound)
- Week 4 (Next.js mental model is the core of the fullstack track)
- The agent eval harness (without it, you have no idea if your agent works)
- Deployment (week 8) — an undeployed project is no project

---

*Tracker v2 (dated) generated 2026-04-16. Start: Fri 17 Apr 2026. End: Thu 11 Jun 2026.*
