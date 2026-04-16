# Progress Tracker — Realistic Edition (v2)

Daily checklist matching `combined-roadmap-v2.md`. Tick boxes as you go.

**Timeline**: 8 weeks • Mon–Fri • 5h/day (2.5h fullstack + 2.5h agents)
**Start date**: _fill in_ • **Target end date**: _fill in_ (40 working days later)

---

## Progress summary

- Days completed: **0 / 40**
- Milestones hit: **0 / 8**
- Rest days taken: **0 / 16** (should be at least 14 by the end — 2 per week × 8)

---

## Week 1 — Foundations

### Day 1 (Mon)
- [ ] **FS**: JS closures, lexical scope (Coursera + javascript.info)
- [ ] **AG**: API key + credit, install `anthropic`, first CLI that prints response + tokens

### Day 2 (Tue)
- [ ] **FS**: JS `this`, prototypes, classes
- [ ] **AG**: Read prompt eng overview; build multi-turn chat CLI with history

### Day 3 (Wed)
- [ ] **FS**: Promises, async/await, event loop — build parallel fetch script
- [ ] **AG**: Read CoT + XML tags + system prompts; write 5 progressive prompts for one task

### Day 4 (Thu)
- [ ] **FS**: Destructuring, spread, optional chaining, array methods, Map/Set, modules
- [ ] **AG**: Read tool use docs; write the agent loop on paper

### Day 5 (Fri)
- [ ] **FS**: Node + npm project setup; rewrite day-3 script properly
- [ ] **AG**: Implement `read_file` / `write_file` / `list_dir` tools (single-turn)

- [ ] 🏁 **Week 1 milestone**: comfortable with JS + Promises; first tool call working

### Weekend 1 (Sat–Sun)
- [ ] Actually rested

---

## Week 2 — React + the Agent Loop

### Day 6 (Mon)
- [ ] **FS**: React basics — components, JSX, props, `useState`
- [ ] **AG**: Full agent loop — iterate until `end_turn`

### Day 7 (Tue)
- [ ] **FS**: `useEffect`, events, lists, conditional rendering
- [ ] **AG**: Test agent on "add docstrings"; fix what breaks (this is v0)

### Day 8 (Wed)
- [ ] **FS**: **Build todo app in React + Vite, plain JS**
- [ ] **AG**: Add `run_bash` (safe); first pass of "Building effective agents"

### Day 9 (Thu)
- [ ] **FS**: Finish todo app; split into components
- [ ] **AG**: Add `grep`/`find`; sandbox agent to `./workspace`

### Day 10 (Fri)
- [ ] **FS**: Review React rendering; add one more todo feature
- [ ] **AG**: Structured logging with `rich`; test on messy Python file

- [ ] 🏁 **Week 2 milestone**: todo app works; hand-rolled agent runs on real tasks

### Weekend 2
- [ ] Rested

---

## Week 3 — TypeScript + a Proper Agent

### Day 11 (Mon)
- [ ] **FS**: TS — basics, everyday types, narrowing; TS project with `strict: true`
- [ ] **AG**: Prompt caching docs; add caching to system prompt + tools

### Day 12 (Tue)
- [ ] **FS**: TS — functions, object types; Matt Pocock beginner tutorial
- [ ] **AG**: Measure cost before/after caching on 20-turn run

### Day 13 (Wed)
- [ ] **FS**: TS — generics, keyof, utility types
- [ ] **AG**: Re-read "Building effective agents"; start refactoring agent

### Day 14 (Thu)
- [ ] **FS**: TS — discriminated unions, type guards, `as const`, `satisfies`
- [ ] **AG**: Finish "proper" agent — clean prompt, 5–7 tools, sandboxed, logged

### Day 15 (Fri)
- [ ] **FS**: **Rewrite todo app in TypeScript**
- [ ] **AG**: Test on 3 different coding tasks; note failures (data for evals)

- [ ] 🏁 **Week 3 milestone**: typed todo app; "proper" agent you're proud of

### Weekend 3
- [ ] Rested

---

## Week 4 — Next.js + Agent SDK

### Day 16 (Mon)
- [ ] **FS**: Next.js learn course — App Router, file conventions
- [ ] **AG**: Agent SDK overview + quickstart; install + run bug-fix quickstart

### Day 17 (Tue)
- [ ] **FS**: **Server vs Client Components** — the main new mental model
- [ ] **AG**: Compare hand-rolled vs SDK; note what you got for free

### Day 18 (Wed)
- [ ] **FS**: Route handlers, Server Actions, data fetching, dynamic routes
- [ ] **AG**: Permissions guide; build read-only code reviewer (Read/Glob/Grep only)

### Day 19 (Thu)
- [ ] **FS**: SQL + Postgres review; Neon free tier; Drizzle setup
- [ ] **AG**: MCP intro; install `mcp` SDK; start a simple MCP server

### Day 20 (Fri)
- [ ] **FS**: **Build notes CRUD in Next.js** with Drizzle + Neon
- [ ] **AG**: Finish MCP server — `search_my_notes` + `summarize_commit`; wire into agent

- [ ] 🏁 **Week 4 milestone**: notes app in Next.js + Postgres; MCP agent working

### Weekend 4
- [ ] Rested

---

## Week 5 — Production Essentials

### Day 21 (Mon)
- [ ] **FS**: Tailwind docs; install shadcn/ui
- [ ] **AG**: Eval guidance doc; design YAML test-case format

### Day 22 (Tue)
- [ ] **FS**: **Restyle notes app** with Tailwind + shadcn
- [ ] **AG**: Build eval harness; 10 test cases running

### Day 23 (Wed)
- [ ] **FS**: Auth.js — sessions, OAuth, password hashing; add signup/login
- [ ] **AG**: Tracing with JSONL + pretty-printer; instrument agent

