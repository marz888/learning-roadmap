# Roadmap Progress Tracker

**Timeline**: 8 weeks + prep day · Mon–Fri · 5h/day (2.5h FS + 2.5h AG)  
**Start**: Fri 17 Apr 2026 · **Target end**: Thu 11 Jun 2026 · **41 working days**

Tags: `FS` = fullstack · `AG` = agents

---

## Progress summary

| Metric | Value |
|--------|-------|
| Days completed | 0 / 41 |
| Milestones hit | 0 / 8 |
| Tasks ticked | 0 / 108 |

---

## Prep Day — Fri 17 Apr

- [ ] `PREP` Set up dev environment: nvm (Node 20+), Python 3.12, uv, git
- [ ] `PREP` Read "Building effective agents" (Anthropic) — the most important doc on the roadmap
- [ ] `PREP` Get Anthropic API key + $10 credit; run hello-world curl or Python snippet
- [ ] `PREP` Skim javascript.info table of contents — note what's unfamiliar vs familiar from C/Python
- [ ] `PREP` Create GitHub repo `roadmap-work`; commit an empty README — you'll commit here daily

---

## Week 1 — Foundations
**Mon 20 – Fri 24 Apr**

### Day 1 — Mon 20 Apr
- [ ] `FS` JS closures & lexical scope (javascript.info ch.6) — think of closures like C function pointers capturing a stack frame
- [ ] `AG` Install anthropic Python SDK; build CLI that prints response + token usage

### Day 2 — Tue 21 Apr
- [ ] `FS` JS `this`, prototypes, classes — mentally map to Python's `self` and C++ vtables
- [ ] `AG` Read prompt engineering overview; build multi-turn chat CLI with message history

### Day 3 — Wed 22 Apr
- [ ] `FS` Promises, async/await, event loop — closest C analogue: non-blocking I/O with callbacks
- [ ] `AG` Read CoT + XML tags + system prompts; write 5 progressive prompts for one task

### Day 4 — Thu 23 Apr
- [ ] `FS` Destructuring, spread, array methods, Map/Set, ES modules
- [ ] `AG` Read tool use docs; sketch the agent loop on paper

### Day 5 — Fri 24 Apr
- [ ] `FS` Node + npm project setup; rewrite Wed fetch script as proper npm project
- [ ] `AG` Implement `read_file` / `write_file` / `list_dir` tools (single-turn, no loop yet)

🏁 **Milestone**: First API call working; JS Promises comfortable

### Weekend 1 — Sat 25 / Sun 26 Apr
- [ ] Actually rested

---

## Week 2 — React + the Agent Loop
**Mon 27 Apr – Fri 1 May**

### Day 6 — Mon 27 Apr
- [ ] `FS` React: components, JSX, props, useState — think of components as C structs with render functions
- [ ] `AG` Implement the full agent loop — iterate until `end_turn`

### Day 7 — Tue 28 Apr
- [ ] `FS` useEffect, events, lists, conditional rendering
- [ ] `AG` Test agent on "add docstrings to utils.py"; fix what breaks — this is v0

### Day 8 — Wed 29 Apr
- [ ] `FS` Build todo app in React + Vite (plain JS) — add, delete, toggle, filter
- [ ] `AG` Add `run_bash` (whitelisted, timeout via subprocess); read "Building effective agents" pass 1

### Day 9 — Thu 30 Apr
- [ ] `FS` Finish todo app; split into multiple components
- [ ] `AG` Add grep/find tool; sandbox agent to `./workspace`

### Day 10 — Fri 1 May
- [ ] `FS` Review React rendering; add one more todo feature
- [ ] `AG` Structured logging with `rich`; test agent on a messy Python file

🏁 **Milestone**: Todo app works; hand-rolled agent loop runs on real tasks

### Weekend 2 — Sat 2 / Sun 3 May
- [ ] Rested

---

## Week 3 — TypeScript + a Proper Agent
**Mon 4 – Fri 8 May**

### Day 11 — Mon 4 May
- [ ] `FS` TS basics, everyday types, narrowing; set up project with `strict: true` — types feel like C's type system but richer
- [ ] `AG` Read prompt caching docs; add caching to system prompt + tool definitions

### Day 12 — Tue 5 May
- [ ] `FS` TS functions, object types; Matt Pocock beginner tutorial
- [ ] `AG` Measure cost before/after caching on a 20-turn run; write down the savings

### Day 13 — Wed 6 May
- [ ] `FS` TS generics, keyof, Partial/Pick/Omit/Record utility types
- [ ] `AG` Re-read "Building effective agents"; start refactoring agent

### Day 14 — Thu 7 May
- [ ] `FS` Discriminated unions, type guards, `as const`, `satisfies`
- [ ] `AG` Finish proper agent — clean prompt, 5–7 tools, sandboxed, logged

### Day 15 — Fri 8 May
- [ ] `FS` Rewrite todo app in TypeScript; type props, events, state
- [ ] `AG` Test agent on 3 coding tasks; note failures (these become eval cases)

