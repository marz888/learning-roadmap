# Detailed Roadmap with Resources

**Timeline**: 8 weeks + prep day · Mon–Fri · 5h/day · 41 working days  
**Split**: 2.5h fullstack (FS) each morning + 2.5h agents (AG) each afternoon  
**Start**: Fri 17 Apr 2026 · **End**: Fri 12 Jun 2026

Within each 2.5h block: ~1h reading/watching, ~1.5h building. Push harder on building.

---

## Before anything else — read these three

Do this on prep day. They shape how you'll think about everything else.

| Doc | Why |
|-----|-----|
| [Building effective agents](https://www.anthropic.com/engineering/building-effective-agents) | Single most important thing on this roadmap. Distinguishes workflows from agents, covers the five core patterns. Read it now, re-read it at week 4, re-read monthly after. |
| [How we built our multi-agent research system](https://www.anthropic.com/engineering/built-multi-agent-research-system) | A real production agent story. Concrete lessons on context management, orchestration, and what actually breaks. |
| [Prompt engineering overview](https://docs.claude.com/en/docs/build-with-claude/prompt-engineering/overview) | Index page for Anthropic's prompt guide. Skim it, bookmark the sub-pages, return as needed. |

Total reading: ~90 minutes. Highest-leverage 90 minutes on the whole roadmap.

---

## The 5 workflow patterns — reference card

Everything in the agent track maps onto these five patterns from [Building effective agents](https://www.anthropic.com/engineering/building-effective-agents). Read this now; you'll build all five on Day 25.

| Pattern | Shape | When to reach for it | Where in the roadmap |
|---------|-------|----------------------|----------------------|
| **Prompt chaining** | A → B → C (sequential, gated) | Multi-step tasks where each step needs the previous output; you want a quality gate between steps | Day 25 (build) |
| **Parallelisation** | A → [B, C, D] → merge | Independent subtasks; or voting/consensus across N identical calls | Day 25 (build), Day 35 (apply to project) |
| **Routing** | classify → dispatch to specialist | Inputs that fall into distinct categories, each needing a different prompt or toolset | Day 25 (build), Day 27 (apply to project) |
| **Orchestrator-workers** | planner → N executors | Tasks too unpredictable to pre-define as a fixed pipeline; orchestrator decides at runtime | Day 25 (build), Day 27 (apply to project) |
| **Evaluator-optimizer** | generate → critique → improve (loop) | Open-ended output where you can define "better" but not a precise correct answer | Day 25 (build), Day 35 (apply to project) |

**Workflows vs agents**: the patterns above are *workflows* — deterministic or near-deterministic multi-step LLM pipelines. A true *agent* is different: it uses the model to decide its own control flow dynamically, with tools. In practice most production systems are hybrid: an outer workflow orchestrates one or more inner agents. You'll build both.

---

## Prep Day — Fri 17 Apr

No new concepts today. Get the environment sorted so Monday starts clean.

### Tasks

- **Toolchain**: install [nvm](https://github.com/nvm-sh/nvm) → `nvm install 20`, Python 3.12, [uv](https://github.com/astral-sh/uv) (`curl -LsSf https://astral.sh/uv/install.sh | sh`), git
- **API access**: sign up at [console.anthropic.com](https://console.anthropic.com), add $10 credit, set a hard spending cap in the console settings — do this now
- **Hello world**: `pip install anthropic python-dotenv` → run a one-shot curl or Python snippet against the API to confirm your key works
- **JS orientation**: skim [javascript.info table of contents](https://javascript.info) — note what's unfamiliar vs what maps to things you know from C/Python
- **Repo**: create a GitHub repo called `roadmap-work`; commit an empty README — you'll commit here every working day

### Install once, use everywhere

```
uv                   # Python package manager — faster than pip, standard in MCP ecosystem
nvm + Node 20        # needed for Agent SDK CLI later
python-dotenv        # .env key management
anthropic            # Anthropic Python SDK
rich                 # pretty terminal output — install now, use from week 2
```

---

## Week 1 — Foundations
**Mon 20 – Fri 24 Apr · Milestone: first tool call working; JS Promises comfortable**

### Day 1 — Mon 20 Apr

**FS — JS closures & scope (2.5h)**

- Primary: [javascript.info — Variable scope, closure](https://javascript.info/closure) (ch. 6) — read and run every example
- Supplement: [Coursera — Programming with JavaScript (Meta)](https://www.coursera.org/learn/programming-with-javascript) — use as a paced companion if you prefer video; audit for free
- C/Python frame: closures are like a C function pointer that also captures its surrounding stack frame. JS just makes this the default.
- Build: write 3–5 small closure examples from scratch (counter factory, memoiser, once-fn)

**AG — API setup & first call (2.5h)**

- Read: [Anthropic API Quickstart](https://docs.claude.com/en/api/getting-started)
- Reference (bookmark now): [Messages API reference](https://docs.claude.com/en/api/messages) — you'll return to this constantly
- Do: [Anthropic courses — `anthropic_api_fundamentals`](https://github.com/anthropics/courses) (Jupyter notebooks, free, run locally)
- Build: CLI script — takes a prompt as argv, prints the text response + input/output token counts

---

### Day 2 — Tue 21 Apr

**FS — `this`, prototypes, classes (2.5h)**

- Read: [javascript.info — Object methods, `this`](https://javascript.info/object-methods) and [Prototypal inheritance](https://javascript.info/prototype-inheritance) (ch. 4, 6)
- C/Python frame: `this` ≈ Python's `self`; the prototype chain ≈ a vtable or `__mro__`. Unlike C, `this` is resolved at call time, not definition time — that's the gotcha.
- Build: rewrite a small Python class you know well as a JS class. Note what's different.

**AG — Prompt engineering basics (2.5h)**

- Read: [Prompt engineering overview](https://docs.claude.com/en/docs/build-with-claude/prompt-engineering/overview) — skim the index, then read "Be clear and direct" and "Use examples" in full
- Do: [Anthropic courses — `prompt_engineering_interactive_tutorial`](https://github.com/anthropics/courses) (Jupyter, free)
- Build: multi-turn chat CLI — maintain a `messages` list, append each user/assistant turn, keep sending the full history

---

### Day 3 — Wed 22 Apr

**FS — Promises, async/await, event loop (2.5h)**

> Most important FS day of Week 1. Take your time.

- Read: [javascript.info — Promises](https://javascript.info/promise-basics), [async/await](https://javascript.info/async-await), [Event loop](https://javascript.info/event-loop)
- Video (optional, 26 min): [What the heck is the event loop anyway? — Philip Roberts, JSConf EU](https://www.youtube.com/watch?v=8aGhZQkoFbQ) — the clearest visual explanation that exists
- C/Python frame: think of Promises as non-blocking I/O callbacks (like `epoll` + callback) but with chaining built in. `async/await` is syntactic sugar that makes it read like synchronous code.
- Build: Node script that fetches 3 different public APIs in parallel using `Promise.all`, prints results

**AG — Chain-of-thought, XML tags, system prompts (2.5h)**

- Read: [Let Claude think (CoT)](https://docs.claude.com/en/docs/build-with-claude/prompt-engineering/extended-thinking), [Use XML tags](https://docs.claude.com/en/docs/build-with-claude/prompt-engineering/use-xml-tags), [System prompts](https://docs.claude.com/en/docs/build-with-claude/prompt-engineering/system-prompts)
- Build: pick one fuzzy task (e.g. "summarise a git diff"). Write 5 progressively better prompts — plain, with CoT, with XML structure, with a system prompt, with few-shot examples. Save all 5 outputs. Notice what changes.

---

### Day 4 — Thu 23 Apr

**FS — Modern JS syntax (2.5h)**

- Read: [javascript.info — Destructuring](https://javascript.info/destructuring-assignment), [Spread/rest](https://javascript.info/rest-parameters-spread), [Optional chaining](https://javascript.info/optional-chaining), [Array methods](https://javascript.info/array-methods), [Map and Set](https://javascript.info/map-set), [Modules](https://javascript.info/modules-intro)
- C/Python frame: destructuring ≈ structured bindings (C++17) or tuple unpacking (Python). Array methods like `.map`, `.filter`, `.reduce` ≈ Python's list comprehensions and `functools`. Modules ≈ Python's `import`.
- Build: rewrite yesterday's fetch script using destructuring and array methods throughout

**AG — Tool use mental model (2.5h)**

- Read: [Tool use overview](https://docs.claude.com/en/docs/agents-and-tools/tool-use/overview) and [How tool use works](https://docs.claude.com/en/docs/agents-and-tools/tool-use/how-tool-use-works) — read both carefully, in order
- Do: [Anthropic courses — `tool_use` notebooks](https://github.com/anthropics/courses/tree/master/tool_use) — at minimum the first two notebooks
- Exercise: draw the agent loop on paper — every message, every role, every `tool_use` / `tool_result` block. Understand every variable before you write a line of code.

---

### Day 5 — Fri 24 Apr

**FS — Node project setup (2.5h)**

- Read: [Node.js — Getting started guide](https://nodejs.org/en/learn/getting-started/introduction-to-nodejs), [npm docs — package.json](https://docs.npmjs.com/cli/v10/configuring-npm/package-json)
- Topics: `nvm`, Node 20+, `package.json`, ESM (`"type": "module"`), `.gitignore`, CLI args via `process.argv`
- Build: rewrite Day 3's parallel-fetch script as a proper npm project with a `start` script and a `--help` flag

**AG — First tool implementation (2.5h)**

- Reference: [Text editor tool schema](https://docs.claude.com/en/docs/agents-and-tools/tool-use/text-editor-tool) and [Bash tool schema](https://docs.claude.com/en/docs/agents-and-tools/tool-use/bash-tool) — copy the schema shapes even if you implement your own logic
- Build: implement `read_file`, `write_file`, `list_dir` tools using `anthropic.messages.create` directly (no SDK loop yet). Get Claude to call one of them in a single-turn request. Verify the `tool_use` block comes back correctly.

🏁 **Week 1 milestone**: first tool call working; comfortable with modern JS and Promises

---

## Week 2 — React + the Agent Loop
**Mon 27 Apr – Fri 1 May · Milestone: todo app works; hand-rolled agent loop runs on real tasks**

### Day 6 — Mon 27 Apr

**FS — React fundamentals (2.5h)**

- Primary: [react.dev — Quick start](https://react.dev/learn) and [Describing the UI](https://react.dev/learn/describing-the-ui)
- Topics: function components, JSX, props, `useState`
- C/Python frame: think of a component as a C struct (holds state) with a render method. JSX compiles to function calls — it's not magic, just syntax.
- Build: 3–4 small throwaway components (counter, toggle, list renderer) to get JSX syntax into muscle memory

**AG — The full agent loop (2.5h)**

- Reference: [How tool use works](https://docs.claude.com/en/docs/agents-and-tools/tool-use/how-tool-use-works) — keep open while coding
- Build: wrap yesterday's three tools in a `while True` loop. Send the full message history each iteration. Break when `stop_reason == "end_turn"`. Add a `max_iterations` guard so a runaway agent doesn't bill you into oblivion.

---

### Day 7 — Tue 28 Apr

**FS — React hooks & rendering (2.5h)**

- Read: [react.dev — `useEffect`](https://react.dev/reference/react/useEffect), [Handling events](https://react.dev/learn/responding-to-events), [Rendering lists](https://react.dev/learn/rendering-lists), [Conditional rendering](https://react.dev/learn/conditional-rendering)
- Key point: read [You Might Not Need an Effect](https://react.dev/learn/you-might-not-need-an-effect) — saves hours of confusion later
- Build: extend yesterday's components to use `useEffect` for one real side effect (e.g. document title update)

**AG — Tiny coding agent v0 (2.5h)**

- Build: point your agent at a small Python file (`utils.py` with a few functions). Prompt: "Add docstrings to every function." Watch it run. Note every place it fails or does something unexpected. Fix one failure. This is your baseline.

---

### Day 8 — Wed 29 Apr

**FS — Build: todo app (2.5h)**

- Reference: [Vite — Getting started](https://vitejs.dev/guide/), [react.dev — Managing state](https://react.dev/learn/managing-state)
- Build: todo app in React + Vite (plain JS, no TypeScript yet). Features: add item, delete item, toggle complete, filter by status. Local state only — no backend.

**AG — `run_bash` + first read of "Building effective agents" (2.5h)**

- Read: [Building effective agents](https://www.anthropic.com/engineering/building-effective-agents) — first pass. Don't try to absorb everything; just read it straight through.
- Reference: [Python subprocess security considerations](https://docs.python.org/3/library/subprocess.html#security-considerations) — read before adding shell access
- Build: add `run_bash` tool. Whitelist commands (`pytest`, `python`, `git diff`, etc.). Add a timeout via `subprocess.run(..., timeout=30)`. Test it runs a real command and returns output.

---

### Day 9 — Thu 30 Apr

**FS — Todo app: components (2.5h)**

- Read: [react.dev — Passing props deeply](https://react.dev/learn/passing-data-deeply-with-context), [Extracting state into a reducer](https://react.dev/learn/extracting-state-logic-into-a-reducer)
- Build: finish the todo app. Split it into at least 3 components (`TodoList`, `TodoItem`, `AddTodoForm`). Pass props cleanly. No prop drilling more than one level.

**AG — Sandboxed agent (2.5h)**

- Build: add `grep` and `find` tools (wrap `subprocess`). Sandbox the agent: all file paths must be prefixed with `./workspace/`. Reject any path that tries to escape (check for `..`). This is your first security boundary — get it right.

---

### Day 10 — Fri 1 May

**FS — React rendering deep dive (2.5h)**

- Read: [react.dev — Managing state](https://react.dev/learn/managing-state) (full section), [react.dev — Preserving and resetting state](https://react.dev/learn/preserving-and-resetting-state)
- Build: add one more feature to the todo app (e.g. drag-to-reorder, or local persistence with `localStorage`)

**AG — Structured logging (2.5h)**

- Docs: [rich library — Getting started](https://rich.readthedocs.io/en/stable/introduction.html) (takes ~20 min to learn enough to be useful)
- Build: instrument your agent so every tool call logs: tool name, arguments, result (truncated to 500 chars), and elapsed time. Use `rich.table` or `rich.panel`. Test on a messy Python file with mixed indentation and missing docstrings.

🏁 **Week 2 milestone**: todo app works; hand-rolled coding agent with 4–5 tools completes real tasks

---

## Week 3 — TypeScript + a Proper Agent
**Mon 4 – Fri 8 May · Milestone: typed todo app; proper agent with 5–7 tools**

### Day 11 — Mon 4 May

**FS — TypeScript basics (2.5h)**

- Primary: [TypeScript Handbook — The Basics](https://www.typescriptlang.org/docs/handbook/2/basic-types.html), [Everyday Types](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html), [Narrowing](https://www.typescriptlang.org/docs/handbook/2/narrowing.html)
- Reference: [TypeScript `tsconfig.json` reference](https://www.typescriptlang.org/tsconfig)
- C/Python frame: TS's type system is stricter than Python's type hints but more expressive than C's. `strict: true` is the equivalent of `-Wall -Werror` — use it from day one.
- Build: set up a TS project from scratch (`tsc --init`, enable `strict: true`). Port one small JS utility from Week 1 to TypeScript.

**AG — Prompt caching (2.5h)**

- Read: [Prompt caching docs](https://docs.claude.com/en/docs/build-with-claude/prompt-caching) — read the whole page, including the "What can be cached" section
- Build: add caching to your agent. The system prompt and tool definitions go in a `cache_control: {type: "ephemeral"}` block. This requires putting them in a specific position — read the docs carefully.

---

### Day 12 — Tue 5 May

**FS — TS functions & object types (2.5h)**

- Read: [TypeScript Handbook — Functions](https://www.typescriptlang.org/docs/handbook/2/functions.html), [Object Types](https://www.typescriptlang.org/docs/handbook/2/objects.html)
- Course: [Matt Pocock — Beginner's TypeScript](https://www.totaltypescript.com/tutorials/beginners-typescript) — free, interactive exercises, excellent for someone who already knows programming
- Build: type your Week 1 fetch script in full — type the API response shape, the function signatures, everything

**AG — Measure caching savings (2.5h)**

- Build: run a 20-turn agent session with caching on, then the same session with caching off. Log `usage.cache_read_input_tokens`, `usage.cache_creation_input_tokens`, and `usage.input_tokens` for every turn. Calculate total cost both ways. Write the numbers down — you'll reference them when explaining caching to someone else.

---

### Day 13 — Wed 6 May

**FS — TS generics & utility types (2.5h)**

- Read: [TypeScript Handbook — Generics](https://www.typescriptlang.org/docs/handbook/2/generics.html), [Utility Types](https://www.typescriptlang.org/docs/handbook/utility-types.html)
- Key utility types to internalise: `Partial<T>`, `Required<T>`, `Pick<T, K>`, `Omit<T, K>`, `Record<K, V>`, `ReturnType<F>`, `Parameters<F>`
- Build: write a generic `Result<T, E>` type (like Rust's `Result`) and use it in a small function

**AG — Re-read + refactor (2.5h)**

- Re-read: [Building effective agents](https://www.anthropic.com/engineering/building-effective-agents) — second pass. The sections on tool design and on parallelisation will hit differently now that you've built an agent.
- Build: refactor your agent with what you've learned. Focus on the system prompt (is it actually focused?), tool schemas (are the descriptions precise?), and error handling (does the agent recover from tool failures?).

---

### Day 14 — Thu 7 May

**FS — Advanced TS patterns (2.5h)**

- Read: [TypeScript Handbook — Discriminated unions](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes-func.html#discriminated-unions), [Type Guards](https://www.typescriptlang.org/docs/handbook/2/narrowing.html#using-type-predicates), [`as const`](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-4.html#const-assertions), [`satisfies`](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-4-9.html#the-satisfies-operator)
- C frame: discriminated unions ≈ tagged unions (`enum` + `union` in C). TS just makes the tagging and narrowing ergonomic.
- Build: model your agent's tool result as a discriminated union (`{status: "ok", data: T} | {status: "error", message: string}`)

**AG — Finish proper agent (2.5h)**

- Build: finish your "proper" coding agent. Checklist:
  - [ ] Clean, focused system prompt (< 500 words, clear task scope)
  - [ ] 5–7 well-named tools with precise descriptions in the schema
  - [ ] All file operations sandboxed to `./workspace/`
  - [ ] Every tool call logged with timestamp and duration
  - [ ] `max_iterations` guard
  - [ ] Graceful error handling when a tool fails

---

### Day 15 — Fri 8 May

**FS — Rewrite todo app in TypeScript (2.5h)**

- Reference: [React + TypeScript cheatsheet](https://react-typescript-cheatsheet.netlify.app) — bookmark, refer constantly
- Reference: [react.dev — TypeScript](https://react.dev/learn/typescript)
- Build: rewrite the todo app in TypeScript. Type: component props, event handlers (`React.ChangeEvent<HTMLInputElement>`), state shapes, and the todo item model. Fix every type error — don't use `any`.

**AG — Stress test the agent (2.5h)**

- Build: run your agent on 3 qualitatively different coding tasks:
  1. Add type annotations to a Python file
  2. Write a test suite for an existing module
  3. Refactor a function with high cyclomatic complexity
- For each: note what it got right, what it got wrong, and what broke. These failure notes are your first eval dataset.

🏁 **Week 3 milestone**: typed todo app; proper coding agent you're proud of

---

## Week 4 — Next.js + Agent SDK
**Mon 11 – Fri 15 May · Milestone: notes app in Next.js + Postgres; Agent SDK + MCP working**

### Day 16 — Mon 11 May

**FS — Next.js App Router foundations (2.5h)**

- Primary: [Next.js learn course](https://nextjs.org/learn) — start from chapter 1. Do chapters 1–3 today (dashboard skeleton, CSS styling, optimising fonts/images).
- Reference: [Next.js App Router docs](https://nextjs.org/docs/app) — file conventions (`page.tsx`, `layout.tsx`, `loading.tsx`, `error.tsx`, `not-found.tsx`)
- Build: spin up a fresh Next.js app (`npx create-next-app@latest`), understand the generated file structure

**AG — Agent SDK quickstart (2.5h)**

- Read: [Agent SDK overview](https://docs.claude.com/en/docs/agent-sdk/overview) and [Agent SDK quickstart](https://docs.claude.com/en/docs/agent-sdk/quickstart)
- Reference: [`claude-agent-sdk-python` GitHub repo](https://github.com/anthropics/claude-agent-sdk-python) — read the README; skim `examples/quick_start.py` and `examples/streaming_mode.py`
- Install: `pip install claude-agent-sdk` (requires Node 18+ for the bundled CLI)
- Build: run the bug-fix quickstart from the docs end-to-end

---

### Day 17 — Tue 12 May

**FS — Server vs Client Components (2.5h)**

> The main new mental model in Next.js. Take your time here.

- Read: [Next.js — Server and Client Components](https://nextjs.org/docs/app/building-your-application/rendering/server-components), [When to use Client Components](https://nextjs.org/docs/app/building-your-application/rendering/client-components#when-to-use-client-components)
- Key insight: Server Components run on the server, have no JS bundle cost, can `await` database calls directly. Client Components run in the browser and handle interactivity. Most components should be Server Components.
- Build: Next.js learn course chapters 4–6 (layouts, pages, navigation)

**AG — Hand-rolled vs SDK (2.5h)**

- Build: take one of your Week 2/3 agent tasks and implement it using the Agent SDK. Run both versions on the same task. Write a short list of what the SDK handles that you wrote by hand: streaming, tool dispatch, error recovery, etc.

---

### Day 18 — Wed 13 May

**FS — Route handlers, Server Actions, data fetching (2.5h)**

- Read: [Next.js — Route Handlers](https://nextjs.org/docs/app/building-your-application/routing/route-handlers), [Server Actions](https://nextjs.org/docs/app/building-your-application/data-fetching/server-actions-and-mutations), [Data fetching patterns](https://nextjs.org/docs/app/building-your-application/data-fetching/patterns)
- Build: Next.js learn course chapters 7–9 (fetching data, static/dynamic rendering, streaming)

**AG — Permissions + read-only code reviewer (2.5h)**

- Read: [Agent SDK permissions guide](https://docs.claude.com/en/docs/agent-sdk/permissions) — critical before giving any agent write access
- Build: configure a read-only code reviewer. Only allow `Read`, `Glob`, and `Grep` permissions. Point it at a small open-source Python repo. Ask it to identify functions missing docstrings and files with no tests. Verify it cannot write anything.

---

### Day 19 — Thu 14 May

**FS — SQL, Postgres, Drizzle (2.5h)**

- Read: [Neon — Getting started](https://neon.tech/docs/get-started-with-neon/signing-up) (free tier, no credit card), [Drizzle ORM — Getting started with Neon](https://orm.drizzle.team/docs/get-started-postgresql#neon)
- Reference: [Drizzle schema declaration](https://orm.drizzle.team/docs/sql-schema-declaration), [Drizzle queries](https://orm.drizzle.team/docs/select)
- C/Python frame: Drizzle is a query builder that stays close to SQL — no magic ORM abstraction. If you know SQL (and you do), the schema declarations will read naturally.
- Build: Next.js learn course chapters 10–11 (partial pre-rendering, setting up the DB). Set up Neon + Drizzle in your Next.js app. Define a `notes` table and run a migration.

**AG — MCP intro + first server (2.5h)**

- Read: [What is MCP — modelcontextprotocol.io](https://modelcontextprotocol.io/docs/getting-started/intro)
- Course: [Anthropic — Introduction to MCP (Skilljar)](https://anthropic.skilljar.com/introduction-to-model-context-protocol) — free, covers the three primitives (tools, resources, prompts). Start it today; finish across today and tomorrow.
- Install: `uv add mcp` (or `pip install mcp`)
- Build: scaffold an MCP server with one tool that does something trivial (e.g. `get_current_time()`)

---

### Day 20 — Fri 15 May

**FS — Build: notes CRUD in Next.js (2.5h)**

- Reference: [Next.js learn course ch. 12–13](https://nextjs.org/learn) (mutating data with Server Actions, handling errors)
- Build: notes CRUD app. Schema: `users` + `notes` (id, user_id, title, content, created_at, updated_at). Server Components for reads, Server Actions for writes, Drizzle + Neon for storage. No auth yet — hardcode a user for now.

**AG — Finish MCP server + wire into agent (2.5h)**

- Finish: [Anthropic — Introduction to MCP (Skilljar)](https://anthropic.skilljar.com/introduction-to-model-context-protocol)
- Supplement: [Hugging Face MCP course](https://huggingface.co/learn/mcp-course/en/unit0/introduction) — free, good conceptual framing
- Reference: [Anthropic courses — MCP sections](https://github.com/anthropics/courses) (check for `mcp/` folder)
- Build: add two real tools to your MCP server: `search_my_notes(query: str)` (queries the Neon DB from Day 19) and `summarize_commit(sha: str)` (runs `git show` via subprocess). Wire the server into your Agent SDK agent. Test both tools end-to-end.
- Tool: install [MCP Inspector](https://github.com/modelcontextprotocol/inspector) — lets you call your MCP tools by hand from a browser UI. Use it to debug before wiring into the agent.

🏁 **Week 4 milestone**: notes app in Next.js + Postgres; Agent SDK agent with custom MCP tools

---

## Week 5 — Production Essentials
**Mon 18 – Fri 22 May · Milestone: auth'd notes app; eval harness with 25 cases**

### Day 21 — Mon 18 May

**FS — Tailwind + shadcn/ui (2.5h)**

- Read: [Tailwind CSS — Core concepts](https://tailwindcss.com/docs/utility-first), [Flexbox](https://tailwindcss.com/docs/display#flex), [Grid](https://tailwindcss.com/docs/display#grid), [Responsive design](https://tailwindcss.com/docs/responsive-design), [Dark mode](https://tailwindcss.com/docs/dark-mode)
- Setup: [shadcn/ui — Installation with Next.js](https://ui.shadcn.com/docs/installation/next)
- Build: nothing to ship today — explore and experiment. Add Tailwind + shadcn to your notes app. Get comfortable with utility classes before trying to build a full layout.

**AG — Eval design (2.5h)**

- Read: [Anthropic eval guidance](https://docs.claude.com/en/docs/test-and-evaluate/develop-tests)
- Read: [Hamel Husain — "Your AI product needs evals"](https://hamel.dev/blog/posts/evals/) — a bit long but worth it
- Design: define your YAML test-case format. Each case needs: `id`, `input` (the task), `expected_behaviour` (what success looks like — be specific), `tags` (e.g. `file_edit`, `test_generation`). Write 5 cases by end of day.

---

### Day 22 — Tue 19 May

**FS — Restyle notes app (2.5h)**

- Reference: [shadcn/ui components](https://ui.shadcn.com/docs/components) — `Button`, `Card`, `Input`, `Textarea`, `Badge`, `Dialog`
- Build: restyle the notes app with Tailwind + shadcn. Proper layout (sidebar + content area), responsive (mobile-first), dark mode that actually works.

**AG — Build eval harness (2.5h)**

- Reference: [Inspect AI](https://inspect.ai-safety-institute.org.uk/) — open-source eval framework from the UK AI Safety Institute. Consider using it, or write your own (100 lines of Python teaches you more than any config file).
- Alternative: [DeepEval](https://github.com/confident-ai/deepeval) — pytest-style, Apache-2.0, good if you like pytest ergonomics
- Build: eval runner that reads your YAML cases, runs each through your agent, scores pass/fail, and prints a report with pass rate, mean duration, and estimated cost per case. Start with 10 cases running end-to-end.

---

### Day 23 — Wed 20 May

**FS — Auth.js (2.5h)**

- Read: [Auth.js — Getting started with Next.js](https://authjs.dev/getting-started?framework=next.js), [Session management](https://authjs.dev/concepts/session-strategies), [OAuth](https://authjs.dev/getting-started/authentication/oauth)
- Reference: [Next.js learn course ch. 15](https://nextjs.org/learn) — auth chapter
- Build: add Auth.js to your notes app. GitHub OAuth is the quickest to set up. Get sign-in/sign-out working before touching anything else.

**AG — Tracing (2.5h)**

- Tracing options (pick one):
  - **JSONL + pretty-printer**: costs $0, teaches you what a trace contains. Start here.
  - [Langfuse](https://langfuse.com) — open-source, self-hostable, free cloud tier. Best upgrade path from JSONL.
  - [Braintrust](https://www.braintrust.dev) — hosted, generous free tier, tight eval + trace integration. Pick if you don't want to self-host.
- Build: instrument your agent. Every run produces a trace file: full message history, tool calls with args + results, token counts per turn, total cost, duration. You should be able to replay and inspect any run from its trace.

---

### Day 24 — Thu 21 May

**FS — Finish auth (2.5h)**

- Build: users can only see their own notes. Protect every Server Action: check that `session.user.id` matches the note's `user_id` before any write. Protect route handlers the same way. Delete the hardcoded user from Day 20.

**AG — Grow evals + fix failures (2.5h)**

- Build: grow your eval suite to 25 cases. Cover at least 4 different task types. Run the full suite against your agent. Look at the failures — what's the pattern? Pick the top 2 failure modes and fix them (system prompt tweak, tool schema change, or error handling). Re-run and measure the improvement.

---

### Day 25 — Fri 22 May

**FS — Next.js caching + optimistic UI (2.5h)**

- Read: [Next.js — Data fetching and caching](https://nextjs.org/docs/app/building-your-application/data-fetching/fetching), [revalidatePath / revalidateTag](https://nextjs.org/docs/app/api-reference/functions/revalidatePath), [`useOptimistic`](https://react.dev/reference/react/useOptimistic)
- Build: add `useOptimistic` to note creation and deletion so the UI responds instantly before the server confirms

**AG — All 5 workflow patterns (2.5h)**

> The original roadmap cut 3 of the 5 Anthropic patterns to save time. Today you build all 5. They take less time than you'd think once you have the agent loop solid. Each is a different answer to the same question: when should you use multiple LLM calls instead of one?

Read the "Workflows" section of [Building effective agents](https://www.anthropic.com/engineering/building-effective-agents) in full before writing any code today.

**Pattern 1 — Prompt chaining** (sequential, each step feeds the next)

- When to use: multi-step tasks where each step's output is the next step's input, and you want a gate between them
- Build: extract → transform → verify on a Python file. (1) extract all function signatures, (2) generate a docstring for each, (3) verify each docstring is accurate against the function body and flag any that aren't. Compare to a single-shot prompt doing all three. Note quality difference and cost difference.
- C analogy: a Unix pipeline — `cat file | step1 | step2 | step3`

**Pattern 2 — Parallelisation** (fan-out, then aggregate)

- When to use: independent subtasks that don't need each other's output; or voting/consensus across N independent model calls
- Two sub-variants:
  - *Sectioning*: split the work, run in parallel, merge results
  - *Voting*: run the same prompt N times, take majority answer (good for high-stakes yes/no decisions)
- Build: given a Python module with 10 functions, run docstring generation for all 10 in parallel using `asyncio.gather`. Compare wall-clock time to sequential. Then: run the same "is this function correct?" prompt 3 times with `temperature=1` and implement a majority vote.
- Reference: [Anthropic cookbooks — parallel tool use examples](https://github.com/anthropics/claude-cookbooks)

**Pattern 3 — Routing** (classify first, then specialise)

- When to use: inputs that fall into distinct categories, each needing a different prompt/tool set. A single general prompt handles all of them worse than a specialised one handles each.
- Build: a code review router. First call classifies the input as one of: `security`, `performance`, `style`, or `correctness`. Then route to a specialised reviewer prompt for that category. Test with 4–5 real code snippets. Compare output quality to a single "review this code" prompt.
- C analogy: a `switch` statement — dispatch on type, handle each case differently

**Pattern 4 — Orchestrator-workers** (one planner, N executors)

- When to use: tasks too complex or unpredictable to pre-define as a fixed pipeline; the orchestrator decides at runtime what to do and in what order
- Build: an orchestrator that receives "refactor this module" and decides which files to read, which functions to change, in which order, and which tools to call. Workers execute those calls. The orchestrator synthesises results and decides when it's done.
- Reference: [Building effective agents — Orchestrator-subagents](https://www.anthropic.com/engineering/building-effective-agents)
- Note: this is the pattern you'll implement properly in Week 6 for your project. Today, build a small version just to understand the shape.

**Pattern 5 — Evaluator-optimizer** (generate, then critique, then improve)

- When to use: open-ended output quality tasks where you can define "better" but not a precise correct answer. Code generation, prose, test suites.
- Build: a two-call loop. First call generates a test suite for a function. Second call (the evaluator) scores it: are edge cases covered, is the setup/teardown correct, are assertions meaningful? If score < threshold, feed the critique back to call 1 and regenerate. Cap at 3 iterations.
- This pattern maps directly to TDD if you squint: write tests → run them → fix code → repeat
- Key insight: the evaluator prompt is often easier to write well than the generator prompt, because judging is easier than creating

**After building all 5**: write a one-paragraph decision guide for yourself — which pattern would you reach for first, and under what conditions? This is more useful than any blog post on the topic.

🏁 **Week 5 milestone**: auth'd, styled notes app; eval harness with 25 cases + traces; all 5 workflow patterns built

---

## Week 6 — Start Your Project
**Mon 25 – Fri 29 May · Milestone: project deployed rough; first agent endpoint end-to-end**

Stop following tutorials. Pick one project that solves a problem you actually have.

**Project ideas that suit a systems background:**
- Self-hosted bookmark manager with tagging, full-text search, and an "auto-summarise URL" agent
- Code snippet manager with syntax highlighting and a "refactor this snippet" agent
- Rate-limited API gateway with auth, logging, and an agent that explains failure patterns

Pick one. Write the project name here: ___________________________

### Day 26 — Mon 25 May

**FS**: Scaffold Next.js app, Drizzle + Neon, define schema (aim for ≥3 tables with relationships), run initial migrations.

**AG**: Plan your agent feature in writing — what tools does it need, what does success look like, what are your first 5 eval cases? Don't write code yet. Write the spec.

---

### Day 27 — Tue 26 May

**FS**: Auth flow (reuse your Auth.js knowledge from Week 5), base layout, bring in shadcn components.

**AG**: Port the orchestrator-workers pattern from Week 5 into your project context.
- Reference: [Building effective agents — Orchestrator-subagents](https://www.anthropic.com/engineering/building-effective-agents)
- You built the pattern in isolation on Day 25 — today you adapt it to your project's actual domain. The orchestrator receives the user's agent request; workers call your project's tools and MCP server. The key difference from the toy version: the workers now operate on real data with real consequences, so the orchestrator's planning prompt needs to be precise about scope and failure conditions.
- Also decide: does your agent feature need a **routing** step before the orchestrator? If users can ask qualitatively different things (e.g. "summarise this" vs "refactor this"), a router that classifies intent and selects the right sub-prompt will improve output quality meaningfully.

---

### Day 28 — Wed 27 May

**FS**: Core CRUD — forms, Server Actions, route handlers for your primary entity.

**AG**: Build your first agent endpoint in Next.js.
- Reference: [Vercel AI SDK — Getting started](https://ai-sdk.dev/docs/introduction) — use the `streamText` helper and `useChat` hook for streaming
- Reference: [Next.js — Streaming with Suspense](https://nextjs.org/docs/app/building-your-application/routing/loading-ui-and-streaming)
- Build: `POST /api/agent/run` that accepts `{prompt, context}`, runs your agent, and streams the response as SSE (Server-Sent Events)

---

### Day 29 — Thu 28 May

**FS**: External API integration (whichever your project needs). Proper error handling, loading states, empty states.

**AG**: Wire the agent endpoint into a client component. The component sends the prompt, reads the SSE stream, and appends tokens to the UI as they arrive. The user should see output appearing word by word.

---

### Day 30 — Fri 29 May

**FS**: Environment variable hygiene — `process.env` validated with [Zod](https://zod.dev) at startup so missing vars fail loudly. Set up [Sentry](https://sentry.io) free tier for error monitoring.

**AG**: Authenticate the agent endpoint — check `session` from Auth.js before running anything. Add per-request cost controls:
- `max_tokens: 4096` (or whatever your task needs — no open-ended runs)
- Early-abort logic: if the agent hasn't called `end_turn` after N iterations, stop and return a partial result
- Reference: [`@upstash/ratelimit`](https://github.com/upstash/ratelimit) — rate limiting per user, works on Vercel Edge

🏁 **Week 6 milestone**: project deployed rough; first agent endpoint runs end-to-end

---

## Week 7 — Build
**Mon 1 – Fri 5 Jun · Milestone: 3+ features; solid agent feature; both tested**

Heads-down week. Less reading, more shipping.

### Day 31 — Mon 1 Jun
**FS**: Feature 2.  
**AG**: Add per-user rate limiting with [`@upstash/ratelimit`](https://github.com/upstash/ratelimit). Log every agent run: user id, prompt, tool calls + args, output length, cost, duration. Store in your DB.

### Day 32 — Tue 2 Jun
**FS**: Feature 3. Start thinking about edge cases — what happens with empty state, with very long inputs, with concurrent requests?  
**AG**: Add 15 more eval cases specific to the integrated agent feature (not the standalone agent from weeks 2–3). Run them. Fix at least 2 failures.

### Day 33 — Wed 3 Jun
**FS**: Polish one rough area — loading states (skeleton UI), empty states (helpful zero-state UI), error states (user-facing error messages).  
**AG**: Refine the agent's system prompt based on eval failures. Re-run all 40 cases. Record the pass rate before and after in your weekly notes.

### Day 34 — Thu 4 Jun
**FS**: Performance pass — run [Lighthouse](https://developer.chrome.com/docs/lighthouse/overview/) on your deployed URL; fix the top 3 flags. Use [`next/image`](https://nextjs.org/docs/app/api-reference/components/image) for any images.  
**AG**: Trace inspection — pick 3 failed agent runs from your trace files. For each: what was the root cause? Fix what's fixable. Document what isn't.

### Day 35 — Fri 5 Jun
**FS**: DB performance — run `EXPLAIN ANALYZE` on 2–3 of your most frequent queries. Add indexes where needed.  
**AG**: Buffer day — catch up on slippage first. If caught up, apply one of the remaining patterns from Day 25 to your project where it fits naturally:
- **Parallelisation**: does your agent make multiple independent tool calls in sequence that could run concurrently? Fan them out with `asyncio.gather`. Measure the latency improvement — parallelising 4 independent file reads typically cuts that segment by 60–70%.
- **Evaluator-optimizer**: does your agent produce open-ended output (summaries, refactors, explanations)? Add a second LLM call that scores the output and triggers a retry if below threshold. One iteration of this loop often eliminates your most common eval failure mode entirely.
- If genuinely caught up on both: read [aider's `coders/` directory](https://github.com/Aider-AI/aider/tree/main/aider/coders) — the best real-world example of context management and multi-step editing strategy in open source.

🏁 **Week 7 milestone**: 3+ features + solid agent feature; both tested and evaled

---

## Week 8 — Ship It
**Mon 8 – Fri 12 Jun · Milestone: deployed, tested, documented project with AI feature**

### Day 36 — Mon 8 Jun
**FS**: [Vitest](https://vitest.dev/guide/) — 10–15 unit tests covering business logic (validation, transformation, auth checks). Don't test UI; don't test the database. Test pure functions.  
**AG**: Make your eval report legible to someone who hasn't seen the codebase. It should show: total cases, pass rate, cost per run, and the top 3 failure categories.

### Day 37 — Tue 9 Jun
**FS**: [Playwright](https://playwright.dev/docs/intro) — 2 end-to-end tests on critical flows: (1) sign up → create item, (2) use agent feature → see result.  
**AG**: Add a "recent runs" page for logged-in users — shows the last 10 agent runs with prompt, status, cost, and a link to the full trace. This is the most impressive thing to show in a demo.

### Day 38 — Wed 10 Jun
**FS**: [GitHub Actions](https://docs.github.com/en/actions/writing-workflows/quickstart) — CI workflow that runs `vitest` and `playwright` on every push. Fix anything that breaks in CI.  
**AG**: Write the agent design doc for the README (2–3 paragraphs): what the feature does, how it works (tools, patterns used), and what can go wrong / current limitations.

### Day 39 — Thu 11 Jun
**FS**: Polished README — screenshots (use [Carbon](https://carbon.now.sh) for code, a browser screenshot tool for UI), live demo link, architecture diagram (even a rough ASCII one is fine). Custom domain optional but worth the $12/year.  
**AG**: Add eval results to the README — a small table: pass rate, mean cost per run, number of test cases. Record a 2-minute [Loom](https://www.loom.com) video of the agent feature working end-to-end.

### Day 40 — Fri 12 Jun
**FS**: Ship announcement — post on LinkedIn, Twitter/X, a Discord, or just tell a friend. Close off the project.  
**AG**: Write up ONE hard-won lesson as a blog post or README section. Good options: how you designed your agent's tool schemas, what your evals caught that you'd have missed, how you handled context limits in practice, what prompt caching actually saved you.

🏁 **Week 8 milestone**: deployed, tested, documented project with integrated agent feature — portfolio ready

---

## Reference codebases (read in Week 7–8 buffer time)

In rough order of readability:

| Repo | Language | What to read | Why |
|------|----------|--------------|-----|
| [claude-code](https://github.com/anthropics/claude-code) | TS | Each file individually | The reference coding agent; authoritative on tool design |
| [aider](https://github.com/Aider-AI/aider) | Python | `aider/coders/` | Best examples of context management and repo-wide editing |
| [Open Interpreter](https://github.com/OpenInterpreter/open-interpreter) | Python | `interpreter/core/` | Simpler than aider; good middle-complexity codebase |
| [Cline](https://github.com/cline/cline) | TS | `src/core/` | VS Code coding agent; shows tool use + UI integration |

---

## Ongoing signal (15 min/week cap — enforced)

| Source | What you get |
|--------|--------------|
| [Anthropic engineering blog](https://www.anthropic.com/engineering) | Rare but essential posts from the people building the models |
| [Simon Willison's blog](https://simonwillison.net) | Consistently lucid on what's actually working in practice |
| [Latent Space podcast](https://www.latent.space) | High signal, practitioner-focused |

Do not subscribe to more than these three. The marginal return on newsletter #4 is negative.

---

## Infrastructure checklist

- [ ] Anthropic API key with hard spending cap set in [console.anthropic.com](https://console.anthropic.com)
- [ ] `uv` installed (Python package manager — faster than pip, standard in Anthropic ecosystem)
- [ ] `nvm` + Node 20 installed (needed for Agent SDK)
- [ ] Docker or a VM ready for sandboxing shell-executing agents — don't skip this
- [ ] A throwaway test repo (200–500 lines of messy Python) for running evals against
- [ ] Daily commit habit — even a one-line commit counts; the streak is what matters

---

## Cost expectations

At Sonnet 4.6 pricing with prompt caching on, expect $3–$15 per week of active agent building. If you hit $50 in a week, something is wrong — probably a runaway loop. Set the spending cap before you start and you won't have to think about it again.

---

## What to deliberately skip

Every week you'll see content promising to teach you "how agents *really* work." Default to skipping it unless it appears in this document or is linked from something that is. Specifically:

- **LangChain** — not now, probably not ever for this use case
- **Vector databases** — coding agents don't need them; if you're reaching for one, you're solving the wrong problem
- **LangSmith** — only useful if you're using LangChain
- **Vendor "LLM eval platform" comparisons** — every one concludes the author's preferred platform wins
- **Any tutorial titled "the REAL way to build agents"** — it's the same loop you built in Week 2

---

*Generated 2026-04-16. Links are entry points, not fixed truths — SDK versions and pricing change. When in doubt, go to the official docs directly.*