### Day 24 (Thu)
- [ ] **FS**: Finish auth — users see only own notes; protect routes
- [ ] **AG**: Grow evals to 25 cases; fix top 2 failure modes

### Day 25 (Fri)
- [ ] **FS**: Next.js caching basics; `useOptimistic` for CRUD
- [ ] **AG**: Implement **prompt chaining** pattern on a real task

- [ ] 🏁 **Week 5 milestone**: auth'd styled notes app; 25-case eval harness

### Weekend 5
- [ ] Rested (halfway point — notice how you're doing)

---

## Week 6 — Start Your Project

Project name: _______________________

### Day 26 (Mon)
- [ ] **FS**: Scaffold Next.js + Drizzle + Neon; define schema; migrations
- [ ] **AG**: Plan agent feature — tools, success criteria, 5 eval cases

### Day 27 (Tue)
- [ ] **FS**: Auth flow, base layout, shadcn components
- [ ] **AG**: Implement **orchestrator-workers** pattern

### Day 28 (Wed)
- [ ] **FS**: Core CRUD — forms, server actions, route handlers
- [ ] **AG**: First agent endpoint — POST `/api/agent/run` with SSE streaming

### Day 29 (Thu)
- [ ] **FS**: External API integration; error handling; loading states
- [ ] **AG**: Wire agent endpoint into client component; stream tokens into UI

### Day 30 (Fri)
- [ ] **FS**: Env vars, Zod-validated `process.env`, Sentry
- [ ] **AG**: Authenticate agent endpoint; add `max_tokens` + early-abort caps

- [ ] 🏁 **Week 6 milestone**: project deployed (rough); first agent endpoint working

### Weekend 6
- [ ] Rested

---

## Week 7 — Build

### Day 31 (Mon)
- [ ] **FS**: Feature 2
- [ ] **AG**: Upstash rate limiting; log user + prompt + tool calls + cost per run

### Day 32 (Tue)
- [ ] **FS**: Feature 3; think about edge cases
- [ ] **AG**: 15 more eval cases for the integrated feature; run them

### Day 33 (Wed)
- [ ] **FS**: Polish one rough area — loading/empty/error states
- [ ] **AG**: Refine system prompt from eval failures; measure improvement

### Day 34 (Thu)
- [ ] **FS**: Lighthouse pass; fix top 3 flags; `next/image`
- [ ] **AG**: Trace inspection — 3 failed runs; fix or document

### Day 35 (Fri)
- [ ] **FS**: DB perf — `EXPLAIN`, add indexes
- [ ] **AG**: Buffer day — catch up on slippage, or read aider source

- [ ] 🏁 **Week 7 milestone**: 3+ features + solid agent feature; both tested

### Weekend 7
- [ ] Rested

---

## Week 8 — Ship It

### Day 36 (Mon)
- [ ] **FS**: Vitest — 10–15 unit tests on business logic (no UI tests)
- [ ] **AG**: Make eval report legible (someone else could read pass/fail + cost)

### Day 37 (Tue)
- [ ] **FS**: Playwright — 2 end-to-end tests on critical flows
- [ ] **AG**: "Recent runs" page for logged-in user (good for demos)

### Day 38 (Wed)
- [ ] **FS**: GitHub Actions CI — tests run on push
- [ ] **AG**: Design doc for agent feature in the README (2–3 paragraphs)

### Day 39 (Thu)
- [ ] **FS**: Polished README — screenshots, live demo, architecture. Custom domain optional
- [ ] **AG**: Eval results in README; 2-minute Loom demo video

### Day 40 (Fri)
- [ ] **FS**: **Ship announcement** — post somewhere or tell someone
- [ ] **AG**: Write up ONE hard-won lesson as blog/README section

- [ ] 🏁 **Week 8 milestone**: **deployed, tested, documented project with AI feature**

### Weekend 8
- [ ] Rested (celebrate — you shipped)

---

## Tracking data (update weekly)

End-of-week honesty check:

### Week 1
- Hours actually worked: _____
- One thing learned: _____
- Anything to adjust? _____

### Week 2
- Hours actually worked: _____
- One thing learned: _____
- Anything to adjust? _____

### Week 3
- Hours actually worked: _____
- One thing learned: _____
- Anything to adjust? _____

### Week 4
- Hours actually worked: _____
- One thing learned: _____
- Anything to adjust? _____

### Week 5 (halfway — big check-in)
- Hours actually worked across weeks 1–5: _____
- Still sustainable? _____
- Any skipped content worth revisiting? _____
- Project idea locked in? _____

### Week 6
- Hours actually worked: _____
- Project progress vs plan: _____

### Week 7
- Hours actually worked: _____
- What's the riskiest thing still unshipped? _____

### Week 8
- Hours actually worked: _____
- What I'm most proud of: _____
- What I'd do differently: _____

---

## Rest day log (aim for 2/week)

Tick every weekend day you genuinely rested:

- [ ] Sat W1  [ ] Sun W1
- [ ] Sat W2  [ ] Sun W2
- [ ] Sat W3  [ ] Sun W3
- [ ] Sat W4  [ ] Sun W4
- [ ] Sat W5  [ ] Sun W5
- [ ] Sat W6  [ ] Sun W6
- [ ] Sat W7  [ ] Sun W7
- [ ] Sat W8  [ ] Sun W8

If these boxes aren't getting ticked, the plan isn't working as designed — the rest is load-bearing.

---

## Emergency shortcuts (use sparingly)

If you're dangerously behind and need to cut further, in order of first-to-cut:

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

*Tracker v2 generated 2026-04-16. Tick, commit, rest, repeat.*