🏁 **Milestone**: Typed todo app; proper coding agent with 5–7 tools

### Weekend 3 — Sat 9 / Sun 10 May
- [ ] Rested

---

## Week 4 — Next.js + Agent SDK
**Mon 11 – Fri 15 May**

### Day 16 — Mon 11 May
- [ ] `FS` Next.js learn course — App Router, file conventions (page.tsx, layout.tsx)
- [ ] `AG` Agent SDK overview + quickstart; install `claude-agent-sdk`; run bug-fix quickstart

### Day 17 — Tue 12 May
- [ ] `FS` Server vs Client Components (`"use client"`) — the main new mental model; take your time
- [ ] `AG` Compare hand-rolled vs SDK; note what the SDK gives you for free

### Day 18 — Wed 13 May
- [ ] `FS` Route handlers, Server Actions, data fetching, dynamic routes
- [ ] `AG` Read permissions guide; build read-only code reviewer (Read/Glob/Grep only)

### Day 19 — Thu 14 May
- [ ] `FS` SQL + Postgres review; Neon free tier; Drizzle setup
- [ ] `AG` MCP intro; install mcp SDK; start a simple MCP server

### Day 20 — Fri 15 May
- [ ] `FS` Build notes CRUD in Next.js — Server Components reads, Server Actions writes, Drizzle + Neon
- [ ] `AG` Finish MCP server with `search_my_notes` + `summarize_commit`; wire into agent

🏁 **Milestone**: Notes app in Next.js + Postgres; Agent SDK + MCP both working

### Weekend 4 — Sat 16 / Sun 17 May
- [ ] Rested

---

## Week 5 — Production Essentials
**Mon 18 – Fri 22 May**

### Day 21 — Mon 18 May
- [ ] `FS` Tailwind docs; install shadcn/ui
- [ ] `AG` Read Anthropic eval guidance; design YAML test-case format

### Day 22 — Tue 19 May
- [ ] `FS` Restyle notes app with Tailwind + shadcn — responsive, dark mode
- [ ] `AG` Build eval harness; 10 test cases running with pass/fail/cost report

### Day 23 — Wed 20 May
- [ ] `FS` Auth.js — sessions, OAuth, password hashing; add signup/login to notes app
- [ ] `AG` Tracing with JSONL + pretty-printer; instrument agent so any run is replayable

### Day 24 — Thu 21 May
- [ ] `FS` Finish auth — users see only own notes; protect server actions + API routes
- [ ] `AG` Grow evals to 25 cases; fix top 2 failure modes

### Day 25 — Fri 22 May
- [ ] `FS` Next.js caching basics; `useOptimistic` for note CRUD
- [ ] `AG` Read "Workflows" section of Building effective agents in full before coding
- [ ] `AG` Pattern 1 — Prompt chaining: extract → generate docstrings → verify (compare to single-shot)
- [ ] `AG` Pattern 2 — Parallelisation: fan out docstring generation for 10 fns with asyncio.gather; implement 3-way majority vote
- [ ] `AG` Pattern 3 — Routing: classify input (security/performance/style/correctness) then dispatch to specialist prompt
- [ ] `AG` Pattern 4 — Orchestrator-workers: small version — orchestrator plans "refactor this module", workers execute
- [ ] `AG` Pattern 5 — Evaluator-optimizer: generate test suite → score it → regenerate if below threshold (cap 3 iterations)
- [ ] `AG` Write a one-paragraph personal decision guide: which pattern, when

🏁 **Milestone**: Auth'd, styled notes app; eval harness with 25 cases + traces; all 5 workflow patterns built

### Weekend 5 — Sat 23 / Sun 24 May
- [ ] Rested (halfway point — honest check-in)

---

## Week 6 — Start Your Project
**Mon 25 – Fri 29 May**

Project name: ___________________________

### Day 26 — Mon 25 May
- [ ] `FS` Scaffold Next.js + Drizzle + Neon; define schema; initial migrations
- [ ] `AG` Plan agent feature — tools, success criteria, 5 eval cases

### Day 27 — Tue 26 May
- [ ] `FS` Auth flow, base layout, shadcn components
- [ ] `AG` Port orchestrator-workers from Day 25 into project context (real tools, real data)
- [ ] `AG` Decide: does your agent need a routing step? Add one if users can ask qualitatively different things

### Day 28 — Wed 27 May
- [ ] `FS` Core CRUD — forms, server actions, route handlers
- [ ] `AG` First agent endpoint — POST `/api/agent/run` with SSE streaming

### Day 29 — Thu 28 May
- [ ] `FS` External API integration; error handling; loading states
- [ ] `AG` Wire agent endpoint into client component; stream tokens into UI

### Day 30 — Fri 29 May
- [ ] `FS` Env vars, Zod-validated `process.env`, Sentry free tier
- [ ] `AG` Authenticate agent endpoint with Auth.js session; add `max_tokens` + early-abort caps

🏁 **Milestone**: Project deployed (rough); first agent endpoint end-to-end

