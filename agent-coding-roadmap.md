# Coding-Agent Roadmap (Companion Track)

**Goal**: Go from zero LLM/agent experience to shipping a real coding agent in ~6 weeks.
**Time commitment**: 2 hours/day, layered on top of the full-stack TypeScript roadmap.
**Primary tools**: Anthropic Python SDK → Claude Agent SDK → TypeScript Agent SDK.

---

## How this track fits with the main roadmap

- **Total daily load**: 6 hours (4h full-stack + 2h agents).
- **Language strategy**: Python first (weeks 1–4), TypeScript second (weeks 5–6). Uses Python while your main track teaches you JS/TS; switches to TS exactly when you're fluent enough to integrate agents into your Next.js project.
- **Convergence point**: Week 5–6 of the main roadmap, your personal project can *be* (or include) an agent — you build one project, two tracks' worth of learning.
- **Deliberate redundancy**: Concepts that appear in both tracks (async, HTTP, TypeScript types) get reinforced. No time wasted on overlap — we lean into it.

### Suggested daily split (2h)

- **1h**: read/watch + take notes (Anthropic docs, prompt-engineering guide, one blog post)
- **1h**: hands-on code (exercises, then your own agent project)

Same principle as the main roadmap: push harder on building than watching.

---

## Stack

- **Language**: Python 3.11+ (weeks 1–4), then TypeScript (weeks 5–6)
- **Core API**: Anthropic Messages API (`anthropic` SDK)
- **Agent framework**: Claude Agent SDK (`claude-agent-sdk` — Python and TS)
- **Model**: Claude Sonnet 4.6 for most work, Opus 4.6 for hard tasks
- **Tool protocol**: MCP (Model Context Protocol) for custom tools
- **Evaluation**: Anthropic's `inspect-ai` or homegrown eval harness
- **Tracing**: Console logging first, then LangSmith or Braintrust (free tiers)

---

## Week 1: LLM + Tool-Use Fundamentals

You need a clean mental model of what an LLM *is* before building agents on top. No frameworks yet — build the agent loop by hand.

### Days 1–2: Get an API key and make it talk

Sign up at console.anthropic.com, get an API key, add $5–10 credit (Sonnet 4.6 is cheap for learning).

