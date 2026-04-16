# Learning Progress Tracker

Daily checklist for the **Full-Stack TypeScript** + **Coding Agent** roadmaps. Tick boxes as you go. Every tick is a commit if you host this on GitHub.

**Daily load**: 4h full-stack + 2h agents = 6h/day.
**Duration**: 6 weeks / 42 days.
**Start date**: _fill in_ • **Target end date**: _fill in_

---

## Progress summary

- Full-stack days done: **0 / 42**
- Agent-track days done: **0 / 42**
- Milestones hit: **0 / 12**

*(Update these numbers manually as you go — or just count the ticks.)*

---

## Week 1 — JavaScript + React Fundamentals • LLM + Tool-Use Fundamentals

### Day 1
- [ ] **Full-stack**: JS deep dive — closures and lexical scope (Coursera *Programming with JS* + javascript.info ch. 2–8)
- [ ] **Agents**: Get API key, install `anthropic` SDK, build a CLI that prints a response + token usage

### Day 2
- [ ] **Full-stack**: JS deep dive — `this`, prototypes, classes
- [ ] **Agents**: Build a multi-turn chat CLI that maintains message history

### Day 3
- [ ] **Full-stack**: Promises, async/await, event loop — build a Node script fetching 3 APIs in parallel with `Promise.all`
- [ ] **Agents**: Read prompt engineering overview + "Be clear and direct" / "Use examples"

### Day 4
- [ ] **Full-stack**: Modern JS idioms (destructuring, spread, optional chaining, array methods, Map/Set, modules)
- [ ] **Agents**: Read "Let Claude think" (CoT) + "Use XML tags" + "System prompts"; write 5 progressively-better prompts for one fuzzy task

### Day 5
- [ ] **Full-stack**: Node basics — nvm, Node 20+, `npm init`, `package.json`, scripts, `.gitignore`. Rewrite day-3 script as a proper npm project with ESM + CLI args
- [ ] **Agents**: Read tool-use overview + "How tool use works". Write the agent loop pseudocode on paper

### Day 6
- [ ] **Full-stack**: Start *React Basics* (Meta) or react.dev tutorial — function components, JSX, props, state
- [ ] **Agents**: Build tool-use agent skeleton — implement `read_file`, `write_file`, `list_dir` tools (no SDK, just `messages.create`)

### Day 7
- [ ] **Full-stack**: React `useEffect`, events, lists, conditional rendering. **Build todo app in React + Vite, plain JS** (add/delete/toggle/filter)
- [ ] **Agents**: **Tiny coding agent v0** — make the loop iterate until Claude says it's done. Test on "add type hints to utils.py"

### Milestones
- [ ] 🏁 **Full-stack week 1**: Can write non-trivial JS with Promises and array methods without reference
- [ ] 🏁 **Agent week 1**: Can explain the agent loop on a whiteboard; hand-rolled agent in ~150 lines of Python

---

## Week 2 — TypeScript + React Patterns • Real Tools + Context Management

### Day 8
- [ ] **Full-stack**: TS Handbook — "The Basics" + "Everyday Types". Set up a TS project from scratch (`tsconfig.json` with `strict: true`)
- [ ] **Agents**: Add `run_bash` tool (whitelisted commands, timeout) to your agent

### Day 9
- [ ] **Full-stack**: TS Handbook — "Functions" + "Object Types" + Generics/Keyof. Start Matt Pocock's *Beginner's TypeScript*
- [ ] **Agents**: Add `grep`/`find` (or `rg`) tool. Read "Building effective agents" (1st pass)

### Day 10
- [ ] **Full-stack**: TS advanced — discriminated unions, type guards, utility types, `as const`, `satisfies`
- [ ] **Agents**: Add proper `edit_file` with line-range patches (not whole-file overwrite)

### Day 11
- [ ] **Full-stack**: React + TS — typing props, event handlers, generic components
- [ ] **Agents**: Read prompt-caching docs. Add caching to your agent's system prompt + tool defs

### Day 12
- [ ] **Full-stack**: **Rewrite the todo app in TypeScript** using react-typescript-cheatsheet
- [ ] **Agents**: Measure cost before/after caching on a 20-turn conversation. Note the savings

### Day 13
- [ ] **Full-stack**: React hooks deep dive — `useReducer`, `useContext`, `useMemo`, `useCallback`, `useRef`, custom hooks
- [ ] **Agents**: Start rebuilding agent with focused system prompt + 5–7 well-designed tools + working-dir sandbox

### Day 14
- [ ] **Full-stack**: **Multi-step form with validation** — use `useReducer`, type everything strictly
- [ ] **Agents**: Finish the "proper" coding agent — structured logging of every tool call. Test on a messy Python file

