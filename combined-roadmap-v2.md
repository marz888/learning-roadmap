# Combined Roadmap — Realistic Edition (v2)

**Timeline**: 8 weeks.
**Cadence**: 5 days/week (Mon–Fri). Weekends fully off.
**Daily load**: 5 hours — 2.5h full-stack + 2.5h agents.
**Total**: 40 working days, 200 hours of study.

This replaces the original 6-week, 6h/day, 7-day plan. It's trimmed from the original content, not just stretched — read the "What's been cut" section below so you know what you're trading.

---

## Why this shape

- **5h/day is sustainable.** The original 6h/day was aspirational. 5h with weekends off lets your brain consolidate; learning happens during rest as much as during work.
- **Balanced split.** 2.5h + 2.5h keeps both tracks progressing together. A lopsided 3+2 ends up 4+1 in practice because the heavier track dominates attention.
- **Weekends off, no exceptions.** If you miss a weekday, you stretch the plan — you don't work Saturday. Rest is load-bearing, not optional.
- **Single-project convergence.** Weeks 6–8 merge into one deployed full-stack app with integrated agent features. You finish with one portfolio piece, not two.

---

## What's been cut from the original

I need to be transparent about this. Moving from 42h/week to 25h/week means real content loss. Here's what's gone and why it's OK:

- **Raw Fastify / Node HTTP backend deep-dive** — Next.js route handlers + Server Actions teach the same request-lifecycle thinking. You can always circle back if you need to build non-Next.js backends later.
- **Separate TypeScript port of your Python agent** — in the original plan this was "rewrite your Python agent in TS for practice." Now you just write the Next.js-integrated agent in TS directly when you need it. Half the work, same outcome.
- **Implementing all 5 agent patterns** — trimmed to implementing 2 patterns well (prompt chaining + orchestrator-workers). You'll recognize the other three; you won't have built them.
- **Deep testing week** — kept unit tests for business logic and 2 end-to-end Playwright tests for critical paths. Cut: comprehensive component testing. Most employable projects don't have it either.
- **"Read real code" week** — reduced from 3 days to 1 afternoon. You'll still do it, just less deeply.

What's **not** cut: TypeScript fundamentals, the hand-rolled agent loop, MCP, evals, auth, database design, deployment, and shipping a real project. The core is intact.

---

## Daily structure (5h)

Split each day roughly:

- **2.5h full-stack** (morning, your best cognitive slot): deep work, new concepts, hard building
- **2.5h agents** (afternoon, after a break): tool use, prompts, agent building

Put a real break between the two blocks — lunch, a walk, a nap. Context-switching costs ~20 minutes of focus; you want that cost amortized over a single switch, not three.

Within each 2.5h block:
- **~1h** reading docs / watching course / taking notes
- **~1.5h** hands-on coding

Push harder on building than watching.

---

## Week-by-week overview

| Week | Full-stack focus | Agent focus | Milestone |
|------|------------------|-------------|-----------|
| 1 | JavaScript deep dive | LLM + API + prompt basics | First API call, first fetch script |
| 2 | React fundamentals | Tool use from scratch | Todo app in React; hand-rolled agent loop |
| 3 | TypeScript + typed React | Agent loop → real coding agent | Typed todo app; 5-tool sandboxed agent |
| 4 | Next.js App Router + DB | Claude Agent SDK + MCP | Notes app in Next.js; agent with custom MCP |
| 5 | Auth + styling + caching | Evals + tracing + patterns | Auth'd notes app; eval harness with 25 cases |
| 6 | Start personal project | Port agent work into project | Project scaffolded with first agent endpoint |
| 7 | Build project features | Deepen agent integration | Core features shipped |
| 8 | Polish, test, deploy | Eval + trace the agent feature | **Deployed project with AI feature** |

---

## Week 1 — Foundations

