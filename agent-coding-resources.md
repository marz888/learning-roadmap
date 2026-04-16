# Agent Coding Roadmap — Learning Resources & Tools

Companion to `agent-coding-roadmap.md`. Curated, opinionated, and organized by phase — not a dump of every link on the internet.

**Rule of thumb**: official Anthropic docs > Anthropic's own courses > well-known practitioners > everything else. Most "agent tutorial" content from random blogs in 2026 is slop. Stick to the list below and you'll avoid 95% of it.

---

## Foundational reading (do these first, before week 1)

Three short, dense pieces that shape how you'll think about everything else:

- **[Building effective agents](https://www.anthropic.com/engineering/building-effective-agents)** (Anthropic) — the single most important thing to read. Distinguishes workflows from agents, covers the five core patterns. Read it at the start of week 1, re-read it at the start of week 4, re-read it monthly after.
- **[How we built our multi-agent research system](https://www.anthropic.com/engineering/built-multi-agent-research-system)** (Anthropic) — an actual production agent story. Concrete lessons on context management, orchestration, and what actually breaks.
- **[Prompt engineering overview](https://docs.claude.com/en/docs/build-with-claude/prompt-engineering/overview)** — the index page for Anthropic's prompt guide. Skim it, bookmark the sub-pages, come back as needed.

Total reading: maybe 90 minutes. Highest leverage 90 minutes on this whole roadmap.

---

## Week 1: LLM + Tool-Use Fundamentals

### Primary (do these)

- **[Anthropic API Quickstart](https://docs.claude.com/en/api/getting-started)** — set up an account, make your first call.
- **[Messages API reference](https://docs.claude.com/en/api/messages)** — you'll hit this page constantly; know where things live.
- **[Anthropic courses repo — API fundamentals](https://github.com/anthropics/courses)** — free Jupyter notebooks. Do the `anthropic_api_fundamentals` and `prompt_engineering_interactive_tutorial` courses. Run them locally against your own key.
- **[Tool use overview](https://docs.claude.com/en/docs/agents-and-tools/tool-use/overview)** and **[How tool use works](https://docs.claude.com/en/docs/agents-and-tools/tool-use/how-tool-use-works)** — the core mental model. Read carefully.
- **[Anthropic courses — Tool use](https://github.com/anthropics/courses/tree/master/tool_use)** — hands-on notebooks covering the loop end to end.

### Tools you'll install

- `anthropic` (Python SDK) — `pip install anthropic`
- `python-dotenv` — for `.env` keys
- `httpx` — if you want to see what the SDK does under the hood; occasionally useful to drop down to raw HTTP

### Skip (for now)

- Anthropic's prompt engineering tutorial has a Google Sheets version. Skip it unless you live in Sheets — the Jupyter version is better for devs.
- Courses that use Claude 3 Haiku as their default — the examples still work, but mentally substitute Sonnet 4.6. Don't rewrite the notebooks, just use a newer model when you run them.

---

## Week 2: Real Tools + Context Management

### Primary

- **[Anthropic claude-cookbooks repo](https://github.com/anthropics/claude-cookbooks)** (previously `anthropic-cookbook`) — copy-pasteable patterns. Especially the tool-use and agents sections. Don't read it linearly; use it as a recipe book when you hit a problem.
- **[Prompt caching docs](https://docs.claude.com/en/docs/build-with-claude/prompt-caching)** — read the whole page, then measure it on your own agent. The 90% cost savings are real but you have to structure the prompt correctly.
- **[Text editor tool docs](https://docs.claude.com/en/docs/agents-and-tools/tool-use/text-editor-tool)** and **[bash tool docs](https://docs.claude.com/en/docs/agents-and-tools/tool-use/bash-tool)** — Anthropic-schema tools that define the "standard shape" of file editing and shell execution. Even if you write your own, copy the schemas.
- **"Building effective agents"** — re-read now that you've built one. Different paragraphs will jump out.

### Tools

- `rich` or `textual` (Python) — for pretty CLI output and trace trees. Massively improves your debugging experience, takes 20 minutes to learn.
- `subprocess` + `shlex` — for `run_bash`. Read the [security considerations in the Python docs](https://docs.python.org/3/library/subprocess.html#security-considerations) before you give your agent shell access.

### Skip

- The urge to use LangChain "because everyone does." Not now. Maybe not ever.
- Vector DBs. Coding agents don't need them. If you find yourself reaching for one, you're solving the wrong problem.

---

## Week 3: Claude Agent SDK + MCP

### Primary — Agent SDK

- **[Agent SDK overview](https://docs.claude.com/en/docs/agent-sdk/overview)** and **[quickstart](https://docs.claude.com/en/docs/agent-sdk/quickstart)** — do the quickstart.
- **[`claude-agent-sdk-python` GitHub repo](https://github.com/anthropics/claude-agent-sdk-python)** — read the README and skim `src/`. The `examples/` folder is gold — especially `streaming_mode.py` and `quick_start.py`.
- **[Agent SDK permissions guide](https://docs.claude.com/en/docs/agent-sdk/permissions)** — critical for any agent that can write files or run shell commands. Read before you build anything beyond toy agents.

### Primary — MCP

- **[modelcontextprotocol.io "What is MCP"](https://modelcontextprotocol.io/docs/getting-started/intro)** — the shortest path to understanding what MCP is and isn't.
- **[Anthropic's "Introduction to MCP" course on Skilljar](https://anthropic.skilljar.com/introduction-to-model-context-protocol)** — free, covers the three MCP primitives (tools, resources, prompts) and builds servers + clients in Python. The single best structured MCP learning resource right now.
- **[Anthropic courses repo — MCP sections](https://github.com/anthropics/courses)** — check for `mcp/` or similarly-named folders; they get updated regularly.
- **[Hugging Face MCP course](https://huggingface.co/learn/mcp-course/en/unit0/introduction)** — free, built in partnership with Anthropic, more conceptual framing. Good supplement.

### Tools

- `claude-agent-sdk` — `pip install claude-agent-sdk`. Bundles the Claude Code CLI (needs Node 18+).
- `mcp` (Python SDK) — for building your own MCP servers. Uses `uv` as package manager per the official examples; `uv` is worth adopting generally.
- **MCP Inspector** — browser-based tool for testing MCP servers. Runs locally, reads your server's schema, lets you call tools by hand. Invaluable for debugging.
- **Claude Desktop** — install it and wire your MCP server into it. Seeing your own tools show up in Claude Desktop is a useful reality check.

### Skip

- The full MCP spec document. Bounce off it early and come back only if you hit an edge case the guides don't cover.
- Writing your own MCP transport. The stdio and Streamable HTTP transports that ship with the SDK cover every case you'll care about for months.

---

## Week 4: Evals, Tracing, Agent Patterns

This week is where most tutorials fall off a cliff. The resources below are what actually work in practice.

### Primary reading

- **[Anthropic eval guidance](https://docs.claude.com/en/docs/test-and-evaluate/develop-tests)** — short, practical.
- **["Building effective agents"](https://www.anthropic.com/engineering/building-effective-agents)** one more time — the patterns section is what you're implementing this week.
- **[How we built our multi-agent research system](https://www.anthropic.com/engineering/built-multi-agent-research-system)** — the eval sections are the most useful part once you're actually building evals.
- **[Hamel Husain: "Your AI product needs evals"](https://hamel.dev/blog/posts/evals/)** — blog post from a well-known practitioner. Opinionated, practical, a bit long but worth it.

### Tools — picking a stack

You do *not* need a paid SaaS platform to start. For the roadmap, pick **one** from each of the two categories below:

**Eval framework** (runs tests, scores outputs):

- **[Inspect AI](https://inspect.ai-safety-institute.org.uk/)** — open-source, from the UK AI Safety Institute, solid for agent evals. No SaaS tier; run it locally. This is my default recommendation.
- **DeepEval** — open-source, pytest-style, strong metric coverage, Apache-2.0. Good choice if you like pytest ergonomics.
- **Homegrown** (YAML + Python script) — totally fine for week 4. You learn more by writing 100 lines of eval code yourself than by configuring any platform. Graduate to a framework only when homegrown creaks.

**Tracing / observability** (sees what your agent did):

- **JSONL files + a pretty-printer** — cost $0, teaches you what a trace actually contains. Start here.
- **[Langfuse](https://langfuse.com)** — open-source, self-hostable, free cloud tier. Best "real" option when JSONL stops scaling.
- **[Braintrust](https://www.braintrust.dev)** — hosted only, has a generous free tier, tight eval + trace integration. Pick this if you'd rather not self-host.

**Don't pick more than one of each.** Resist the urge to try every tool in the LLMOps space — it's a trap that will eat week 4 whole.

### Skip

- LangSmith unless you're also using LangChain. The two are deeply coupled, and since you're not using LangChain, LangSmith gives you less than Langfuse or Braintrust for similar effort.
- "LLM evaluation platform" comparison articles written by vendors. Every one of them concludes that they are the best platform. Read two and stop.

---

## Week 5: TypeScript Agent SDK + Next.js Integration

### Primary

- **[Agent SDK TypeScript docs](https://docs.claude.com/en/docs/agent-sdk/typescript)** — mirror of the Python docs.
- **[`@anthropic-ai/claude-agent-sdk` on npm](https://www.npmjs.com/package/@anthropic-ai/claude-agent-sdk)** — check the README and examples folder in the linked repo.
- **[Vercel AI SDK docs](https://ai-sdk.dev/docs/introduction)** — *not* a replacement for the Agent SDK, but it's the standard way to stream agent output to a Next.js frontend. Specifically: the `useChat` hook and streaming primitives. Use the Agent SDK to *run* the agent, use the Vercel AI SDK to *stream* its output to the browser.
- **[Next.js streaming docs](https://nextjs.org/docs/app/building-your-application/routing/loading-ui-and-streaming)** — for Suspense and streamed responses from Server Components / Route Handlers.

### Tools

- `@anthropic-ai/sdk` — the raw Anthropic TS SDK.
- `@anthropic-ai/claude-agent-sdk` — the agent framework, TS version.
- `zod` — you're already using it from the main roadmap; double down for typing tool inputs/outputs.
- `@upstash/ratelimit` — cheap, simple, works on Vercel's Edge. Mandatory for any agent endpoint that faces users.

### Skip

- Any Next.js tutorial that tries to teach you both Next.js and agents at the same time. You already know Next.js by this point; just glue in what you built in weeks 1–4.

---

## Week 6: Shipping + Deepening

### Read real code (this is the week for it)

In rough order of readability:

- **[Anthropic's `claude-code`](https://github.com/anthropics/claude-code)** — the reference coding agent. Big, but each file is digestible.
- **[aider](https://github.com/Aider-AI/aider)** — Python, mature, exceptional for studying context management and repo-wide editing strategies. Read `coders/`.
- **[Cline](https://github.com/cline/cline)** — VS Code coding agent in TS. Good for seeing how tool use + UI integration looks.
- **[Open Interpreter](https://github.com/OpenInterpreter/open-interpreter)** — Python, simpler than aider, good "middle-complexity" codebase.

### Community / signal (light touch)

Most of what you need is in docs. For keeping up with the ecosystem:

- **[Latent Space podcast](https://www.latent.space)** — high signal, practitioner-focused.
- **Anthropic's engineering blog** — [anthropic.com/engineering](https://www.anthropic.com/engineering). New posts are rare but essential.
- **[Simon Willison's blog](https://simonwillison.net)** — consistently lucid on what's actually working.

Set a 15-minutes-a-week cap on newsletters/podcasts. You learn more by shipping.

---

## Infrastructure you'll want, regardless of phase

- **Anthropic API key** — $5–10 credit is plenty for all 6 weeks at Sonnet 4.6 prices.
- **`uv`** (Python package manager from Astral) — faster than pip, becoming the de facto standard in the MCP and Anthropic ecosystem. Worth adopting.
- **Git + GitHub** — obvious, but *commit every single day* this roadmap. You'll want the history later.
- **Docker or a VM** — for sandboxing any agent that runs shell commands. Don't skip this. Agents execute code; hosts get executed on.
- **A throwaway test repo** — 200–500 lines of messy Python you don't mind your agents destroying. Your evals run against this. I use a fork of an old side-project.

---

## Cost expectations

At Sonnet 4.6 pricing, with prompt caching on, a full week of building and testing agents usually lands in the $3–$15 range if you're reasonable. If you hit $50 in a week, something is wrong — probably a runaway loop. The exercises around `max_tokens` caps and early-abort logic in week 5 are there precisely to prevent this. Set a hard budget cap in the [Anthropic console](https://console.anthropic.com) from day one.

---

## What to deliberately ignore

Every week, you will see new content with breathless titles promising to teach you "how agents *really* work." 99% of it is one of three things:

1. A thin wrapper around the basic agent loop you built in week 1.
2. A framework reinventing what the Agent SDK already does, but with more abstractions.
3. Speculation about AGI dressed up as practical advice.

If a resource isn't on the list above and isn't linked from something that is, default to skipping it. You can always revisit. Shipping beats reading.

---

*Resources current as of 2026-04-16. SDK versions, pricing, and platform features change often — treat links as entry points, not fixed truths.*