### Milestones
- [ ] 🏁 **Full-stack week 2**: Can set up a TypeScript project from scratch and write typed code
- [ ] 🏁 **Agent week 2**: Real coding agent with 5+ tools, sandboxed, logged

---

## Week 3 — Backend Fundamentals + Next.js • Claude Agent SDK + MCP

### Day 15
- [ ] **Full-stack**: HTTP/REST — build a minimal HTTP server with Node's `http` module. Understand methods, status codes, headers
- [ ] **Agents**: Read Agent SDK overview + quickstart. Install `claude-agent-sdk`. Run the bug-fix quickstart

### Day 16
- [ ] **Full-stack**: Fastify + TS — **build REST API for notes** (GET/POST/PATCH/DELETE). Validate with Zod. In-memory storage
- [ ] **Agents**: Compare hand-rolled agent vs SDK version — note what you got for free (built-in Read/Edit/Bash, permissions, subagents)

### Day 17
- [ ] **Full-stack**: SQL + Postgres review — schema design, keys, joins, indexes, transactions, `EXPLAIN`
- [ ] **Agents**: Read Agent SDK permissions guide. Understand `allowed_tools` / `disallowed_tools` / permission modes

### Day 18
- [ ] **Full-stack**: Install Postgres (or use Neon). Learn Drizzle ORM. **Connect the notes API to Postgres via Drizzle**. Add users table
- [ ] **Agents**: **Build a read-only code reviewer** — agent with only `Read`, `Glob`, `Grep`. Point at a small OSS repo

### Day 19
- [ ] **Full-stack**: Next.js learn course (part 1) — App Router, `page.tsx`/`layout.tsx`/`loading.tsx`/`error.tsx`
- [ ] **Agents**: Read MCP "What is MCP" intro. Start Anthropic Skilljar MCP course (unit 1)

### Day 20
- [ ] **Full-stack**: Next.js learn course (part 2) — **Server vs Client Components** mental model. Route handlers, Server Actions
- [ ] **Agents**: Build a simple MCP server in Python — `search_my_notes(query)` tool

### Day 21
- [ ] **Full-stack**: **Rebuild notes app as Next.js app** — Server Components where possible, Server Actions for mutations
- [ ] **Agents**: Add `summarize_commit(sha)` tool to your MCP server. **Wire it into your Agent SDK agent**

### Milestones
- [ ] 🏁 **Full-stack week 3**: Understands request lifecycle browser → Next.js → database; built a Next.js app
- [ ] 🏁 **Agent week 3**: Shipped a custom agent on the SDK with own MCP tools

---

## Week 4 — Full-Stack Skills • Evals, Tracing, Agent Patterns

### Day 22
- [ ] **Full-stack**: Tailwind CSS docs — flexbox/grid utilities, responsive prefixes, dark mode
- [ ] **Agents**: Read Anthropic's eval guidance. Design your YAML test-case format

### Day 23
- [ ] **Full-stack**: shadcn/ui — install, add a few components to the notes app
- [ ] **Agents**: **Build eval harness** — runner + report (pass/fail, duration, tokens, cost). Start with 10 cases

### Day 24
- [ ] **Full-stack**: Pick Auth.js or Clerk. Learn sessions vs JWTs, OAuth, password hashing
- [ ] **Agents**: Pick tracing approach (JSONL files → Langfuse / Braintrust). Instrument your agent

### Day 25
- [ ] **Full-stack**: **Add auth to notes app** — signup, login, users see only their own notes. Protect server actions + API routes
- [ ] **Agents**: Expand evals to 25 cases. Confirm you can replay any failed run from traces

### Day 26
- [ ] **Full-stack**: Next.js caching — static vs dynamic, `cache()`, `revalidatePath`, `revalidateTag`, streaming with Suspense
- [ ] **Agents**: Re-read "Building effective agents". Implement **prompt chaining** pattern

### Day 27
- [ ] **Full-stack**: `useOptimistic`, `useActionState`, loading/error boundaries. Learn TanStack Query
- [ ] **Agents**: Implement **routing** and **parallelization** patterns. Compare to single-shot

### Day 28
- [ ] **Full-stack**: **Add to notes app**: search, pagination, tags, optimistic UI for CRUD
- [ ] **Agents**: Implement **orchestrator-workers** and **evaluator-optimizer** patterns. Grow evals to 50 cases

### Milestones
- [ ] 🏁 **Full-stack week 4**: Real, styled, authenticated full-stack app with good UX
- [ ] 🏁 **Agent week 4**: Production-shaped agent with evals + traces + deliberate architecture

---

## Week 5 — Build Your Own Project • TypeScript Agent SDK + Next.js Integration