### Weekend 6 — Sat 30 / Sun 31 May
- [ ] Rested

---

## Week 7 — Build
**Mon 1 – Fri 5 Jun**

### Day 31 — Mon 1 Jun
- [ ] `FS` Feature 2
- [ ] `AG` Upstash rate limiting; log user + prompt + tool calls + cost per run

### Day 32 — Tue 2 Jun
- [ ] `FS` Feature 3; think about edge cases
- [ ] `AG` 15 more eval cases for integrated feature; run them

### Day 33 — Wed 3 Jun
- [ ] `FS` Polish loading/empty/error states
- [ ] `AG` Refine system prompt from eval failures; re-run and measure improvement

### Day 34 — Thu 4 Jun
- [ ] `FS` Lighthouse pass; fix top 3 flags; `next/image` for images
- [ ] `AG` Trace inspection — 3 failed runs; fix or document

### Day 35 — Fri 5 Jun
- [ ] `FS` DB perf — `EXPLAIN` on 2–3 queries; add indexes
- [ ] `AG` Buffer: catch up on slippage first; then apply parallelisation or evaluator-optimizer to your project, or read aider source

🏁 **Milestone**: 3+ features + solid agent feature; both tested

### Weekend 7 — Sat 6 / Sun 7 Jun
- [ ] Rested

---

## Week 8 — Ship It
**Mon 8 – Fri 12 Jun**

### Day 36 — Mon 8 Jun
- [ ] `FS` Vitest — 10–15 unit tests on business logic (not UI)
- [ ] `AG` Make eval report legible — pass/fail counts + cost readable by anyone

### Day 37 — Tue 9 Jun
- [ ] `FS` Playwright — 2 end-to-end tests on critical flows
- [ ] `AG` Add "recent runs" page for logged-in user — great for demos

### Day 38 — Wed 10 Jun
- [ ] `FS` GitHub Actions CI — tests run on push
- [ ] `AG` Write 2–3 paragraph agent design doc for the README

### Day 39 — Thu 11 Jun
- [ ] `FS` Polished README — screenshots, live demo link, architecture overview
- [ ] `AG` Eval results in README; record 2-minute Loom demo video

### Day 40 — Fri 12 Jun
- [ ] `FS` Ship announcement — post somewhere or tell someone
- [ ] `AG` Write up ONE hard-won lesson as blog post or README section

🏁 **Milestone**: Deployed, tested, documented project with AI feature. Portfolio ready.

### Weekend 8 — Sat 13 / Sun 14 Jun
- [ ] Rested (celebrate — you shipped)

---

## Weekly check-ins

### Week 1 (ending Fri 24 Apr)
- Hours actually worked: ___
- One thing learned: ___
- Anything to adjust? ___

### Week 2 (ending Fri 1 May)
- Hours actually worked: ___
- One thing learned: ___
- Anything to adjust? ___

### Week 3 (ending Fri 8 May)
- Hours actually worked: ___
- One thing learned: ___
- Anything to adjust? ___

### Week 4 (ending Fri 15 May)
- Hours actually worked: ___
- One thing learned: ___
- Anything to adjust? ___

### Week 5 — halfway check-in (ending Fri 22 May)
- Hours worked across weeks 1–5: ___
- Still sustainable? ___
- Any skipped content worth revisiting? ___
- Project idea locked in? ___

### Week 6 (ending Fri 29 May)
- Hours actually worked: ___
- Project progress vs plan: ___

### Week 7 (ending Fri 5 Jun)
- Hours actually worked: ___
- What's the riskiest thing still unshipped? ___

### Week 8 (ending Fri 12 Jun)
- Hours actually worked: ___
- What I'm most proud of: ___
- What I'd do differently: ___

---

## Rest day log

- [ ] Sat 25 Apr  [ ] Sun 26 Apr  (W1)
- [ ] Sat 2 May   [ ] Sun 3 May   (W2)
- [ ] Sat 9 May   [ ] Sun 10 May  (W3)
- [ ] Sat 16 May  [ ] Sun 17 May  (W4)
- [ ] Sat 23 May  [ ] Sun 24 May  (W5)
- [ ] Sat 30 May  [ ] Sun 31 May  (W6)
- [ ] Sat 6 Jun   [ ] Sun 7 Jun   (W7)
- [ ] Sat 13 Jun  [ ] Sun 14 Jun  (W8)

If these aren't getting ticked, the plan isn't working — rest is load-bearing.

---

## Emergency shortcuts (use sparingly, in this order)

1. Cut Week 7 polish days; ship rougher
2. Cut 1 of the 3 planned project features
3. Cut the Day 40 blog post (do it later)
4. Cut Playwright tests, keep Vitest only
5. Extend by 1–2 weeks rather than cutting core content

**Never cut**: Week 1 foundations · Week 4 Next.js mental model · The eval harness · Deployment

---

*Generated 2026-04-16. Commit this file to `roadmap-work` and tick boxes as you go.*
