# Awesome Jev [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

<p align="center">
  <a href="https://ollaya.dev"><img src="assets/ollaya.png" alt="Ollaya: run decision models locally. Typed questions in, calibrated answers out, in milliseconds." width="100%"></a>
</p>

<p align="center">
  <b>New:</b> <a href="https://ollaya.dev">Ollaya</a> runs open decision models locally behind a Jev-compatible API.<br>
  <a href="https://ollaya.dev">Website</a> · <a href="https://github.com/ollaya-dev/ollaya">GitHub</a> · <a href="https://ollaya.dev/search">Models</a> · <a href="https://ollaya.dev/docs">Docs</a>
</p>

> A curated, source-backed list of projects built with Jev, TypeSafe AI's System One model for fast, typed, probabilistic decisions.

Jev takes program state plus typed questions and returns constrained answers with probabilities. It is designed for software decisions such as classification, routing, scoring, ranking, verification, and guardrails, rather than free-form text generation.

This list favors public source code, concrete Jev usage, clear limitations, and reproducible evidence. The latest review added **20 source-reviewed integrations, projects, and studies**, bringing the community catalog to **155**, alongside official resources, provider integrations, and related lists. See the [September 20 research notes](research/2026-09-20.md) for pinned source evidence and review boundaries. Review completed September 20, 2026 (Europe/Istanbul); upstream event dates below are UTC.

## Contents