### Day 1 (Mon)
- **Full-stack (2.5h)**: Start Coursera *Programming with JavaScript* (Meta). Cover: closures, lexical scope. Write small examples as you go.
- **Agents (2.5h)**: Sign up at console.anthropic.com, add $10 credit. `pip install anthropic python-dotenv`. Read [Anthropic API Quickstart](https://docs.claude.com/en/api/getting-started). Build a CLI that takes a prompt, prints response + token usage.

### Day 2 (Tue)
- **Full-stack**: JS — `this`, prototypes, classes (javascript.info ch. 4, 6).
- **Agents**: Read prompt engineering overview + "Be clear and direct" + "Use examples". Build multi-turn chat CLI maintaining message history.

### Day 3 (Wed)
- **Full-stack**: JS — **Promises, async/await, event loop**. Most important day of the week. Build a Node script fetching 3 APIs in parallel with `Promise.all`.
- **Agents**: Read "Let Claude think" (CoT) + "Use XML tags" + "System prompts". Write 5 progressively-better prompts for a fuzzy task, save each output.

### Day 4 (Thu)
- **Full-stack**: Modern JS — destructuring, spread, optional chaining, array methods, Map/Set, modules.
- **Agents**: Read [Tool use overview](https://docs.claude.com/en/docs/agents-and-tools/tool-use/overview) + ["How tool use works"](https://docs.claude.com/en/docs/agents-and-tools/tool-use/how-tool-use-works). Write the agent loop on paper — understand every variable.

### Day 5 (Fri)
- **Full-stack**: Node basics — `nvm`, Node 20+, `package.json`, ESM, `.gitignore`. Rewrite day-3 script as a proper npm project with CLI args.
- **Agents**: Implement `read_file`, `write_file`, `list_dir` tools (no SDK, just `anthropic.messages.create`). Get Claude to call them in a single-turn test.

**Weekend**: off. Don't code.

**Week 1 milestone**: Comfortable with modern JS and Promises. First tool-using prompt working (single turn, no loop yet).

---

## Week 2 — React + the Agent Loop

### Day 6 (Mon)
- **Full-stack**: Start *React Basics* / react.dev tutorial. Function components, JSX, props, state (`useState`).
- **Agents**: Wrap yesterday's tools in a while loop — **implement the full agent loop**. Keep iterating until Claude says `end_turn`.

### Day 7 (Tue)
- **Full-stack**: React — `useEffect` (and when NOT to use it), events, lists, conditional rendering.
- **Agents**: Test your agent on "add docstrings to utils.py". Watch it work. Fix what breaks. This is your **Tiny coding agent v0**.

### Day 8 (Wed)
- **Full-stack**: **Build todo app in React + Vite, plain JS**. Features: add, delete, toggle, filter. Local state only.
- **Agents**: Expand tools — add `run_bash` (whitelisted commands, timeout via `subprocess`). Read ["Building effective agents"](https://www.anthropic.com/engineering/building-effective-agents) (first pass).

### Day 9 (Thu)
- **Full-stack**: Finish todo app; clean up state management. Try splitting into multiple components.
- **Agents**: Add `grep`/`find` tool. Start building a "real" agent: focused system prompt, working-directory sandbox (agent can't escape `./workspace`).

### Day 10 (Fri)
- **Full-stack**: Review React rendering behavior. Read [react.dev on state](https://react.dev/learn/managing-state). Add one more feature to the todo app.
- **Agents**: Add structured logging of every tool call (rich printing with the `rich` library helps here). Test agent on a messy Python file.

**Week 2 milestone**: Todo app works. Hand-rolled coding agent with 4–5 tools runs to completion on real tasks.

---

## Week 3 — TypeScript + a Proper Agent

### Day 11 (Mon)
- **Full-stack**: TS Handbook — "The Basics" + "Everyday Types" + "Narrowing". Set up a TS project from scratch with `strict: true`.
- **Agents**: Read prompt caching docs. Add caching to your agent's system prompt and tool definitions.

### Day 12 (Tue)
- **Full-stack**: TS Handbook — "Functions" + "Object Types". Start [Matt Pocock's Beginner's TypeScript](https://www.totaltypescript.com/tutorials/beginners-typescript).
- **Agents**: Measure agent cost before/after caching on a 20-turn run. Write down the savings.

### Day 13 (Wed)
- **Full-stack**: TS — Generics, Keyof, utility types (`Partial`, `Pick`, `Omit`, `Record`).
- **Agents**: Re-read "Building effective agents" (second pass — different paragraphs will hit). Start refactoring your agent with what you've learned.

### Day 14 (Thu)
- **Full-stack**: TS — discriminated unions, type guards, `as const`, `satisfies`.
- **Agents**: Finish the "proper" agent — clean system prompt, 5–7 well-designed tools, sandboxed, logged.

### Day 15 (Fri)
- **Full-stack**: **Rewrite the todo app in TypeScript**. Reference the [React+TS cheatsheet](https://react-typescript-cheatsheet.netlify.app). Type props, events, state.
- **Agents**: Test your real agent on 3 different coding tasks. Note where it fails — this is data for evals later.

**Week 3 milestone**: Typed todo app. "Proper" coding agent you're proud of.

---

## Week 4 — Next.js + Agent SDK

### Day 16 (Mon)
- **Full-stack**: Start the [Next.js learn course](https://nextjs.org/learn). App Router, file conventions (`page.tsx`, `layout.tsx`, `loading.tsx`, `error.tsx`).
- **Agents**: Read [Agent SDK overview](https://docs.claude.com/en/docs/agent-sdk/overview) + [quickstart](https://docs.claude.com/en/docs/agent-sdk/quickstart). Install `claude-agent-sdk`. Run the bug-fix quickstart.

### Day 17 (Tue)
- **Full-stack**: Next.js — **Server Components vs Client Components** (`"use client"`). This is the main new mental model. Take your time.
- **Agents**: Compare hand-rolled vs SDK versions. Note what the SDK gives you for free.

### Day 18 (Wed)
- **Full-stack**: Next.js — route handlers (API routes), Server Actions, data fetching in Server Components. Dynamic routes.
- **Agents**: Read Agent SDK permissions guide. Configure a **read-only code reviewer** (only `Read`, `Glob`, `Grep`). Point it at a small OSS repo.

### Day 19 (Thu)
- **Full-stack**: SQL + Postgres review — schema design, keys, joins, indexes, `EXPLAIN`. Set up Neon free tier. Install Drizzle.
- **Agents**: Read [MCP intro](https://modelcontextprotocol.io). Install the Python `mcp` SDK. Start a simple MCP server.

### Day 20 (Fri)
- **Full-stack**: **Build notes CRUD in Next.js** — Server Components for reads, Server Actions for writes, Drizzle + Neon for storage. Schema: notes + users.
- **Agents**: Finish MCP server — expose `search_my_notes(query)` + `summarize_commit(sha)`. Wire it into your Agent SDK agent.

**Week 4 milestone**: Notes app working in Next.js + Postgres. Agent SDK + custom MCP tools both functional.

---

## Week 5 — Production Essentials

### Day 21 (Mon)
- **Full-stack**: Tailwind docs — flexbox/grid utilities, responsive prefixes, dark mode. Install shadcn/ui.
- **Agents**: Read [Anthropic's eval guidance](https://docs.claude.com/en/docs/test-and-evaluate/develop-tests). Design your YAML test-case format.

### Day 22 (Tue)
- **Full-stack**: **Restyle the notes app** with Tailwind + shadcn. Proper layout, responsive, dark mode.
- **Agents**: Build eval harness — runner + pass/fail/duration/cost report. Start with 10 test cases.

### Day 23 (Wed)
- **Full-stack**: Pick Auth.js. Learn sessions vs JWTs, OAuth, password hashing. Add signup/login to notes app.
- **Agents**: Pick tracing approach (start with JSONL files + a pretty-printer). Instrument your agent — you should be able to replay any run.

### Day 24 (Thu)
- **Full-stack**: Finish auth — users see only their own notes, protect server actions + API routes.
- **Agents**: Grow evals to 25 cases. Run them against your real agent. Fix the top 2 failure modes.

### Day 25 (Fri)
- **Full-stack**: Next.js caching basics — static vs dynamic rendering, `revalidatePath`. Add `useOptimistic` for note CRUD.
- **Agents**: Implement **prompt chaining** pattern (extract → transform → verify) on a real task. Compare to single-shot.

**Week 5 milestone**: Notes app with auth, styling, good UX. Eval harness with 25 cases + traces.

---

## Week 6 — Start Your Project

Stop following tutorials. Pick one project (≥3 tables with relationships, auth, external API, non-trivial UI, will deploy). Project name: _______________

Ideas that lean into your systems background:
- **Self-hosted bookmark manager** with tagging, search, + an "auto-summarize URL" agent feature
- **Code snippet manager** with syntax highlighting, search, + a "refactor this snippet" agent
- **Rate-limited API gateway** that proxies APIs with auth + logging + an agent that explains failures

Pick one that actually solves a problem you have. Motivation matters at this stage.

### Day 26 (Mon)
- **Full-stack**: Scaffold Next.js app, set up Drizzle + Neon, define schema, initial migrations.
- **Agents**: Plan the agent feature — what tools does it need, what does success look like, what are 5 eval cases for it?

### Day 27 (Tue)
- **Full-stack**: Auth flow, base layout, shadcn components for primary UI.
- **Agents**: Implement **orchestrator-workers** pattern — the shape most real integrated agents take.

### Day 28 (Wed)
- **Full-stack**: Core CRUD — forms, server actions, route handlers.
- **Agents**: Build your first agent endpoint in Next.js — POST `/api/agent/run`, SSE streaming (use [Vercel AI SDK](https://ai-sdk.dev/docs/introduction) helpers or raw `ReadableStream`).

### Day 29 (Thu)
- **Full-stack**: External API integration (whichever your project needs). Error handling, loading states.
- **Agents**: Wire the agent endpoint into a client component that streams tokens into the UI.

### Day 30 (Fri)
- **Full-stack**: Environment variables, Zod-validated `process.env`, error monitoring (Sentry free tier).
- **Agents**: Authenticate the agent endpoint with your Auth.js session. Add per-request cost cap (`max_tokens`, early-abort).

**Week 6 milestone**: Project scaffolded and deployed in a rough state. First agent endpoint runs end-to-end.

---

## Week 7 — Build

Heads-down week. Less reading, more shipping.

### Day 31 (Mon)
- **Full-stack**: Feature 2 of the project.
- **Agents**: Add per-user rate limiting (Upstash Ratelimit). Log every agent run with user + prompt + tool calls + cost.

### Day 32 (Tue)
- **Full-stack**: Feature 3 of the project. Start thinking about edge cases.
- **Agents**: Add 15 more eval cases specific to the integrated agent feature. Run them in CI if you can manage it; locally if not.

### Day 33 (Wed)
- **Full-stack**: Polish one rough area — loading states, empty states, error states.
- **Agents**: Refine the agent's system prompt based on eval failures. Re-run evals, measure improvement.

### Day 34 (Thu)
- **Full-stack**: Performance pass — Lighthouse on your deployed URL, fix top 3 flags. `next/image` for any images.
- **Agents**: Trace inspection — pick 3 failed runs, understand why. Fix or document.

### Day 35 (Fri)
- **Full-stack**: Database perf — look at slow queries, add indexes where needed. Run `EXPLAIN` on 2–3 queries.
- **Agents**: Buffer day for whatever agent work slipped this week. If caught up, read [aider's source](https://github.com/Aider-AI/aider) for patterns.

**Week 7 milestone**: Project has 3+ working features and one solid agent feature. Both have tests and evals.

---

## Week 8 — Ship It

### Day 36 (Mon)
- **Full-stack**: Vitest — unit tests for business logic (don't test UI; test utilities). 10–15 tests.
- **Agents**: Make sure your eval report is legible — someone else should be able to understand pass/fail counts + cost.

### Day 37 (Tue)
- **Full-stack**: Playwright — 2 end-to-end tests covering your critical user flows (sign up → create thing → agent feature → see result).
- **Agents**: Add a "view recent runs" page to your app showing agent run history for the logged-in user. Great for demos.

### Day 38 (Wed)
- **Full-stack**: GitHub Actions — run tests on push. Fix anything that breaks in CI.
- **Agents**: Write a 2–3 paragraph design doc for the agent feature: what it does, how it works, what can go wrong. Goes in the README.

### Day 39 (Thu)
- **Full-stack**: Polished README with screenshots, live demo link, architecture overview. Custom domain if you want one.
- **Agents**: Add eval results to the README. Record a 2-minute Loom video of the feature working.

### Day 40 (Fri)
- **Full-stack**: Ship announcement. Post on your social of choice or just tell a friend. Close off the project.
- **Agents**: Pick ONE hard-won lesson and write it up as a short blog post or README section. Examples: "how I designed my agent's tools," "what my evals caught that I'd have missed," "how context management changed my system prompt."

**Week 8 milestone**: **Deployed, tested, documented project with integrated agent feature. Portfolio ready.**

---

## Rest day protocol

Weekends are not catch-up days. They are actual rest.

- **Saturday**: completely off. No coding. No tutorials. Do something non-screen if you can.
- **Sunday**: still off, but you can spend 30 minutes reviewing next week's plan and prepping your environment (pulling docs, clearing your desk). This isn't work — it's reducing Monday's friction.

If you want to code on weekends because you're enjoying it: fine, but make it something different from the roadmap (a small side-tool, a game, whatever). Don't work ahead — the rest matters more than the extra hours.

---

## Falling-behind protocol

You will miss days. Here's what to do without blowing up the plan:

- **Missed 1 day**: do nothing. The plan has natural slack in buffer days. You're still on track.
- **Missed 2–3 days in a row**: don't try to catch up by doing double days. Instead, skip ahead to where you should be. You lose the content of those specific days — that's the cost of real life.
- **Missed a whole week**: add a week to the timeline. 8 weeks becomes 9. No shame; this is the honest path.
- **Feeling fried**: take a 2-day break beyond the weekend. Return refreshed. Burnout costs more than the days you saved.

The only rule: commit *something* to the repo each working day, even if it's a note saying "today was rough, light review only." The streak is what keeps the plan alive.

---

## Daily startup ritual (5 minutes)

Do this at the start of every weekday. It's the single highest-leverage habit on this plan:

1. Open `progress.md` in GitHub.
2. Read today's two tasks out loud (silly but effective).
3. Write tomorrow's first task in your notes section *now*, so tomorrow-you doesn't have to decide.
4. Close everything except the tools you need for the first task.
5. Set a 50-minute timer. Work. Break 10 minutes. Repeat.

---

## What to track

In addition to ticking boxes, keep rough notes on:

- **Hours actually worked** (not planned) — honest data for whether 5h is working
- **One thing learned per day** — in a single sentence
- **Any code committed** — keep the green squares going

You'll want this data at week 4 to decide if you need to adjust the plan further.

---

## Expectations

After 40 days at 5h/day of honest work, you will be:

- **Confident**: writing TypeScript, building Next.js apps with auth + DB + UI, building tool-using agents, running evals, integrating agents into real apps
- **Competent**: with production essentials — deployment, tests, traces, rate limits, cost controls
- **Not yet expert**: at performance optimization, complex state management, multi-agent orchestration, accessibility, large-scale architecture

That's a realistic outcome. The original 6-week plan promised the same, but required 68% more study time to deliver it. This plan is slower on the calendar and faster in practice, because you'll actually finish it.

---

*Roadmap v2 generated 2026-04-16. Replaces the 6-week / 6-hour version. 8 weeks, 5 days/week, 5 hours/day, balanced split.*