Stop following tutorials. Pick a project (≥3 tables, auth, external API, non-trivial UI, deployed). _Write project name here_: ______________

### Day 29
- [ ] **Full-stack**: Project day 1 — scaffold Next.js, set up Drizzle + Neon, define schema
- [ ] **Agents**: Install `@anthropic-ai/sdk` + `@anthropic-ai/claude-agent-sdk`. Start porting your best Python agent to TS

### Day 30
- [ ] **Full-stack**: Project day 2 — auth flow, base layout, shadcn components
- [ ] **Agents**: Finish TS port. Confirm feature parity with Python version

### Day 31
- [ ] **Full-stack**: Project day 3 — core CRUD (forms, server actions, route handlers)
- [ ] **Agents**: Build first agent endpoint in Next.js — POST `/api/agent/run` with SSE streaming

### Day 32
- [ ] **Full-stack**: Project day 4 — external API integration, error handling
- [ ] **Agents**: Stream agent output to a Next.js client component. Use Vercel AI SDK's `useChat` or manual SSE

### Day 33
- [ ] **Full-stack**: Project day 5 — environment variables, Zod-validated `process.env`, error monitoring (Sentry)
- [ ] **Agents**: Authenticate agent endpoints (tie into your existing Auth.js setup)

### Day 34
- [ ] **Full-stack**: Project day 6 — polish UX, loading/error states, empty states
- [ ] **Agents**: Add per-user rate limits (Upstash Ratelimit). Add per-request cost caps

### Day 35
- [ ] **Full-stack**: **Deploy to Vercel + Neon**. Custom domain (optional). Confirm working in production
- [ ] **Agents**: Log every agent run (user, prompt, tool calls, cost). Confirm logged to your tracing backend

### Milestones
- [ ] 🏁 **Full-stack week 5**: Deployed personal project live on the internet
- [ ] 🏁 **Agent week 5**: Real agent feature deployed on top of Next.js app

---

## Week 6 — Professional Polish • Ship It + Deepen

### Day 36
- [ ] **Full-stack**: Vitest — unit tests for utilities and business logic
- [ ] **Agents**: Merge tracks — pick one agent feature to add to your project that genuinely improves it

### Day 37
- [ ] **Full-stack**: React Testing Library — component tests for 2–3 key components
- [ ] **Agents**: Build that feature (day 1 of 3) — scope and design tools

### Day 38
- [ ] **Full-stack**: Playwright — 2–3 critical end-to-end user flows
- [ ] **Agents**: Build that feature (day 2 of 3) — implement + wire into UI

### Day 39
- [ ] **Full-stack**: Performance — bundle analyzer, Lighthouse, Core Web Vitals. Fix what it flags
- [ ] **Agents**: Build that feature (day 3 of 3) — add evals for it, write trace replay script

### Day 40
- [ ] **Full-stack**: DB perf — `EXPLAIN`, indexes, N+1. `next/image` optimization
- [ ] **Agents**: Read real agent code — skim claude-code or aider for 1h. Note 3 patterns you'll steal

### Day 41
- [ ] **Full-stack**: Read the source of cal.com, dub.co, or documenso for 1h. Note patterns
- [ ] **Agents**: Write a short blog post / README section on one hard-won lesson (context mgmt, eval insight, tool-design mistake)

### Day 42
- [ ] **Full-stack**: GitHub Actions CI/CD — run tests on push, deploy on merge. Write polished README with screenshots + demo link
- [ ] **Agents**: Record a 2-min demo video. Add eval results + trace examples to project README. **Ship announcement**

### Milestones
- [ ] 🏁 **Full-stack week 6**: Portfolio-ready project; full lifecycle code → production understood
- [ ] 🏁 **Agent week 6**: Portfolio-quality agent feature shipped with evals + traces + write-up

---

## Notes & reflections

Use this space to jot down what you learned, blockers, things to revisit. Dated entries help future-you.

### Week 1
_..._

### Week 2
_..._

### Week 3
_..._

### Week 4
_..._

### Week 5
_..._

### Week 6
_..._

---

## If you fall behind

The 6-hour/day load is heavy. If you're falling behind, prioritize in this order:

1. **Main roadmap daily tasks** — web fundamentals compound faster and are harder to catch up on
2. **Agent-track milestone tasks only** (days 7, 14, 21, 28, 35, 42) — skip the in-between days rather than skimping on either track
3. **Agent-track daily tasks** — catch these up on weekends if possible

Better to finish week 4 of both tracks well than week 6 of both tracks shallowly. Adjust ruthlessly.

---

*Tracker generated 2026-04-16. Tick, commit, repeat.*