- [Start here](#start-here)
- [Recent developments](#recent-developments)
- [Official resources](#official-resources)
- [Provider integrations](#provider-integrations)
- [Framework integrations](#framework-integrations)
- [SDKs and developer tools](#sdks-and-developer-tools)
- [Agents, coding, and guardrails](#agents-coding-and-guardrails)
- [Context and compaction](#context-and-compaction)
- [Browser and computer use](#browser-and-computer-use)
- [Routing, data, and workflows](#routing-data-and-workflows)
- [Games, robotics, and interactive demos](#games-robotics-and-interactive-demos)
- [Media and creative tools](#media-and-creative-tools)
- [Open reproductions and research](#open-reproductions-and-research)
- [Evaluation and calibration](#evaluation-and-calibration)
- [Guides and cookbooks](#guides-and-cookbooks)
- [Related lists](#related-lists)
- [Acknowledgements](#acknowledgements)

## Start here

**System One shape:** text or structured state + typed questions → constrained answers + probabilities → deterministic application code.

**Question primitives:** `Choice` selects an option, `Score` evaluates ordered rubric levels, and `Noul` returns a number from 0 to 1 representing the probability of "yes". Review or abstention behavior is defined in application code. See the [primitive reference](https://docs.typesafe.ai/primitives).

**Input boundary:** the hosted Jev model is text-only. Browser, audio, image, and robotics projects supply extracted text or structured observations, or use separate perception models. Independent multimodal reproductions are listed separately.

**Good fits:** semantic routing, triage, reranking, rubric scoring, moderation, verification, and low-latency decisions inside bounded workflows.

**Important caveat:** schema-valid output is not the same as a correct decision. Validate on your own data, calibrate thresholds, keep high-impact actions behind deterministic checks, and provide a human fallback.

## Recent developments

**September 18: Python SDK 0.7.0.** [Release notes](https://github.com/typesafe-ai/typesafe-sdk-python/releases/tag/v0.7.0) document a breaking serialization change from `msgspec` to Pydantic, a new `response_model` argument, and corrected serialization of `str` subclasses.

**September 18: OpenRouter listing.** Jev 1.13 is listed with a September 18 date. This is a provider listing date, not evidence of a separate new upstream model revision.

**September 16: Vercel AI Gateway integration.** The integration introduces typed evaluation via AI SDK's experimental `evaluate` API.

**Current model:** TypeSafe documents `jev-1.13.0`, with both `jev-latest` and `jev-preview` currently pointing to it. Pin the version when comparing evaluations.

**September 20: framework adoption.** Source-level Jev integrations are now present in LangChain, Pydantic AI, LiteLLM, Rig, Composio, Effect, BAML, Ax, and TanStack AI. Availability and release status vary, so inspect the linked repository before depending on a package.

## Official resources

- [TypeSafe AI](https://typesafe.ai/) - Product overview and early-access entry point.
- [Documentation](https://docs.typesafe.ai/) - Concepts, primitives, API, patterns, and SDK guides.
- [Introducing System One Models and Jev](https://typesafe.ai/blog/introducing-system-one-models-and-jev) - Launch post covering the model interface, RLCD, published performance claims, demos, and caveats.
- [typesafe-sdk-js](https://github.com/typesafe-ai/typesafe-sdk-js) - Official TypeScript and JavaScript SDK with inferred answer types.
- [typesafe-sdk-python](https://github.com/typesafe-ai/typesafe-sdk-python) - Official synchronous and asynchronous Python SDK.
- [system-one-adapter-python](https://github.com/typesafe-ai/system-one-adapter-python) - Drop-in adapter for comparing the System One interface with LLM providers.
- [skills](https://github.com/typesafe-ai/skills) - Official agent skills for building and evaluating System One workflows.
- [Models and aliases](https://docs.typesafe.ai/models) - Version IDs, current limits, pricing, and the distinction between stable and preview aliases.
- [Confidence](https://docs.typesafe.ai/confidence) - Distinguishes Choice/Score confidence from answer probability; Noul has no separate confidence field.
- [Jev 1.13 jaggedness](https://docs.typesafe.ai/model-jaggedness/jev-1.13) - First-party limitations covering arithmetic, dates, distractors, adversarial state, and structural inconsistencies.

## Provider integrations

- [Cloudflare AI](https://developers.cloudflare.com/ai/models/typesafe/jev/) - Provider-maintained `typesafe/jev` integration accepting state and typed questions.
- [Netlify AI Gateway](https://www.netlify.com/changelog/typesafe-jev-ai-gateway/) - Zero-configuration access from Netlify Functions through `@typesafe-ai/sdk`, with credentials and billing handled by Netlify.
- [OpenRouter](https://openrouter.ai/typesafe/jev-1.13) - Provider listing for `typesafe/jev-1.13`, alongside the moving `typesafe/jev-latest` alias.
- [Vercel AI Gateway](https://vercel.com/changelog/typesafe-ai-jev-now-available-on-ai-gateway) - `typesafe-ai/jev` through AI SDK's experimental `evaluate` interface; its Boolean primitive corresponds to TypeSafe's Noul.

## Framework integrations

Upstream framework integrations with inspectable Jev implementations. Presence on a default branch does not guarantee a stable package release.

- [Ax](https://github.com/ax-llm/ax) - Native TypeSafe client and Ax provider for Boolean, Choice, Score, and raw Jev questions, with answer validation and examples.
- [BAML](https://github.com/BoundaryML/baml) - The v1 nightly integration maps typed function return values to Jev questions; it is not part of the stable release line yet.
- [Composio](https://github.com/ComposioHQ/composio) - TypeSafe provider that shortlists tools, selects one from a bounded set, maps closed-set arguments, and exposes confidence and destructive-action gates.
- [Effect](https://github.com/Effect-TS/effect) - `@effect/ai-typesafe` decision model mapping Effect's classify, probability, and rating operations to Jev Choice, Noul, and Score questions.
- [LangChain](https://github.com/langchain-ai/langchain) - Python `TypeSafeClassifier` Runnable with batched typed questions plus model-routing and risky-tool middleware.
- [LangChain.js](https://github.com/langchain-ai/langchainjs) - JavaScript/TypeScript classifier Runnable and middleware for bounded routing and tool-call checks.
- [LiteLLM](https://github.com/BerriAI/litellm) - Jev-backed complexity routing and an optional relevance guardrail for compacting tool results before they return to an agent.
- [Milvus Model](https://github.com/milvus-io/milvus-model) - Python reranker adapter that sends candidate documents as Jev Noul questions in one request, then sorts the returned scores and preserves original document indices.
- [Pydantic AI](https://github.com/pydantic/pydantic-ai) - TypeSafe model provider that derives Jev questions from Pydantic output types and supports typed routing and fallback workflows.
- [Rig](https://github.com/0xPlaygrounds/rig) - Rust `rig-typesafeai` crate with typed Choice, Score, and Noul queries, response validation, examples, and fixtures.
- [TanStack AI](https://github.com/TanStack/ai) - `@tanstack/ai-typesafe` adapter exposing typed Boolean, Choice, and Score decisions through TanStack AI's `decide()` API.

## SDKs and developer tools

Community-maintained clients and tools; official TypeSafe SDKs are listed above.

- [advocaat](https://github.com/pithings/advocaat) - Small type-safe client for asking Jev questions about datasets.
- [discern](https://github.com/doeixd/discern) - TypeScript library for Effect: Jev's Choice, Noul, and Score answers become typed patterns with an explicit `Uncertain` branch, and procedure routing, with recording, replay, caching, and call budgets as `DecisionModel` middleware.
- [hunch](https://github.com/carldaws/hunch) - Probabilistic control flow for Ruby: `if Hunch.likely?("fraudulent", given: order)` branches on a typed Jev answer, with graded predicates from `possibly?` to `definitely?`.
- [jeff](https://github.com/saembit/jeff-cli) - Go CLI where Jev scores each item on each weighted dimension of a YAML spec in one request and code sums the weights into a ranking, with noul, choice and score commands whose thresholds become exit codes for shell and CI.
- [jegrep](https://github.com/can1357/jegrep) - Rust semantic grep that scores live repository files and ranges with Jev probabilities, without an embedding index or background daemon.
- [jev](https://github.com/dannote/jev) - Elixir/OTP client designed around GenServer replies and pattern matching.
- [jev-acp](https://github.com/formulahendry/jev-acp) - Standalone ACP agent exposing Jev Choice, Score, and Noul decisions through guided input and reusable templates, with typed results and probabilities.
- [jev-axi](https://github.com/shiftynick/jev-axi) - CLI for picking, rating, checking, ranking, triaging, and guarding from the shell.
- [jev-dsl](https://github.com/inanna-malick/jev-dsl) - Early-alpha Haskell DSL that encodes typed question packets and decodes answers; HTTP transport is left to the caller.
- [jev-mcp](https://github.com/blakestone-x/jev-mcp) - MCP server exposing classify, score, check, match, and screen tools.
- [jev-mcp](https://github.com/BYK/jev-mcp) - An eval-first MCP server for Jev, that returns typed judgments (noul, choice, score) with probabilities instead of generated text.
- [jev-shell-history](https://github.com/mrnugget/jev-shell-history) - Ranks existing zsh history entries for inline completion; accepting a suggestion does not execute it.
- [jev.nvim](https://github.com/valentynkit/jev.nvim) - Neovim plugin that splits the buffer into functions with Treesitter, scores each against a plain-language question with Jev, and ranks answers by probability in the quickfix window.
- [Jevbridge](https://github.com/gamesonrblx/Jevbridge) - ACP/MCP adapter for using Jev alongside coding and chat models.
- [jevclient](https://github.com/AboveColin/jevclient) - Async Python client for typed Jev questions and probabilities.
- [jevgrep (allebee)](https://github.com/allebee/jevgrep) - Jev decides, one Noul per line, whether each line of a log or other text stream satisfies a plain-English question; code applies the threshold and prints the matches grep-style, including from `tail -f`.
- [jevr](https://github.com/simxnherrera/jevr) - Native R client for typed questions and provider-independent answers through TypeSafe or OpenRouter.
- [jgrep (kyu1204)](https://github.com/kyu1204/jgrep) - Semantic grep for code, git diffs and CSV rows: one Noul per 5-60 line chunk, 16 chunks per Jev request, grep-style file:line output and exit codes for CI lint rules written in English; ships an interactive init and a Claude Code / Codex skill.
- [kojev](https://github.com/ItisNoMatter/kojev) - Kotlin Multiplatform client that answers Choice and Score questions as the caller's own enums; thresholds and routing stay in the caller's code.
- [laravel-typesafe-jev](https://github.com/Butochnikov/laravel-typesafe-jev) - Laravel integration with typed responses, async requests, and testing fakes.
- [neurolink](https://github.com/juspay/neurolink) - The pipe layer of an AI nervous system: TypeScript SDK connecting provider neurons — including TypeSafe Jev for `decide` — to an application across generate/stream/decide.
- [Ollaya](https://github.com/ollaya-dev/ollaya) - Rust daemon and CLI that pulls open decision models (Laya, decider, NLI, GLiClass) by name and serves them locally behind TypeSafe-compatible `/v1/systemone`, `/v1/decisions`, and `/v1/models` endpoints, so existing Jev clients switch with `TYPESAFE_BASE_URL`; the `laya` router picks an English or multilingual checkpoint per request, and answers come from these open models, not from Jev.
- [pytest-jev](https://github.com/allebee/pytest-jev) - pytest plugin where Jev decides whether each plain-English claim about a test's text holds, and the test passes only when every claim clears 0.8 (or stays at or below 0.2 for claims that must not hold), with Choice and Score answers compared by probability.
- [ruby_decision_model](https://github.com/obie/ruby_decision_model) - Ruby client with standard-library transport for TypeSafe and OpenRouter decision endpoints.
- [semdecide](https://github.com/sharziki/semdecide) - Typed semantic decisions for Unix pipelines and CI.
- [stuntd](https://github.com/bladedevoff/stuntd) - Local proxy that serves the Jev System One API from the open Laya model and, placed in front of a Jev upstream, records each Choice, Score, or Noul answer to train a per-question head; code applies a calibrated confidence threshold to decide whether the head or the upstream answers and demotes the head on drift.
- [typesafe-go](https://github.com/zhirschtritt/typesafe-go) - Idiomatic Go SDK for the TypeSafe API.
- [typesafe-java](https://github.com/dfa1/typesafe-java) - JDK 21+ client, modular by design, with a dedicated testkit module for unit testing callers.
- [typesafe-mcp](https://github.com/itsmostafa/typesafe-mcp) - MCP connector that gives agents access to Jev decisions.
- [typesafe-sdk-java](https://github.com/Premo-Cloud/typesafe-sdk-java) - Community Java 17 client for Choice, Score, and Noul, with an optional Spring Boot starter.
- [zod-jev](https://github.com/jomatsu/zod-jev) - Pairs local Zod shape validation with Jev semantic validation.

## Agents, coding, and guardrails

Source-reviewed experiments and integrations. A model judgment does not establish safety or replace the host application's permission checks.

- [agent-router](https://github.com/nidhi-singh02/agent-router) - Pre-release Herdr integration that filters eligible coding models by quota and policy before Jev ranks them.
- [blink](https://github.com/ellipsis-dev/blink) - Navigates file and directory names with Jev-guided walkers to find codebase paths for a natural-language query.
- [Canny](https://github.com/qkal/Canny) - Evidence ledger that challenges unsupported "done" claims from coding agents.
- [Codex Jev Router](https://github.com/suenot/codex-jev-router) - Uses Jev Choice and Noul decisions to select a Codex subagent model and reasoning effort; uncertain decisions fall back to Sol.
- [commit-miner](https://github.com/devanshbatham/commit-miner) - Classifies Git diffs and commit messages into change types and candidate security-fix/CWE labels for inspection.
- [Edward](https://github.com/VeridicalTech/Edward) - External control plane for coding agents: one batched Jev call judges the whole cross-turn trajectory (continue, pause, or escalate, confidence-gated), while deterministic code owns dangerous-command blocking, budget caps, intervention execution, and an Ed25519-signed receipt chain.
- [foreman](https://github.com/thruwire/foreman) - Software-factory supervisor that uses Jev to keep coding agents on task.
- [is-malicious](https://github.com/luantak/is-malicious) - Scans source, configuration, build, and CI files with Jev, then reports suspicious behavior and implicated lines before the code is run.
- [jev-agent-skill](https://github.com/yuyang2230/jev-agent-skill) - Claude Code/ZCode skill that offloads classify, screen, score, and compliance-check judgments to Jev via OpenCode Zen's free tier; ships a retry-hardened zero-dependency caller and a shop comment-triage pipeline.
- [jev-belay](https://github.com/valentynkit/jev-belay) - Claude Code Stop hook that checks the transcript for evidence before trusting a "done" claim, spending one four-question Jev call only when files changed with no passing check since, and failing open on every error path.
- [jev-codex-router](https://github.com/0xNatoshi/jev-codex-router) - Per-turn Codex model, reasoning, and speed-mode routing.
- [jev-commit](https://github.com/valentynkit/jev-commit) - Pre-commit hook where one Jev call judges whether the commit message matches the staged diff, flags debug leftovers and unmentioned work, and blocks only when it detects a credential.
- [jev-engineering](https://github.com/eugeniughelbur/jev-engineering) - Decision layer for coding agents: deterministic hard rules, then a Jev call, exposed as a Claude Code PreToolUse hook, an MCP server, a loopback service and a shared team policy. Ships a 300-call injection kit and its results: blunt injections moved 0 of 30 dangerous commands but caused 10% false denials on safe ones, authority framing moved 3 of 30.
- [jev-guard (leepokai)](https://github.com/leepokai/jev-guard) - Cross-agent tool-call risk scoring with allow, ask, and deny outcomes.
- [jevguard-mcp](https://github.com/seb4ez/jevguard-mcp) - Zero-dependency MCP server and Python runtime where Jev evaluates shell command safety, code patch regression risk, and discrete decision certainty, with local SQLite WAL caching and automatic closed-world escape injection.
- [jev-pref](https://github.com/doeixd/jev-pref) - Linter that has Jev check code changes against project preferences from `jev-pref.json` and feeds findings back to coding agents.
- [jev-review](https://github.com/devagrawal09/jev-review) - Staged code-review workflow with a local dashboard.
- [jev-review MCP plugin](https://github.com/NiazMorshed2007/jev-review) - Local-first continuous software-quality review for coding agents.
- [jev-router](https://github.com/gargpratyush/jev-router) - Chooses a model for each fresh Claude Code or Codex turn while wrapping the existing CLI.
- [JevRouter](https://github.com/BillionsBobby/JevRouter) - Routes agent requests across models, subagents, skills, MCP tools, CLIs, and plugins with Jev Choice decisions; the host filters by availability, permissions, risk, and confirmation before anything executes.
- [jev-scout](https://github.com/kierandotai/jev-scout) - MCP server that scores an agent's every search query, result, and fetched page for relevance and credibility, with session budgets, SSRF-guarded fetching, and a live decision dashboard.
- [jev-skill-router](https://github.com/shimo4228/jev-skill-router) - Claude Code plugin whose UserPromptSubmit hook asks Jev one `Choice` over the installed skill roster plus `Noul` gates, while code applies the thresholds and names at most one skill; it starts in a shadow mode that only logs the decision.
- [jev-use](https://github.com/shitianfang/jev-use) - Claude Code / Codex / pi plugin where Jev answers batched noul, choice, and score questions and risk-checks tool calls, while a typed escalation contract hands writing and unsure steps back to the LLM.
- [JevLoop](https://github.com/parkavenue9639/jevloop) - Python agent runtime where Jev `Choice` decisions select tools and targets, uncertain decisions escalate to an LLM, and a shared guarded kernel supports isolated Docker workspaces and paired LLM-only comparisons.
- [jevwire](https://github.com/Brainwires/jevwire) - MCP tools, an embeddable decision library, and advisory or restrictive Claude Code hooks; judgments do not grant native permissions.
- [Jevonian](https://github.com/xinyao27/jevonian) - Local OpenAI/Anthropic-compatible proxy where one Jev call answers model route and thinking level for `jevonian/auto`, after deterministic code has already filtered candidates by wire protocol, context window, thinking-level floor, and spent quota windows; `minConfidence` marks a low-confidence route in the ledger instead of silently accepting it, and Jev is skipped entirely for pinned models, explicit `jevonian/<route>` requests, and `routing.mode: "off"`.
- [langchain-skill-router](https://github.com/deyna256/langchain-skill-router) - Per-turn skill routing for LangChain deepagents: Jev ranks the SKILL.md catalog against the request and the recent conversation and verifies the top candidates, while the library applies the thresholds and either loads one skill's instructions or offers a short list; the judge is a protocol, so a self-hosted model or static rules can take Jev's place.
- [Oko](https://github.com/bartlomein/oko) - Jev judges whether each keyword-shortlisted code chunk implements what a coding agent asked for; code applies the threshold and returns the accepted chunks as excerpts over MCP.
- [opencode-jev-orchestrator](https://github.com/aaronshaf/opencode-jev-orchestrator) - Keeps an OpenCode parent model fixed and uses Jev difficulty judgments to delegate harder turns to temporary subagents.
- [perch](https://github.com/lakeday-org/perch) - Semantic code linter that evaluates code units against configurable Jev questions.
- [pi-jev](https://github.com/y0usaf/pi-jev) - Measured tool-call gate and general typed decision layer for the Pi coding agent.
- [pi-warden](https://github.com/DevMortimer/pi-warden) - Pi extension that judges rule compliance, risky actions, stuck loops, and completion claims; enforcement depends on the hook and policy.
- [skillbox](https://github.com/kitze/skillbox) - Self-hosted skill library with optional Jev relevance recommendations over an authorized catalog.
- [skillranker](https://github.com/Dicklesworthstone/skillranker) - Rust CLI that ranks agent skills against live session context and can abstain.
- [slop-grader](https://github.com/lukstei/slop-grader) - Rule-based text grader that uses Jev scores and line-by-line flags to audit documents against custom rulesets and guide an AI agent to auto-fix violations.
- [supercov](https://github.com/supercorp-ai/supercov) - Scores source files so coding agents can prioritize code-quality work.
- [Switchboard](https://github.com/ruban-24/switchboard) - Claude Code and Codex wrapper that uses Jev to assess a new conversation's task, applies deterministic confidence rules to choose a model and reasoning effort, and pins the pair through follow-ups, tool calls, and resume to avoid unnecessary prompt-cache disruption.
- [taste-lint](https://github.com/mblode/taste-lint) - CLI that uses Jev probabilities on semantic taste checks to catch AI slop in UI, copy, and agent instructions before ship.
- [wakegate](https://github.com/shitianfang/wakegate) - Experimental gate where Jev decides whether a timer or incoming event is worth resuming a sleeping agent's LLM; code skips only when Jev is confident and always wakes on user messages, errors, and a skip limit.

## Context and compaction

These tools select what reaches a model. Preserving retained text verbatim does not prove that omitted history was unnecessary.

- [fast-dev-compaction](https://github.com/leonaaardob/fast-dev-compaction) - Codex port that restores Jev-selected verbatim history around native session compaction.
- [fast-jev-compaction](https://github.com/tamaratran/fast-jev-compaction) - Claude Code plugin and library that score tool-call/result pairs for deletion or truncation while retaining selected text verbatim.
- [pi-fast-jev-compaction](https://github.com/joelhooks/pi-fast-jev-compaction) - Pi extension that prunes stale tool history and leaves summary compaction to Pi when pruning is insufficient.
- [pi-jev-compact](https://github.com/ilkerulusoy/pi-jev-compact) - Selective, verbatim context compaction for Pi using Jev model.
- [pi-jev-context](https://github.com/kevinpita/pi-jev-context) - Opt-in Pi extension that filters older messages from model requests while preserving the original session history.
- [winnow](https://github.com/GhalebDweikat/winnow) - Judges tool results before admitting them into Claude Code context.
- [yoshi](https://github.com/compozy/yoshi) - Experimental Claude Code/Codex proxy that uses Jev to prune request context while preserving tool-call protocol structure.

## Browser and computer use

These projects can operate real browsers or devices when enabled. Published demos have task-specific success criteria and do not establish general reliability.

- [BrowserClaw](https://github.com/GoldenLoaf24h/browserclaw) - Zero-lock, session-preserving Chrome MCP server that couples a local Jev System One semantic micro-loop (`chrome_act_toward_goal`) with an 85%+ pruned DOM tree (Shadow DOM & iframe pierced), dispatching native CDP events (`isTrusted: true`) on active logged-in sessions without focus theft.
- [jev-browser](https://github.com/jkudish/jev-browser) - Browser-use experiment powered by Jev decisions.
- [jev-browser-use](https://github.com/wy-coliney/jev-browser-use) - Codex browser skill that uses Jev for navigation and target selection while Codex handles text entry and outcome verification.
- [jev-social](https://github.com/socai-io/jev-social) - Local Instagram and TikTok research app where Jev selects a platform and bounded socai operation from observed state, while code enforces confidence and the socai CLI executes the browser step.
- [jev-ultrafast](https://github.com/browser-use/jev-ultrafast) - Browser agent where Jev selects an operation and compatible DOM target, and a separate LLM supplies typed text.
- [jev-voice-browser](https://github.com/moritzkremb/jev-voice-browser) - Maps partial speech transcripts to browser intents and observed targets, with code deciding whether to act, wait, or ask.
- [Jev for Chrome](https://github.com/chy4pro/jev-for-chrome) - Unofficial Chrome extension (Manifest V3) port of Jev Ultrafast: Jev picks the operation and DOM element in one request, a small text model writes typed values, and it runs in the user's own tabs through OpenRouter, TypeSafe or Cloudflare; includes a 17-task headless-Chromium suite with recorded traces.
- [mobile-jev](https://github.com/droidrun/mobile-jev) - Android agent using Mobilerun observations and bounded Jev actions; execute mode controls a real device, while the published Uber demo stops before booking.
- [typesafe-computer-use](https://github.com/awlevin/typesafe-computer-use) - macOS computer-use experiment using OCR plus bounded Jev action selection.

## Routing, data, and workflows

- [algovault-integrations: typesafe-jev](https://github.com/AlgoVaultLabs/algovault-integrations/tree/main/examples/typesafe-jev) - Jev decides whether to act on a composite AlgoVault verdict (direction, confidence, regime) for a crypto perp market now, and how well the regime fits a directional entry; code computes position conflict, applies every threshold, and logs act, hold, or escalate. Read-only: it never places orders, and runs as a dry run with no key required.
- [duckdb-jev](https://github.com/colliber/duckdb-jev) - DuckDB extension that exposes Jev judgments as SQL values with return types derived from the declared criteria.
- [HA-Jev](https://github.com/AboveColin/HA-Jev) - Home Assistant integration exposing typed answers as sensors, automation actions, and an Assist conversation agent.
- [hono-jev-router](https://github.com/yusukebe/hono-jev-router) - Routes Hono HTTP requests by meaning.
- [Inbox Zero](https://github.com/elie222/inbox-zero) - Email assistant where Jev is an optional classifier backend returning bounded categories and yes/no probabilities.
- [jev-align (Sutro)](https://github.com/sutro-sh/jev-align) - Active-learning CLI where Jev evaluates rows and surfaces uncertain or audit samples for human labeling, then GEPA proposes revised decision definitions that the user can accept or reject.
- [jev-curate](https://github.com/AkashPriyadarshii/jev-curate) - Streaming filter and scorer for Parquet and JSONL datasets.
- [jev-guard (klauswg)](https://github.com/klauswg/jev-guard) - Real-time deposit/withdrawal risk-triage gateway for crypto exchanges: Jev answers four typed questions per transfer while a hard-rule layer vetoes and a direction-aware Java gate composes the final action; ships a 100-sample, three-column calibration (rules-only vs Jev vs combined) with stated limitations.
- [jev-logtriage](https://github.com/jyatesdotdev/jev-logtriage) - Jev scores collapsed log batches for noise, severity, and whether an operator should act. Code maps the answers to suppress, watch, review, notify, or page. Nothing is executed.
- [JevMail](https://github.com/fazlerocks/jevmail) - Read-only Gmail triage that stores messages locally and asks Jev for bounded category, urgency, and human-sender probabilities.
- [jev-reranker](https://github.com/hotchpotch/jev-reranker) - Retrieval and RAG: uses Jev Noul judgments to assess retrieved documents for relevance and usefulness as answer evidence, then sorts results and optionally filters them using a configurable threshold.
- [Jev Reranker (Rust CLI)](https://github.com/shinpr/jev-reranker) - Rust JSON-in/JSON-out CLI that asks Jev about relevance, usable evidence, or which source text to retain, then applies the resulting order and thresholds in code.
- [jev-research-pipeline](https://github.com/shimo4228/jev-research-pipeline) - Daily research monitor: for every fetched paper and each of the author's open research questions, Jev answers Noul gates (on topic, method transferable, evidence compatible) and Score dimensions through Pydantic AI's typesafe: model; code routes each pair to keep / review / drop, and Qwen writes one question-centric Obsidian note per research line.
- [jev-reviewer](https://github.com/choxos/jev-reviewer) - Research-document extraction aid where Jev selects and verifies source lines for verbatim quotes; findings require human review and are not clinical decisions.
- [jev-search](https://github.com/superagents-lab/jev-search) - Uses Jev to select search sources and rank Search1API results, returning source links and snippets.
- [jev-sheets](https://github.com/Cab14bacc/jev-sheets) - Google Sheets custom functions (`JEV_IF`, `JEV_PROB`, `JEV_CHOICE`, `JEV_SCORE`) where Jev answers a Noul, Choice, or Score question per cell; the sheet formula applies the threshold or minimum confidence and returns `UNSURE` below it.
- [jev-trade](https://github.com/aowang-ai/jev-trade) - Hyperliquid trading desk where Jev answers Choice questions for long/short, open/close/hold, and leverage; application code quotes or sends no order. Defaults to a dry run; a live key can place real orders.
- [jev-trader](https://github.com/jarrodwatts/jev-trader) - Kuru/Monad trading experiment with optional Jev buy/sell decisions; defaults to a mock model and dry-runs without a private key, but configured execution can place real orders.
- [jev-tree](https://github.com/reachjalil/jev-tree) - Recursive choice over taxonomies larger than Jev's direct option limit.
- [Jev Web Analyzer](https://github.com/replynodes/jev-web-analyzer) - Fetches a public SaaS page as Markdown, then asks Jev ten bounded questions about likely first-visit comprehension; URL validation, caching, sanitization, and presentation remain deterministic. [Demo](https://replynodes.com/jev-web-analyzer/).
- [Jev Wrapped](https://github.com/gaborishka/jev-wrapped) - Telegram channel X-ray: for each public post of the last twelve months Jev answers a Choice over ten kinds of post and three yes/no questions (paid ad, clickbait, emotional pressure); deterministic code reads the posts from Telegram's public web preview, samples up to 1,500 evenly across the year, applies fixed thresholds and turns the answers into a card with the monthly mix and links to the highest-scoring posts.
- [jevlogs](https://github.com/reachjalil/jevlogs) - OpenTelemetry log triage before more expensive analysis.
- [JevPDF](https://github.com/kylemclaren/jevpdf) - Browser PDF search where pdf.js extracts lines locally and Jev answers one Noul per line on whether it answers the query; code highlights lines above a 0.55 threshold ranked by probability, and only extracted text is sent to TypeSafe.
- [jevql](https://github.com/kylemclaren/jevql) - Psql-shaped client and Go/TypeScript/Python SDKs for vanilla PostgreSQL where Jev makes Noul, Choice, and Score judgements about individual table rows after the plain SQL has run on the server, and the client applies the resulting filter, sort, or group.
- [jevsearch](https://github.com/kylemclaren/jevsearch) - Site-search block for shadcn/ui where a local keyword pass shortlists up to 20 pages and one Jev request answers a Noul per page, a Choice for the single best answer, and a Noul for whether any page answers; code blends the answers, drops hits under a threshold, and keeps keyword order if TypeSafe is unavailable.
- [jevsql](https://github.com/EugeneBoondock/jevsql) - SQL-like filtering, ranking, classification, and scoring with natural-language predicates.
- [llama-index-jev](https://github.com/WiktorB2004/llama-index-jev) - LlamaIndex reranker and selector using Jev Score and Choice answers, with configurable confidence handling.
- [n8n-nodes-typesafe-jev](https://github.com/n3ndor/n8n-nodes-typesafe-jev) - Community n8n node for asking multiple typed questions over workflow state.
- [Paper Radar](https://github.com/Eliot5566/JEV-Paper-Radar) - Daily arXiv/bioRxiv radar that asks Jev one Noul per plain-English interest for every new paper, then publishes a must-read page and RSS feed from a fork-and-go GitHub Action; 501 papers judged in 33s for $0.0196, with a `calibrate` command that measures calibration on your own labels.
- [pg-jev](https://github.com/realZachi/pg-jev) - PostgreSQL extension for semantic questions over table rows.
- [pg_typesafe](https://github.com/giuliosmall/pg_typesafe) - Pre-alpha PostgreSQL C extension exposing Choice, Noul, Score, and batched judgments from SQL.
- [tax-doc-classifier](https://github.com/kyotofin/tax-doc-classifier) - Classifies text-bearing PDF pages into IRS form and page-kind candidates with a confidence gate; document triage, not tax advice, and scanned pages need OCR.
- [tiershift](https://github.com/iamvatsalpatel/tiershift) - Policy-bounded model routing for TypeScript and Python.
- [typesafe-jev-workflow](https://github.com/GiesN/typesafe-jev-workflow) - LangGraph email-intent workflow using a typed Jev choice.
- [World Monitor](https://github.com/koala73/worldmonitor) - Geopolitical dashboard that batches Jev 1.13.0 headline-severity and topic classifications, validates the answers, and falls back when classification fails.

## Games, robotics, and interactive demos

- [Embodied Jev](https://github.com/FBddcz/embodied-jev) - MuJoCo Franka Panda workbench where Jev can choose from bounded simulator actions over structured observations; deterministic code owns physics and safety checks, and the published Jev comparison is still pending.
- [heist-one](https://github.com/AbdelStark/heist-one) - Browser stealth game where Jev judges guards while deterministic code owns the world.
- [jev-canvas](https://github.com/gaborishka/jev-canvas) - Voice and finger-pointing control of a tldraw canvas: Jev picks the action, target shape and place from each partial transcript plus the fingertip position; deterministic code applies thresholds and executes the edit.
- [jev-drone](https://github.com/RomanSlack/jev-drone) - Simulated MuJoCo quadrotor with Jev making slower tactical judgments from processed camera observations; deterministic code controls flight.
- [jev-experiments](https://github.com/dabit3/jev-experiments) - Collection of inspectable Jev demos, including scripted support conversations with typed intent, escalation, and suggested-response decisions.
- [jev-palette](https://github.com/amycardoso/jev-palette) - Command-palette demo where a single Choice question over a 77-command catalog turns the returned probability distribution into the per-keystroke ranking for Portuguese or English input; deterministic code executes the selected command, with a classic fuzzy-match baseline shown side by side.
- [jev-plays-pokemon-red](https://github.com/valentynkit/jev-plays-pokemon-red) - Pokemon Red on PyBoy where deterministic code owns the route and arithmetic and Jev picks only at branches, with every battle turn's faint prediction scored by Brier against the emulator's RAM state.
- [jev-tetris](https://github.com/thelau/jev-tetris) - Tetris where deterministic code enumerates every reachable placement, including tucks and spins, and writes each one as an English sentence; Jev returns a probability for all of them across five Choice questions, and the highest-weighted option is played while the whole distribution is drawn on the board. Ships a shuffled-probability control and a 23-line regex baseline over the same sentences, which outscores the model.
- [JevPilot](https://github.com/standardagents/jevpilot) - Three.js driving simulation where Jev chooses among candidate paths and speeds while local code handles vehicle dynamics and geometry.
- [JevScape](https://github.com/Skyvern-AI/jevscape) - RuneBench-based RuneScape harness that maps Jev choices to a bounded game-action catalog and records tick-level results.
- [Jevtown](https://github.com/gaborishka/jevtown) - Town of 10,000 computed personas where Jev scores a post, listing, product, or headline against about 60 audience attributes to plan who sees it, then answers one batched Choice question per persona for the reaction (scrolled past, stopped, liked, disliked, reposted, followed, blocked) and a follow-up question for listings and products; deterministic code computes every persona from its id, picks each wave, samples the reaction from the returned probabilities with a fixed seed, and stops the text when sorry reactions outweigh glad ones.
- [killmyidea](https://github.com/monteduro/killmyidea) - Startup-idea evaluator that chooses kill, fix, or ship.
- [Magic Jev Ball](https://github.com/mikecann/magic-jev-ball) - three.js Magic 8 Ball where a Convex action asks Jev one Choice question over the 20 classic answers; the page shows Jev's probability for every answer and displays the highest-probability one.
- [Soupbase](https://github.com/spoonnotfound/soupbase) - Jev `Choice` judgments answer lateral-thinking puzzle questions and assess proposed solutions, while application code requires supported facts, a coherent explanation, and sufficient confidence before marking a puzzle solved.
- [tsai-sc](https://github.com/phyous/tsai-sc) - Original StarCraft shareware controlled with recorded Jev action probabilities.
- [typesafe-mario](https://github.com/fhshaik/typesafe-mario) - Super Mario Bros. agent choosing actions from structured emulator state.
- [typesafe-snake](https://github.com/sorrycc/typesafe-snake) - Snake autoplayer with one typed decision per tick and code-generated legal moves.

## Media and creative tools

- [Jev Paint](https://github.com/achimala/jev-paint) - Local browser app that turns batched per-pixel Jev distributions into paintings; prompts describe pixels and regions rather than sending raw images.
- [jev-skip](https://github.com/valentynkit/jev-skip) - Browser extension that reads the YouTube caption track and paints a per-segment sponsor probability on the seek bar before the intro ends, with no crowd database; reports catching 77% of SponsorBlock's sponsor seconds across 23 videos at $0.0008 a video.
- [jevmeter](https://github.com/ChetasLua/jevmeter) - Scores every sentence in a video and renders the result as an overlay.
- [Jevthoven](https://github.com/cocktailpeanut/jevthoven) - Symbolic-music studio where Jev chooses plans, instruments, and bar patterns, and code renders editable music and MIDI.
- [PlotVeil](https://github.com/Dearest/plotveil) - Chrome extension where one Jev Noul question per YouTube comment answers whether it reveals a concrete plot event of the video being watched or of another title the user protects; the extension owns the 0.85 / 0.7 / 0.5 threshold and keeps the comment covered when the check fails.
- [SlidePilot](https://github.com/harshil1712/slidepilot) - Experimental Slidev controller that judges speech transcripts for slide completion, with deterministic checks and manual navigation.
- [Sponsor Skip](https://github.com/trungdq88/youtube-sponsor-detection) - Finds sponsor reads in YouTube transcripts or transcribed audio while code owns timestamps and playback skipping.
- [unclutter](https://github.com/kitze/unclutter) - Browser extension that uses Jev to identify page clutter and saves reusable, reversible hiding rules.
- [Vibe Check for X](https://github.com/RafalWilinski/vibecheck) - Chrome extension that scores draft posts and reply context before posting; optional media descriptions come from a separate vision model.

## Open reproductions and research

These projects explore Jev-like interfaces or open implementations. They are independent efforts, not official TypeSafe releases or verified reproductions of its proprietary architecture, RLCD training, or calibration.

- [AnyJev](https://github.com/MorrisZJ/AnyJev) - Library that turns any open transformers or vLLM model into a Jev-style Choice/Score/Noul decision from one prefill with no training, using cyclic-shift marginalization and a label-free prior estimate to reduce option-order sensitivity; every result is labeled raw, L0 or L1 by the debiasing and calibration it carries, and the committed bench reports order-flip rate, Brier and ECE on its own task set.
- [Diffusion Jev](https://github.com/Hangzhi/diffusion-jev-sglang) - Independent DiffusionGemma/SGLang implementation of Choice, Score and Noul for text and images, with a doodle-classification playground and public evaluation artifacts; option scores come from self-conditioned denoising logits and are not calibrated correctness probabilities.
- [Jev Visual](https://github.com/hr98w/jev-visual) - Educational MLX/Qwen vision-language experiment sharing image context across candidate-scoring questions; its probabilities are not calibrated correctness estimates.
- [JevForge](https://github.com/zwliJay/jev-forge) - Auditable Qwen3.5-0.8B pipeline covering data synthesis, training, calibration, fixed evaluation, Jev-compatible serving, and public model and dataset artifacts; its metrics are project-local.
- [Jevlike](https://github.com/vinnylarouge/jevlike) - Trainable encoder and option-attention head for variable candidate sets, with separate visual game experiments.
- [Laya Vision](https://github.com/r33drichards/laya-vision) - Research fork of Laya that replaces its text encoder with SmolVLM-256M so typed `choice` and `noul` decisions are read from an image plus optional text in one forward pass with no generated text; reports 75.2% accuracy and post-calibration ECE 0.034 across A-OKVQA, ScienceQA image questions, and a VQAv2 yes/no re-split, and states that `score` questions are untrained and meaningless.
- [LitJev](https://github.com/zhengxuyu/litjev) - Reproduction of Jev that turns any Qwen model into a fast decision model, serving the same `/v1/systemone` schema (Choice, Score, Noul) with no training and no generated answer text.
- [jevmlx](https://github.com/bnsd55/jevmlx) - Jev-style parallel constrained decisions for MLX models on Apple Silicon.
- [kev](https://github.com/jaredpalmer/kev) - Qwen2.5-0.5B adapter and decision head with training code, released weights, and parallel typed-question inference.
- [minojev](https://github.com/zeredy879/minojev) - Head-training reproduction: a frozen Qwen3-1.7B backbone plus a ~0.8M-parameter decision head returns calibrated Choice/Boolean/Score distributions in one forward pass with zero decoded tokens; ships an 8k-request converted dataset, source-isolated OOD evaluation, and a same-backbone generation baseline (95.8% vs 80.0% on its own balanced suite, ECE 0.024).
- [NanoJev](https://github.com/TianyuCodings/NanoJev) - Small parallel-decision model with dynamic candidates, a training pipeline, and recorded game comparisons that include shared code planning.
- [open-jev (MLX)](https://github.com/daseinlabs/open-jev) - Gemma 3 option scorer for Apple MLX that shares one prefill across candidate continuations and exposes a System One-compatible endpoint; its docs show zero-shot overconfidence and an optional trained head.
- [openjev](https://github.com/zhihz/openjev) - Local bilingual probability decisions from context, questions, and candidate answers.
- [OpenJev (DiffusionGemma)](https://github.com/razorback16/openjev) - Independent Jev-compatible server over DiffusionGemma/vLLM; the documented setup requires custom vLLM patches.
- [openJev Verdict 2.0](https://github.com/Heman10x-NGU/openJev-verdict-2.0) - ModernBERT-based decision model with separate distribution and confidence heads, saved evaluation artifacts, public weights, and an in-browser WebGPU demo; reported results are project-local.
- [openjev-sglang](https://github.com/ekzhang/openjev-sglang) - Jev-compatible API endpoint backed by open models and prefill-only inference.
- [openvons](https://github.com/genai-craft/openvons) - Open decision layer for finite options across text, images, and Japanese voice commands.
- [parallelConstraintDecoding](https://github.com/stephanj/parallelConstraintDecoding) - Java and llama.cpp experiments in parallel constrained decoding.
- [PlayJev](https://github.com/OmniJev/PlayJev) - Open 0.8B vision-language model that reads a 448 px game frame and returns one move from the game's typed option list with a probability on each, one forward pass and no generated text; the game loop executes the argmax, the confidence gates an optional handover to a search program, and the weights and a ten-game browser demo are public.
- [poorjev](https://github.com/rupeshpoojary9/poorjev) - Local-first reproduction of the Choice/Score/Noul interface on commodity zero-shot NLI models, adding temperature scaling and conformal abstention; ships a reproducible calibration eval (ECE 0.170 to 0.071 on its own labeled set) and runs offline with no API key.
- [Prosodia](https://github.com/alperiox/audio-jevlike) - Audio-native Jev-style decision model: a frozen Whisper encoder turns speech into one shared state and typed questions branch over it in parallel, returning Choice/Score/Noul distributions over emotion, sentiment and acoustic properties with no ASR step and no generated text; question text and option sets are supplied at request time, and a hosted demo takes mic input or an uploaded file.
- [reflex](https://github.com/kshetrajna12/reflex) - Open-model decision engine with shared-state inference, isolated question branches, and a WebGPU demo; browser and Python configurations differ.
- [ruling](https://github.com/bradAGI/ruling) - Reproduction that serves Jev's `/v1/systemone` schema from a frozen MLX model or OpenAI-compatible endpoint by reading option probabilities from the logits, with option-order averaging, temperature calibration, and a harness that replays Jev's published answers on public judgments.
- [SemIf](https://github.com/TheoLeeCJ/SemIf) - Formerly OpenJev: an independent study of typed option readout from frozen open models, with shared-prefix experiments and a WebGPU demo.
- [Simple Jev](https://github.com/featherless-ai/simple-jev) - Transforms compatible open-model logits into typed decisions without a separately trained classifier head; model compatibility is constrained.

## Evaluation and calibration

Results belong to each project's dataset, prompts, model version, and measurement setup. Inclusion means the evidence is inspectable, not that benchmarks were independently rerun.

- [Convex Decision Evals](https://github.com/get-convex/convex-evals/tree/main/runner/decisions) - Leaderboard that asks Jev (native Choice questions through OpenRouter's decisions endpoint) and 14 other models (structured output limited to A-D, no tools, low reasoning effort) 108 verified four-option questions about the Convex backend platform, each asked 3 times per run with shuffled options (random guessing is 25%); in the 23 Sept 2026 benchmark jev-1.13 scored 84.6% ±0.7 (13th of 15) at a 199 ms median per question and $0.0088 per full run, against 98.0% at 2.12 s and $1.59 per run for the top model, GPT-6 Astra. [Leaderboard](https://www.convex.dev/evals/decision), [per-answer explorer](https://convex-evals.netlify.app).
- [Janus](https://github.com/FirasSX914/Janus) - Measures when to use Jev versus other models and routes accordingly.
- [JevBench](https://github.com/fstandhartinger/jevbench) - Public evaluation of Jev and Jev-class typed-decision systems, with versioned aggregate results and measurement conditions.
- [Jev Calibration Study (Nautilus Assay)](https://github.com/chunxiaoxx/nautilus-compass/blob/main/docs/wall/GENESIS_HOSTED_JEV_CALIBRATION.md) - Independent, reproducible calibration evaluation of hosted Jev (240 seeded questions, all raw artifacts published): accuracy 92.2%, Brier 0.048, ECE 0.041 overall.
- [Jev Does Not Play Dice](https://github.com/KantaHayashiAI/jev-does-not-play-dice) - Calibration check on inputs with known true probabilities (hidden fair dice, coins, four-way spinners) and on synthetic forecast documents; Choice put 82.9% on face 1 across all 400 die rolls at 19.0% accuracy and turned a stated 30% shortage risk into 5.3%, while Noul returned 26.7%; raw responses and offline recomputation in the repo, run in launch week against jev-1.13.0. [Write-up](https://kantahayashiai.github.io/posts/jev-does-not-play-dice/).
- [Jev IDS](https://github.com/jev-ids/jev-ids) - Intrusion-detection prototype where one Noul (attack or not) and a five-way Choice (category) are asked per NSL-KDD network flow and Python applies a 0.5 cut; ships a 300-flow pilot comparison against GPT-5.6 Luna and a few-shot Random Forest with latency, cost, and novel-attack recall, and lists its limits (pilot split, gateway retries, list-price costs).
- [Jev in Search: Three Practical Evaluations](https://zc277584121.github.io/rag/2026/09/22/jev-search-deep-evaluation.html) - Independent experiments on search stopping, memory reranking, and multi-hop relation selection, with implementation links and limitations including private data, unequal sample counts, and a simulated speed illustration.
- [jev-behavior-study](https://github.com/RINNECODER/jev-behavior-study) - Independent synthetic-task study of Jev 1.13.0 framing sensitivity and failures, with raw responses and offline report checks.
- [jev-benchmarks](https://github.com/AbdelStark/jev-benchmarks) - Reproducible evaluation for calibration, selective risk, and latency.
- [jev-decision-benchmarks](https://github.com/baibizhe/jev-decision-benchmarks) - Independent evaluation of Jev on MetaTool, When2Call, and BFCL V4 agent decision tasks, focusing on tool selection, abstention, and tool-use decisions. Includes comparison tables against Claude, Qwen, and GPT models.
- [jev-eval](https://github.com/4esv/jev-eval) - Independent Jev versus GPT-5.6 Terra comparison on three labeled classification tasks, reporting accuracy, calibration, latency, and cost.
- [jev-eval-agent](https://github.com/vinilana/jev-eval-agent) - Compares LLM tool selection with Jev routing in a personal-assistant harness containing 100 mocked tools.
- [jev-fanout-bench](https://github.com/blowxian/jev-fanout-bench) - Reproducible comparison of batched and one-question-per-call Jev requests whose 2,976-request OpenRouter run reports approximately 261 fixed input tokens per request, observed charges matching the published token rate, and batched-vs-single answer differences comparable to repeat-request noise.
- [jev-korean-benchmark](https://github.com/mahlernim/jev-korean-benchmark) - Small Korean/English sample study with recorded responses, including medical-text questions; not a clinical validation.
- [jev-orderby-bench](https://github.com/yodablocks/jev-orderby-bench) - Measures whether ORDER BY over a Jev probability is defensible (inversion rate, Score ordinality against a human grade, calibration, wording invariants, sort-key ties) under a pre-registered gate; passes on 20 Newsgroups topics, fails four of six conditions on Amazon ESCI product relevance, and shows a DuckDB extension's default 40-row batching fails the ranking gate that one row per request passes.
- [jev-rerank-bench](https://github.com/anessbelbati/jev-rerank-bench) - Fourteen-dataset reranking study with saved raw responses, paired bootstrap intervals, order-sensitivity checks, and no-relevant-document tests; comparisons remain study-specific.
- [jev-scout golden-set study](https://github.com/kierandotai/jev-scout/blob/main/docs/accuracy/2026-09-19-jev-golden-set-study.md) - Hand-labeled 25-item search-triage study with pinned rubric versions and a drift baseline; reports 88% relevance and 96% credibility with all four misses decomposed.
- [jev-search-rerank-eval](https://github.com/zhuyansen/jev-search-rerank-eval) - Chinese/English retrieval evaluation comparing Jev reranking with lexical, embedding, and fusion baselines, including judge-circularity analysis.
- [jev-trust](https://github.com/chunxiaoxx/nautilus-compass/tree/main/sdks/jev-trust) - Python middleware around the Jev API that logs every typed decision, measures calibration in your own domain from outcomes you record (accuracy, Brier, top-label ECE), annotates each answer with its measured effective confidence, and signs the evidence (ed25519) for independent recomputation.
- [Jevals.com](https://jevals.com/) - Independent benchmark that grades hosted Jev and six LLMs against human labels on the same Noul, Choice and Score questions (PubMedQA, Banking77, HelpSteer2), with per-decision logs in [jevals-data](https://github.com/Jevals/jevals-data).
- [jevcal](https://github.com/abhixhek/jevcal) - Fits and drift-checks confidence thresholds against labeled data.
- [Jev Capability Atlas](https://github.com/Zaious/jev-capability-atlas) - Bilingual evidence map with recorded API runs and reusable suites that separates its own tests, third-party benchmarks, and editorial synthesis.
- [typesafe-ai-benchmark](https://github.com/iammrduncan/typesafe-ai-benchmark) - LLM gateway that mimics the System One output shape for comparison work.
- [When a Judgment Layer's Self-Reported Fields Lie](https://doi.org/10.5281/zenodo.22901853) - Independent measurement of Jev's typed decisions as one of three judgment layers compared on a common item set, with a reproduction artifact and a 59-check verification suite; reports Jev's verdict vocabulary collapsing to three reachable values and a truncation flag that does not track the clamp actually in force.

## Guides and cookbooks

- [Augustus](https://github.com/24601/Augustus) - Independent agent skill for finding, building, evaluating, and improving decision-model systems through composition rules, evaluation harnesses, and bounded prompt/program optimization; TypeSafe Jev is the default hosted exemplar.
- [Building with Jev](https://github.com/dbreunig/building-with-jev-skill) - Community agent skill covering question design, state preparation, confidence thresholds, and debugging decisions.
- [Classifying RAG passages](https://docs.typesafe.ai/cookbooks/classifying_rag_passages) - Official example of judging retrieved passages before passing them to an answering model.
- [Date extraction](https://docs.typesafe.ai/cookbooks/date_extraction_cookbook) - Official pattern separating typed extraction from date validation and arithmetic in code.
- [Double-checking citations](https://docs.typesafe.ai/cookbooks/citation_check) - Official example of checking whether source context supports a claim.
- [Gating agent tool calls](https://openrouter.ai/docs/cookbook/building-agents/gate-tool-calls-with-jev) - OpenRouter recipe combining deterministic checks with Jev Noul probabilities and fixed approve, block, or human-review thresholds.
- [Jev by Example](https://github.com/ReallyArtificial/jev-by-example) - Ten runnable JavaScript lessons where Jev judges memory relationships, task evidence, and handoff constraints while application code enforces explicit policies; offline fixtures are the default and live calls are opt-in.
- [Jev Cookbook](https://github.com/nexibeo/jev-cookbook) - Community cookbook of 15 runnable recipes where Jev picks categories, tags, dates, duplicates and next browser actions while deterministic code owns thresholds, review bands and every action.
- [Milvus Search with Jev](https://github.com/milvus-io/bootcamp/tree/master/bootcamp/RAG/search_with_jev) - Nine Python notebooks combining Gemini embeddings, Milvus retrieval, and typed Jev decisions for reranking, filtering, search stopping, routing, cache reuse, curation, guardrails, and evaluation.
- [Parallel questions](https://docs.typesafe.ai/cookbooks/parallel_questions) - Official worked example of evaluating many questions over shared state in one request.
- [Skill suggestion](https://docs.typesafe.ai/cookbooks/skill_suggestion) - Official two-stage workflow that selects a skill and can reject the shortlist.
- [Verified cascade](https://openrouter.ai/docs/cookbook/evaluate-and-optimize/jev-verified-cascade) - OpenRouter example that checks a cheaper draft against grounding constraints with Jev before accepting it or escalating to a stronger model.

## Related lists

- [awesome-jev-by-typesafe](https://github.com/Anil-matcha/awesome-jev-by-typesafe) - Evidence-backed use cases, patterns, prompts, and starter code.
- [awesome-jev](https://github.com/hellogumbo/awesome-jev) - Large community directory with a searchable companion site.
- [yibie/awesome-jev](https://github.com/yibie/awesome-jev) - High-signal field guide organized by decision domain.
- [awesome-open-system-one](https://github.com/rupeshpoojary9/awesome-open-system-one) - Open-only focus: open models and reproductions, independent benchmarks, and the calibration and constrained-decoding tooling behind typed decisions.
- [awesome-typesafe](https://github.com/AbdelStark/awesome-typesafe) - Broader TypeSafe and System One ecosystem list.
- [OmniJev/awesome-jev](https://github.com/OmniJev/awesome-jev) - Papers, open reproductions, independent evaluations, and technical lineage.
- [awesome-jev-typesafe](https://github.com/valentynkit/awesome-jev-typesafe) - CC0, awesome-lint clean, sorted by what you would install, with a short know-before-you-build section on the limits.
- [MrJev/awesome-jev](https://github.com/MrJev/awesome-jev) - Selective list with a 10-star bar and hands-on reviews of each tool at mrjev.com.
- [Made with Jev](https://madewithjev.com) - Use-case directory of Jev builds, guides, and posts, with the cost and speed each author reported, plus free Jev-powered tools.
- [jev-in-the-wild](https://github.com/Jessie-QingYu/jev-in-the-wild) - Index covering Reddit, Hacker News and YouTube alongside GitHub, with a dedicated section for limits and failed results. Data is JSON with a schema; the README is generated from it.

## Contributing

Built something with Jev? Read [CONTRIBUTING.md](CONTRIBUTING.md) and open a pull request. Small projects are welcome when the source clearly shows a concrete Jev decision loop.

**License:** [CC0 1.0 Universal](LICENSE). Linked projects keep their own licenses.

## Acknowledgements

Discovery used public GitHub search, TypeSafe and provider documentation, and the related community lists above. Descriptions added in this refresh were checked against pinned project READMEs and relevant source files; the latest research notes record those sources, and the [September 19 notes](research/2026-09-19.md) preserve the preceding review. Inclusion is not an endorsement by TypeSafe AI or a claim of production readiness.