- Install: `pip install anthropic python-dotenv`
- Read: [Anthropic API Quickstart](https://docs.claude.com/en/api/getting-started) and [Messages API reference](https://docs.claude.com/en/api/messages)
- Build: a CLI that takes a prompt, returns a response, prints token usage and cost

Key ideas to internalize:
- System prompt vs user message vs assistant message
- Temperature, `max_tokens`, stop sequences
- Streaming vs non-streaming
- Stateless API: *you* keep the conversation history, not the server

**Day 2 exercise**: Multi-turn chat CLI. Maintain a `messages` list in Python. Handle Ctrl-C gracefully. Print input/output token counts per turn.

### Days 3–4: Prompt engineering that actually matters

Read Anthropic's [prompt engineering overview](https://docs.claude.com/en/docs/build-with-claude/prompt-engineering/overview) and these sub-pages: "Be clear and direct", "Use examples", "Let Claude think" (chain-of-thought), "Use XML tags", "System prompts".

Stop reading "prompt hacks" on Twitter. Anthropic's docs are the real deal.

**Exercise**: Take one fuzzy task ("summarize this codebase") and write five progressively-better prompts for it. Save each version + output. Notice what changes.

### Days 5–7: Tool use from scratch — the agent loop

This is the single most important week. Build the agent loop *by hand* before ever touching an SDK that hides it.

Read: [Tool use overview](https://docs.claude.com/en/docs/agents-and-tools/tool-use/overview) and ["How tool use works"](https://docs.claude.com/en/docs/agents-and-tools/tool-use/how-tool-use-works).

Core mental model: the loop is just
```
while True:
    response = claude.messages.create(messages=..., tools=...)
    if response.stop_reason == "end_turn":
        break
    tool_calls = extract_tool_uses(response)
    tool_results = [execute(call) for call in tool_calls]
    messages.append(assistant_response)
    messages.append(tool_results)
```

That's it. Every agent framework is decoration on this loop.

**Day 7 exercise — "Tiny coding agent v0"**: Python script that takes a task like "add type hints to utils.py" and solves it in a loop using three hand-written tools: `read_file`, `write_file`, `list_dir`. No SDK. Just `anthropic.messages.create` + a while loop. Keep iterating until Claude says it's done. This is your foundation — understand every line.

**Week 1 milestone**: You can explain the agent loop on a whiteboard and have built one in ~150 lines of Python.

---

## Week 2: Building Real Tools + Context Management

### Days 8–10: More tools, more care

Expand your toy agent with:
- `run_bash` (dangerous — use `subprocess` with a timeout; start with no shell, whitelisted commands)
- `grep` / `find` (or shell out to `rg`)
- `apply_patch` or a proper `edit_file` with line ranges (not just "overwrite whole file")

Read: [Anthropic's "Building effective agents"](https://www.anthropic.com/engineering/building-effective-agents) — short, dense, essential. Read it twice.

Key takeaways:
- Start with workflows (fixed code paths), only reach for full agents when needed
- Tools should be self-explanatory with good descriptions and error messages
- Simpler is almost always better

### Days 11–12: Context window is a resource

Understand:
- Context windows (200k for Sonnet 4.6, but speed and quality degrade past ~50k)
- Prompt caching ([docs](https://docs.claude.com/en/docs/build-with-claude/prompt-caching)) — 90% cost reduction on cached prefixes
- How to summarize / truncate old turns
- When to start a fresh session vs continue

**Exercise**: Add prompt caching to your agent's system prompt and tool definitions. Measure cost before/after on a 20-turn conversation.

### Days 13–14: Your first "proper" coding agent

Rebuild your toy agent into something real:
- A focused system prompt ("You are a careful Python refactoring assistant...")
- 5–7 well-designed tools
- A working directory sandbox (agent can't escape `./workspace`)
- Structured logging of every tool call
- A simple CLI: `python agent.py "refactor utils.py to use dataclasses"`

Test it on a messy Python file of yours. Watch where it fails.

**Week 2 milestone**: You have a working hand-rolled coding agent. You know exactly what every part does.

---

## Week 3: Claude Agent SDK + MCP

Now you've earned the right to use a framework, because you know what it's replacing.

### Days 15–16: Agent SDK quickstart

Read: [Agent SDK overview](https://docs.claude.com/en/docs/agent-sdk/overview) and [quickstart](https://docs.claude.com/en/docs/agent-sdk/quickstart).

Install `pip install claude-agent-sdk` (bundles the Claude Code CLI — needs Node 18+). Work through the quickstart: an agent that finds and fixes bugs in `utils.py`.

Compare with your hand-rolled version. Note what the SDK gives you for free:
- Built-in `Read`, `Edit`, `Write`, `Glob`, `Grep`, `Bash` tools
- Permission modes and allowed-tool lists
- Session resumption
- Subagents

### Days 17–18: Permissions, safety, and options

Coding agents execute code. Danger is real.

- `allowed_tools` vs `disallowed_tools`
- `permission_mode`: `default`, `acceptEdits`, `bypassPermissions` (never in production)
- Working-directory isolation
- Why you should usually run agents in a container or VM for anything untrusted

**Exercise**: Configure an agent with only `Read`, `Glob`, `Grep` — a read-only code reviewer. Point it at a small open-source repo and ask for a review.

### Days 19–21: MCP — your own tools, properly

MCP (Model Context Protocol) is how you expose custom tools to Claude in a standard way. Read the [MCP spec intro](https://modelcontextprotocol.io) — don't read the whole spec yet.

Build a simple MCP server in Python that exposes:
- `search_my_notes(query)` — greps a local notes directory
- `summarize_commit(sha)` — runs `git show` and returns structured output

Wire it into your Agent SDK agent. Now you have a coding agent with custom superpowers.

**Week 3 milestone**: You can ship a custom agent built on the SDK with your own MCP tools.

---

## Week 4: Evals, Tracing, and Agent Patterns

This is the week that separates hobby projects from real software.

### Days 22–23: Why you *must* eval agents

An agent that works for your 3 test cases may fail for 30% of real ones. Without evals, you won't notice until users complain.

Read: [Anthropic's eval guidance](https://docs.claude.com/en/docs/test-and-evaluate/develop-tests).

Build a simple eval harness:
- A folder of `.yaml` test cases: `{prompt, setup_files, assertion}`
- A runner that spins up your agent on each and checks the assertion
- A report: pass/fail, duration, tokens, cost per case

Start with 10 cases. Aim for 50 by end of week.

### Days 24–25: Tracing and observability

When an agent fails, you need to see every tool call and every message. Options:
- Cheap: log everything to JSONL, one file per run
- Mid: print a pretty trace tree to stderr
- Real: [Langfuse](https://langfuse.com) or [Braintrust](https://braintrust.dev) free tier

Pick one. Instrument your agent. You should be able to replay any failed run.

### Days 26–28: Agent patterns beyond "one loop"

Read ["Building effective agents"](https://www.anthropic.com/engineering/building-effective-agents) again — now it'll make more sense. Implement each pattern at least once:

- **Prompt chaining**: step 1 extracts, step 2 transforms, step 3 verifies
- **Routing**: classify input, dispatch to specialized sub-prompts
- **Parallelization**: fan out to multiple Claudes, aggregate
- **Orchestrator-workers**: a planner LLM that delegates to worker agents
- **Evaluator-optimizer**: one LLM critiques another's output in a loop

**Exercise**: Pick one real task (e.g., "generate a README for a repo") and implement it three ways: single-shot prompt, tool-using agent, orchestrator-worker. Compare quality, latency, cost.

**Week 4 milestone**: Production-shaped agent with evals, traces, and deliberate architecture.

---

## Week 5: TypeScript Agent SDK + Next.js Integration

Your main roadmap has you deep in Next.js by now. Time to merge the tracks.

### Days 29–30: Port to TypeScript

Install `@anthropic-ai/sdk` and `@anthropic-ai/claude-agent-sdk`. Port your best Python agent to TS. Most of the API is mirror-symmetric.

Read: [Agent SDK TS docs](https://docs.claude.com/en/docs/agent-sdk/typescript).

This doubles as TypeScript practice — real code, not tutorial toys.

### Days 31–32: Agents as a Next.js feature

Approaches:
- **Route handler**: POST `/api/agent/run` kicks off an agent, streams results via Server-Sent Events or a ReadableStream
- **Server Action**: for one-shot tasks triggered from a form
- **Background job**: agents can run long — use a queue (Inngest, Trigger.dev free tier) and poll for status

Pick SSE streaming first — it's the most satisfying to watch.

**Exercise**: Add an agent endpoint to the notes app from your main roadmap. Feature: "Ask an agent to clean up my notes" — agent reads notes, suggests edits, shows a diff, user approves.

### Days 33–35: Auth, rate limiting, cost controls

Production essentials that apply doubly to agents because they can burn tokens fast:
- Authenticate agent endpoints (your main roadmap covered Auth.js)
- Per-user rate limits (Upstash Ratelimit)
- Per-request token/cost caps (`max_tokens`, early-abort on runaway loops)
- Log every agent run with user, prompt, tool calls, total cost — you'll want this

**Week 5 milestone**: A real agent feature deployed on top of your Next.js app, not a standalone script.

---

## Week 6: Ship It + Deepen

### Days 36–38: Merge with your main project

Your main roadmap's week 5 has you building a personal project. Week 6 of that roadmap polishes it. Pick one agent feature to add that makes the project actually better:

- Bookmark manager → "Summarize this link" agent (reads URL, extracts, tags)
- Snippet manager → "Explain this snippet / suggest refactors" agent
- Knowledge base → "Find and link related notes" agent with MCP tools that search your DB
- Analytics dashboard → "Weekly summary" agent that runs on a cron

Don't bolt on a chatbot. Find the spot where an agent is objectively better than a traditional feature.

### Days 39–40: Read real agent code

- [Claude Code itself](https://github.com/anthropics/claude-code) — reference implementation
- [Cline](https://github.com/cline/cline) — VS Code coding agent, readable TS
- [aider](https://github.com/Aider-AI/aider) — Python, very mature, great for studying context management
- Anthropic's [courses repo](https://github.com/anthropics/courses) and [cookbooks](https://github.com/anthropics/anthropic-cookbook)

Steal patterns shamelessly.

### Days 41–42: Polish, write up, share

- Write a short blog post or README section explaining one thing you learned the hard way (context management, an eval insight, a tool-design mistake)
- Add your agent-eval results to the project README
- Record a 2-minute demo video

**Week 6 milestone**: Portfolio-quality agent feature shipped in a real app, with evals, traces, and a write-up.

---

## Reference Resources

Bookmark these, in order of how often you'll hit them:

- [Anthropic docs — API + Agent SDK](https://docs.claude.com) — primary reference
- [Building effective agents](https://www.anthropic.com/engineering/building-effective-agents) — re-read monthly
- [Anthropic Cookbook](https://github.com/anthropics/anthropic-cookbook) — copy-pasteable patterns
- [Anthropic Courses](https://github.com/anthropics/courses) — API, prompt engineering, tool use, MCP
- [Prompt engineering overview](https://docs.claude.com/en/docs/build-with-claude/prompt-engineering/overview)
- [MCP docs](https://modelcontextprotocol.io)
- [Every AI newsletter](https://every.to) and [Latent Space podcast](https://www.latent.space) — signal, not noise

---

## Things to deliberately ignore (for now)

You will see hype about these. They're fine, but not on the critical path:

- **LangChain / LlamaIndex**: huge surface area, distracts from fundamentals. Revisit only if you need their specific integrations.
- **Vector DBs and RAG**: important for knowledge agents, not for coding agents. Skip until you have a concrete need.
- **Fine-tuning**: almost never the right answer for an agent. Prompt + tools + evals get you 95%.
- **Every new "agent framework" that launches during these 6 weeks**: if you can't articulate what it does that Agent SDK can't, skip it.
- **AGI discourse**: log off, build.

---

## Expectations

**After 6 weeks at 2h/day, you will be:**

- **Confident**: writing prompts, building tool-using agents, using the Agent SDK, designing evals
- **Competent**: integrating agents into real apps, handling cost/safety/permissions
- **Not yet expert**: at complex multi-agent orchestration, long-horizon agents (days/weeks of autonomy), or cutting-edge research patterns

Expertise here is newer than in web dev — 6 months of real work puts you ahead of most people claiming to "build AI agents" in 2026.

---

## Milestone Checklist

- [ ] Day 7: Hand-rolled agent loop in ~150 lines of Python, no SDK
- [ ] Day 14: Real coding agent with 5+ tools, sandboxed, logged
- [ ] Day 21: Agent SDK + custom MCP server, both working
- [ ] Day 28: Eval harness with 50 cases; tracing in place
- [ ] Day 35: Agent integrated into your Next.js app with streaming + auth
- [ ] Day 42: Shipped agent feature in portfolio project; write-up published

---

*Roadmap generated 2026-04-16. The agent ecosystem moves fast — check for newer SDK versions, new Anthropic patterns pages, and current model names when you start each week.*
