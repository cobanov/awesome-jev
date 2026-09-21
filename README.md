# Awesome Jev [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

A curated list of applications, libraries, tools, and resources for [Jev](https://docs.typesafe.ai/introduction), TypeSafe's flagship [System One](https://docs.typesafe.ai/concepts/system-one) model.

**[English](README.md)** | **[简体中文](README_zh.md)**

> Send state and typed questions; get structured answers your code can use directly.

Jev launched in early access on 15 September 2026. This list is unofficial and not affiliated with [TypeSafe AI](https://typesafe.ai). Pull requests are welcome — the ecosystem is young and growing fast.

## Contents

- [What is Jev?](#what-is-jev)
- [Official](#official)
- [Community](#community)
- [SDKs & Clients](#sdks--clients)
- [Applications](#applications)
- [Demos & Games](#demos--games)
- [Agent Tools](#agent-tools)
- [Research & Open Models](#research--open-models)
- [Cookbooks](#cookbooks)
- [Patterns](#patterns)
- [Articles](#articles)
- [Contribute](#contribute)

## What is Jev?

Large language models generate text. Jev does not. It evaluates typed *questions* against a *state* and returns values your code can branch on, sort by, and route with — plus calibrated probabilities and confidence.

| Question | Goal | Returns |
| --- | --- | --- |
| [Choice](https://docs.typesafe.ai/primitives/choice) | Pick one option from a list | `choice`, `probabilities`, `confidence` |
| [Score](https://docs.typesafe.ai/primitives/score) | Rate the state on a rubric | `score`, `probabilities`, `confidence` |
| [Noul](https://docs.typesafe.ai/primitives/noul) | Is this statement true? | `noul` (0–1) |

Questions in one request run in parallel against the same state. Atomic questions, composed in code.

## Official

- [TypeSafe](https://typesafe.ai) - Company homepage, waitlist, and product overview.
- [Documentation](https://docs.typesafe.ai/introduction) - Introduction, primitives, patterns, API, and SDKs. Start with the [quick start](https://docs.typesafe.ai/introduction/quickstart).
- [Playground](https://console.typesafe.ai/playground) - Paste a state, add questions, see typed answers in the browser.
- [API keys](https://console.typesafe.ai/settings/keys) - Dashboard for TypeSafe API keys (`TYPESAFE_API_KEY`).
- [HTTP API](https://docs.typesafe.ai/api) - `POST https://api.typesafe.ai/v1/systemone`.
- [Workflow evals](https://evals.typesafe.ai) - Published eval methodology and per-model results.
- [GitHub org](https://github.com/typesafe-ai) - Official open-source repositories.
- [Agent skill](https://docs.typesafe.ai/agent-skill) - Drop-in skill for Claude Code, Codex, and other coding agents ([`typesafe-ai/skills`](https://github.com/typesafe-ai/skills)).
- [Jev 1.13 jaggedness](https://docs.typesafe.ai/model-jaggedness/jev-1.13) - Known failure modes of the current public model.
- [Introducing System One Models and Jev](https://typesafe.ai/blog/introducing-system-one-models-and-jev) - Launch post: architecture, pricing, Doom and Wikiracing demos, FAQ.
- [Jev on Vercel AI Gateway](https://vercel.com/ai-gateway/models/jev) - Hosted `typesafe-ai/jev` for AI SDK `evaluate`, no TypeSafe waitlist required.
- [Manifesto](https://typesafe.ai/manifesto) - Case for machine-native intelligence built for software, not conversation.
- [The Bitterest Lesson](https://typesafe.ai/blog/bitterest-lesson) - Why optimizing the wrong task can dominate gains from scale.
- [AI: too good to be true, too bad to be useful](https://typesafe.ai/blog/ai-too-good-to-be-true-too-bad-to-be-useful-typesafe-ai) - Argument against preference-optimized chat models for automation.

## Community

- [Discord](https://discord.gg/typesafe) - Official TypeSafe server. Builder demos live in [Show and Tell](https://discord.com/channels/1483217544214085663/1483217545040232493).
- [X @typesafeai](https://x.com/typesafeai) - Product and research updates.
- [LinkedIn](https://www.linkedin.com/company/typesafe-ai/) - Company announcements and hiring.

## SDKs & Clients

Official first, then community clients. Community packages are not affiliated with TypeSafe unless noted.

- [Python SDK](https://github.com/typesafe-ai/typesafe-sdk-python) - Official client. `pip install typesafe-sdk`. Docs: [Python SDK](https://docs.typesafe.ai/sdk/python).
- [JavaScript / TypeScript SDK](https://github.com/typesafe-ai/typesafe-sdk-js) - Official client. `npm install @typesafe-ai/sdk`. Docs: [JavaScript SDK](https://docs.typesafe.ai/sdk/javascript).
- [System One adapter (Python)](https://github.com/typesafe-ai/system-one-adapter-python) - Official drop-in `TypeSafeClient` replacement backed by LLM APIs, for comparing Jev against chat models on the same questions. `pip install system-one-adapter`.
- [Vercel AI SDK provider](https://ai-sdk.dev/providers/ai-sdk-providers/typesafe-ai) - `@ai-sdk/typesafe-ai` plus `experimental_evaluate`. Use `typeSafeAi.evaluationModel('jev-latest')` or the Gateway id `typesafe-ai/jev`.
- [Elixir SDK](https://github.com/nshkrdotcom/typesafe_sdk) - Community Hex package [`typesafe_sdk`](https://hex.pm/packages/typesafe_sdk) for `system_one` and model listing. Docs: [HexDocs](https://hexdocs.pm/typesafe_sdk).
- [Jev (Elixir OTP)](https://github.com/dannote/jev) - Hex package [`jev`](https://hex.pm/packages/jev): Jev as a peer GenServer; answers arrive as messages you pattern-match, with network-free tests
- [Ruby SDK](https://github.com/joshmn/typesafe-sdk) - Community Ruby 3.1+ client: Noul / Choice / Score, retries, model listing, thread-safe pooled HTTP. No async client.
- [RubyLLM TypeSafe](https://github.com/kieranklaassen/ruby_llm-typesafe) - TypeSafe provider for RubyLLM 2 with offline model metadata and typed responses.
- [typesafe-ai-rails](https://github.com/GenieRobot/typesafe-ai-rails) - Rails integration on top of the official Python SDK: config, usage/cost telemetry, opt-in confidence policies.
- [Rust SDK (typesafe-ai-rs)](https://github.com/gilljon/typesafe-ai-rs) - Independent async and blocking client for System One.
- [TypeSafe AI for Rust](https://github.com/Twister915/typesafe-ai) - Another Rust client: async + blocking transports, typed responses, observable retries.
- [typesafe-rs](https://github.com/AbdelStark/typesafe-rs) - Latency-focused Rust transport SDK aiming for behavioral parity with the official clients.
- [s1-rs](https://github.com/AbdelStark/s1-rs) - Rust derive layer for Choice / Score / Noul, typed question sets, confidence gates, and network-free tests.
- [Advocaat](https://github.com/pithings/advocaat) - Small TypeScript client with tagged helpers for chances, choices, and scores.
- [Scala / ZIO SDK](https://github.com/jamesward/zio-typesafe-ai) - Community ZIO client with a small DSL for noul / choice / score.
- [.NET SDK](https://github.com/saibimajdi/typesafe-dotnet-sdk) - Community client for typed questions and confidence-scored answers.
- [PHP SDK](https://github.com/Butochnikov/typesafe-sdk-php) - Unofficial PHP client: typed DTOs, promises, and exceptions. Used by the Laravel package below.
- [Laravel TypeSafe Jev](https://github.com/Butochnikov/laravel-typesafe-jev) - Unofficial Laravel 12/13 integration: config, facade, scoped DI, and a recording fake on the PHP SDK.
- [jev-go](https://github.com/Gaurav-Gosain/jev-go) - Unofficial Go client for typed judgments and calibrated probabilities. `go get github.com/Gaurav-Gosain/jev-go`.
- [Stumble/jev-go](https://github.com/Stumble/jev-go) - Unofficial dependency-free Go SDK for TypeSafe direct and Vercel AI Gateway, with typed questions, retries, an interactive CLI, and an installable agent skill
- [jevclient](https://github.com/AboveColin/jevclient) - Unofficial async Python client (`pip install jevclient`). Typed Noul / Choice / Score helpers, separate from the official `typesafe-sdk`.
- [LlamaIndex Jev](https://github.com/WiktorB2004/llama-index-jev) - Unofficial LlamaIndex reranker (`JevRerank`) and router (`JevSingleSelector` / `JevMultiSelector`) on the official Python SDK
- [Swift SDK](https://github.com/ainame/swift-typesafe) - Unofficial Swift 6.4 client aligned with the Python SDK 0.6.0 API, including Linux
- [TypeSafe AI Swift SDK](https://github.com/alterhq/typesafe-sdk-swift) - Unofficial dependency-free Swift 6 client for Choice / Score / Noul, with strict concurrency, configurable authentication and retries, and network-free tests

## Applications

Open-source products and demos that put Jev in a real loop.

- [Jev Ultrafast](https://github.com/browser-use/jev-ultrafast) - Browser agent from [Browser Use](https://github.com/browser-use). Jev picks an operation and a DOM element in one request; a small LLM writes text only for `TYPE_TEXT`. Zürich → London on Google Flights in ~7s. Library, local inspector, and measurements included.
- [Jev Web Analyzer](https://github.com/replynodes/jev-web-analyzer) - Community project that analyzes a public SaaS landing page as clean Markdown and asks Jev ten bounded `Choice` questions about first-visit understanding, including the first change to make.
- [JevBrowserExt](https://github.com/chy4pro/JevBrowserExt) - Chrome extension (Manifest V3) port of Jev Ultrafast: Jev picks the operation and DOM element in one request, a small text model writes typed values, and it runs in the user's own tabs through OpenRouter, TypeSafe or Cloudflare; includes a 17-task headless-Chromium suite with recorded traces.
- [jev-align (Sutro)](https://github.com/sutro-sh/jev-align) - Unofficial active-learning CLI that evaluates CSV, Parquet, and JSONL rows with Jev, asks people to label uncertain and audit samples, and uses GEPA to propose improved definitions
- [Jev for Chrome](https://github.com/chy4pro/jev-for-chrome) - Unofficial Chrome extension (Manifest V3) port of Jev Ultrafast: Jev picks the operation and DOM element in one request, a small text model writes typed values, and it runs in the user's own tabs through OpenRouter, TypeSafe or Cloudflare; includes a 17-task headless-Chromium suite with recorded traces.
- [jev-ego](https://github.com/romaluev/jev-ego) - Browser agent on [ego lite](https://lite.ego.app/): one TypeSafe request picks operation + indexed element; agent-facing observe/act/suggest/step CLI
- [jev-browser](https://github.com/Ying-Kai-Liao/jev-browser) - Unofficial browser automation: an LLM plans the outcome, Jev decides each click/type on a Playwright snapshot (~300 ms/call). Ships as a library, CLI, and MCP server (`npx -y -p jev-browser jev-browser-mcp`).
- [typesafe-computer-use](https://github.com/awlevin/typesafe-computer-use) - macOS computer-use loop: OCR the screen, Jev classifies the next action, then click. About $0.0002/step.
- [Yappy](https://yappy.biz/jev/) - macOS voice agent (closed source, public write-up with measurements). On its hosted plan Jev picks the operation and target control from the window's accessibility table each step; a chat model writes text only for typing, and the full agent takes over when confidence drops. Author-reported: 275–690 ms per decision, $0.003 for five.
- [Mobile Jev](https://github.com/droidrun/mobile-jev) - Android agent on [Mobilerun](https://mobilerun.ai): Jev decides each tap. Opens Uber, SFO → Golden Gate, payment screen in ~21s / 9 actions. Live studio, CLI, and traces. No ADB.
- [Unclutter](https://github.com/kitze/unclutter) - Chrome / Firefox extension: Jev classifies nonessential page elements; local template rules hide them on later visits.
- [TypeSafe AdBlock](https://github.com/realZachi/typesafe-adblock) - Chrome extension: Jev judges whether a DOM element is an ad and removes it. BYOK, no backend. Author calls it a demo, not a real ad blocker
- [HA-Jev](https://github.com/AboveColin/HA-Jev) - Unofficial Home Assistant integration: typed questions about entity state become sensors and automation actions, with a target picker that builds the state from the user's own entities and usage, cost, and daily-budget entities alongside the answers
- [Every](https://github.com/sufianetaouil/every) - Semantic code-search CLI: a yes/no question against every function, ranked by Noul probability.
- [blink](https://github.com/ellipsis-dev/blink) - Codebase search: an ensemble of walkers asks Jev which file answers a natural-language query
- [Jev Search](https://github.com/superagents-lab/jev-search) - Unofficial web search app using Jev's Choice and Noul judgments to select sources, time ranges, and query candidates, then rank results retrieved through Search1API
- [Jev Reranker (Rust CLI)](https://github.com/shinpr/jev-reranker) - Unofficial JSON-in/JSON-out CLI that uses Jev `Noul` judgments to rerank search results, filter documents without usable evidence, or extract query-specific passages
- [neo4jev](https://github.com/jexp/neo4jev) - Neo4j graph navigation: at each node Jev chooses which relationship to follow, with beam search over log-probabilities
- [hono-jev-router](https://github.com/yusukebe/hono-jev-router) - Experimental Hono router: Jev matches an incoming request to a plain-language route description
- [sqlite3-jev](https://github.com/mattn/sqlite3-jev) - SQLite C extension: `jev_noul` / `jev_choice` / `jev_score` as SQL functions via libcurl
- [jevql](https://github.com/kylemclaren/jevql) - Unofficial psql-shaped CLI and Go/TypeScript/Python SDKs for vanilla Postgres: `jev()` / `jev_prob` / `jev_choice` / `jev_score` in plain SQL with no extension, the SQL runs on the server and Jev judges the surviving rows in batches
- [jev-resilience](https://github.com/Vicente-MD/jev-resilience) - Unofficial Spring WebFlux starter: a semantic circuit breaker that uses Jev to catch silent HTTP 200 failures
- [tripwire](https://github.com/noelzappy/tripwire) - Unofficial AI SDK middleware and OpenAI-compatible proxy: seven Jev checks on every LLM response in ~100 ms, confidence-gated
- [ProgressGate](https://github.com/AshutoshVJTI/progressgate) - Detects semantic stagnation in agent loops: Jev judges the trajectory; code returns CONTINUE / WARN / REPLAN / HALT
- [jev-harness](https://github.com/AntonioCoppe/jev-harness) - Unofficial production layer around Jev: policy, confidence gate, shadow mode, recipes, and an eval CLI
- [jev-tree](https://github.com/reachjalil/jev-tree) - Recursive Choice over a taxonomy so catalogs larger than Jev's 255-option cap still fit
- [jev-shell-history](https://github.com/mrnugget/jev-shell-history) - Fish-style zsh autosuggestions: Jev ranks recent history as you type
- [Supercov](https://github.com/supercorp-ai/supercov) - Code quality and test coverage for coding agents: Jev scores each source file so the agent knows what to fix first
- [Jev Review](https://github.com/devagrawal09/jev-review) - Staged code-review workflow and local dashboard driven by focused Jev calls.
- [Foreman](https://github.com/thruwire/foreman) - Software-factory loop: Codex implements; Jev independently judges completeness, tests, and whether a human is needed.
- [Jev Drone](https://github.com/RomanSlack/jev-drone) - MuJoCo quadrotor: control and safety stay in code; Jev handles slower tactical judgments.
- [Jev Plays StarCraft](https://github.com/phyous/tsai-sc) - Structured-state harness for the original StarCraft shareware campaign, with verified run and probability traces.
- [Jev × Civilization II](https://github.com/phyous/tsai-civ2) - Original Civ II in a browser; Jev chooses empire, city, research, and unit actions. Experimental; no verified win yet
- [Jev Trade](https://github.com/aowang-ai/jev-trade) - Live Hyperliquid desk: each tick Jev answers Choice questions for long/short, open/close/hold, and leverage; code places or pulls the quote. Dry-run by default; a live key sends real orders. Demo: [jev-trade.com](https://www.jev-trade.com/).
- [Jev Trader](https://github.com/jarrodwatts/jev-trader) - One buy/sell decision per Monad block on Kuru's MON-USDC book. Live demo: [jev-trader.vercel.app](https://jev-trader.vercel.app/).
- [Human Compiler](https://github.com/asfarsadewa/human-compiler) - Paste corporate prose; Jev scores passive-aggression, urgency, and information density, then code emits rustc-style diagnostics. Live: [human-compiler.asfarlab.fun](https://human-compiler.asfarlab.fun).
- [JEVMETER](https://github.com/ChetasLua/jevmeter) - Live Jev meter on any video: every sentence scored, rendered as a 16:9 edit. Demo: [Chetaslua](https://x.com/chetaslua/status/2100473581251748216).
- [jev-audio-beeper](https://github.com/santos-sanz/jev-audio-beeper) - Low-latency audio insult detector: Jev decides, ffmpeg beeps in ~466 ms without rewriting the rest of the track.
- [jev-askable-arm](https://github.com/TarunTomar122/jev-askable-arm) - Zero-shot English goals on a simulated Franka. Jev chains hardcoded primitives.
- [jev-codex-router](https://github.com/0xNatoshi/jev-codex-router) - Per-turn Codex routing: Jev picks model, thinking depth, and speed mode.
- [jev-router](https://github.com/gargpratyush/jev-router) - Per-turn routing for Claude Code and Codex: Jev sends simple work to the fast tier and hard work to the strong tier. `npm i -g jev-router`.
- [jev-secret-detection](https://github.com/teyhouse/jev-secret-detection) - Secret-in-diff detector with repeatable Jev verdicts.
- [commit-miner](https://github.com/devanshbatham/commit-miner) - Rust CLI that classifies commit diffs with Jev: bug fixes, security/CWEs, and change types. HTML/CSV reports.
- [jev-eval-agent](https://github.com/vinilana/jev-eval-agent) - Public eval harness for early Jev tests.
- [Jev Logs](https://github.com/reachjalil/jevlogs) - OpenTelemetry log triage: Jev scores diagnostic value and priority before an expensive LLM looks at the archive.
- [Smart home assistant demo](https://docs.typesafe.ai/demos/smart-home) - Official interactive demo of [speculative fan-out](https://docs.typesafe.ai/patterns/fan-out): many questions in one call, code keeps the relevant answers, LLM only for splits and chit-chat. Source is slated for GitHub at release.
- [jev.nvim](https://github.com/valentynkit/jev.nvim) - Neovim plugin that splits the buffer into functions with Treesitter, scores each against a plain-language question with Jev, and ranks answers by probability in the quickfix window.
- [jev-skip](https://github.com/valentynkit/jev-skip) - Browser extension that reads the YouTube caption track and paints a per-segment sponsor probability on the seek bar before the intro ends, with no crowd database, reporting catching 77% of SponsorBlock's sponsor seconds across 23 videos at $0.0008 a video.

## Demos & Games

Toys, live sites, and realtime agents. Most shipped in the first 48 hours after launch.

- [Yes / No](https://yesno.coderai.dev) - Free no-signup Noul demo. Ask a question, get yes / no / maybe, with web search when needed.
- [Jev Tetris](https://jev-omega.vercel.app) - Jev picks rotation and column from holes, stack height, and bumpiness.
- [Jev Pac-Man](https://jev-pacman.ephraimduncan.com) - Maze as JSON; Jev picks the turn at each junction in realtime.
- [typesafe-mario](https://github.com/fhshaik/typesafe-mario) - Super Mario Bros. from structured emulator state.
- [jev-doom-agent](https://github.com/lukaske/jev-doom-agent) - Browser-native Doom with Chocolate Doom WASM, spatial state, and live decision telemetry.
- [jev-gomoku](https://github.com/mizchi/jev-gomoku) - MoonBit client plus Jev-vs-Jev gomoku; write-up: [jev 同士に五目並べで対戦させた](https://zenn.dev/mizchi/articles/jev-plays-gomoku).
- [jev-t-rex-runner](https://github.com/joshlarsen/jev-t-rex-runner) - Chrome dinosaur game played by Jev.
- [snake-jev](https://github.com/siroccomask/snake-jev) - Snake: hundreds of typed direction decisions per run.
- [Jev Guard](https://guard-jev.vercel.app) - Comment-moderation playground.
- [jev-fit](https://jev-fit.com) - Paste a software idea; Jev answers a fixed typed rubric in one call and the page says plain code, Jev, or a reasoning LLM, with probabilities. Unofficial, closed source, free page and API.
- [Hollow Creek](https://hollow-creek-sigma.vercel.app) - Village NPCs that *judge* you each tick (what to do, how they feel) instead of chatting.
- [Jev mood demo](https://jev-demo.vercel.app) - Talk nicely or nastily over time; structured state tracks mood.
- [Jev Room](https://jev-room.moe136231.chatgpt.site) - One sentence → six room settings. Jev chooses, the app renders.
- [TypeSafe Typewriter](https://typesafe-demo.val.run/) - Live Val Town demo: 16 typed judgments update as you type. Launch post: [Steve Krouse](https://x.com/stevekrouse/status/2100287368221659289).
- [got-jev](https://github.com/phureewat29/got-jev) - Game of Thrones roleplay as Jon Snow. A story model writes the scene; Jev answers where he is, how much danger, and what should play under it.
- [Little Airways](https://github.com/lbotinelly/jev-little-airways) - Toy archipelago ATC: Jev judges divert / emergency / who lands first from each plane's local state, ~150 ms.
- [jev-plays-pokemon-red](https://github.com/valentynkit/jev-plays-pokemon-red) - Pokemon Red on PyBoy where deterministic code owns the route and arithmetic and Jev picks only at branches, with every battle turn's faint prediction scored by Brier against the emulator's RAM state.
- [jev-canvas](https://github.com/gaborishka/jev-canvas) - Draw on a tldraw canvas with your voice and a webcam-tracked finger; Jev decides action, target and place on every partial transcript. English and Ukrainian commands.
- [sudoku-vs-jev](https://github.com/zebedelu/sudoku-vs-jev) - Terminal Sudoku where Python owns the rules and Jev picks one move per turn, steady while forced moves exist and shaky once it has to guess.
- [chess-vs-jev](https://github.com/zebedelu/chess-vs-jev) - Pygame chess where python-chess owns the rules and Jev picks one legal move per turn, playable Human vs Human, Human vs Jev, or Jev vs Jev.
- [JevsBistro](https://github.com/andrewsilber/JevsBistro) - Deterministic 3D restaurant sim that replays the same dinner service to compare rule-based, camera-assisted, and Jev-planned waiters, logging each decision's state, options, confidence, and latency.
- [jev-asks-until-sure](https://github.com/mintannn/jev-asks-until-sure) - Twenty questions where confidence sets the stopping rule: Jev commits, hedges, or refuses to guess, and the UI narrates every judgment. Live: [jev.mintan.org](https://jev.mintan.org).
- [Jev × 2048](https://jev-2048-ultra.vercel.app) - A web lab where Jev is the 2048 decision engine, showing each move's probability distribution, confidence, latency, and token cost so you can watch how context design shapes the decision model.

## Agent Tools

Tools that expose Jev to coding agents and MCP clients.

- [TypeSafe agent skill](https://github.com/typesafe-ai/skills) - Official skill: primitives, patterns, and how to structure evaluations. Claude Code: `claude plugin marketplace add typesafe-ai/skills` then `claude plugin install typesafe@typesafe-ai`. Other agents: `npx skills add typesafe-ai/skills --skill typesafe-ai`.
- [fast-jev-compaction](https://github.com/tamaratran/fast-jev-compaction) - Claude Code plugin and npm library: Jev scores tool calls and drops stale ones instead of summarizing context
- [SkillRanker](https://github.com/Dicklesworthstone/skillranker) - Rust CLI: Jev ranks which agent skill fits the next step from live session context, with Claude Code hooks
- [Jevbridge](https://github.com/gamesonrblx/Jevbridge) - Unofficial ACP/MCP adapter: typed Jev decisions and computer use beside Codex, Claude, Grok, and OpenCode
- [eve](https://github.com/vercel/eve) - Vercel's agent framework. Experimental `autoModel` defaults to Gateway `typesafe-ai/jev` to pick a language model from an allowlist.
- [jev-mcp](https://github.com/jkudish/jev-mcp) - Node MCP wrapping three cookbook patterns: `jev_verify` (citation check), `jev_screen` (prompt-injection / guardrails), `jev_find` (semantic ranking without embeddings). `npx -y github:jkudish/jev-mcp`.
- [Jev MCP (Python)](https://github.com/blakestone-x/jev-mcp) - Python MCP server: classify, score, check, match, and screen tools.
- [Jev Review MCP](https://github.com/NiazMorshed2007/jev-review) - Local-first MCP: Claude Code, Codex, Cursor, and OpenCode get structured quality review from Jev while they write. Not the same project as [Jev Review](#applications) above.
- [typesafe-mcp](https://github.com/itsmostafa/typesafe-mcp) - Go CLI and single-binary MCP for Claude Desktop, Claude Code, and Codex.
- [pi-typesafe](https://github.com/DevMortimer/pi-typesafe) - Pi extension: one consented, key-managed TypeSafe client, batched `typesafe_evaluate`, offline-testable transport.
- [pi-jev](https://github.com/y0usaf/pi-jev) - Pi extension with a shadow-mode tool-call gate, output judge, and typed `jev_ask`.
- [pi-warden](https://github.com/DevMortimer/pi-warden) - Pi guardrails on pi-typesafe: held tool results instead of a dialog; write checks against a project rules file.
- [pi-jev-auto-mode](https://github.com/jomatsu/pi-jev-auto-mode) - Pi auto mode: Jev semantically approves `bash` / `write` / `edit`, and fails closed when it cannot decide.
- [Bicameral](https://github.com/AbdelStark/bicameral) - Pi coding harness: LLM writes, Jev supplies typed reflexes for policy, loop detection, and review. Explicitly not a sandbox.
- [jev-pref](https://github.com/doeixd/jev-pref) - Turn AGENTS.md preferences into a Jev-powered AI linter: project-specific semantic review rules in `jev-pref.json`, checked against hunks, staged files, or PRs, with findings fed back to your coding agent. `npx jev-pref setup`.
- [ask-jev-skill](https://github.com/shantanugoel/ask-jev-skill) - Hermes skill: ask Jev whenever the agent needs a bounded decision.
- [jev-system-architect](https://github.com/samtay32/jev-system-architect) - Skill that hunts for brittle semantic logic and turns it into Choice / Score / Noul boundaries.
- [augustus](https://github.com/24601/Augustus) - Design-judgment skill: maps Choice/Score/Noul onto classical methods (decision theory, rerank, routing) with a composition algebra, question-design diagnosis, and falsifying validation gates
- [jev-browser MCP](https://github.com/Ying-Kai-Liao/jev-browser) - Same project as above; MCP tools `browser_do`, `browser_check`, `browser_choose` so an agent can drive the page without reading full snapshots.
- [jev-ego](https://github.com/romaluev/jev-ego) - Same project; observe/act/suggest/step on a live ego lite TaskSpace
- [jev-axi](https://github.com/shiftynick/jev-axi) - CLI plus Claude Code and Codex hooks: Jev scores each shell command for hazards before it runs and screens fetched text for prompt injection, with routine commands decided locally so nothing is sent
- [jev-engineering](https://github.com/eugeniughelbur/jev-engineering) - Decision layer for coding agents: deterministic rules before any model call, then one Jev request, as a Claude Code hook, an MCP server, a loopback service and a shared team policy. Ships the 300-call injection test behind its own numbers.
- [jev-belay](https://github.com/valentynkit/jev-belay) - Claude Code Stop hook that checks the transcript for evidence before trusting a "done" claim, spending one four-question Jev call only when files changed with no passing check since, and failing open on every error path.
- [jev-commit](https://github.com/valentynkit/jev-commit) - Pre-commit hook where one Jev call judges whether the commit message matches the staged diff, flags debug leftovers and unmentioned work, and blocks only when it detects a credential.
- [jev-use](https://github.com/shitianfang/jev-use) - Claude Code, Codex and pi plugin: Jev answers the batched typed questions an agent loop needs, and a typed escalation contract hands writing and low-confidence steps back to the LLM
- [dsh-jev-tools](https://github.com/HorusJiang/dsh-jev-tools) - DeepSeek Harness plugin: Jev prunes oversized tool output, screens fetched pages for injected instructions, and picks which skill fits the next step, plus the jev_ask and jev_gate tools
- [slop-grader](https://github.com/lukstei/slop-grader) - Rule-based CLI and agent skill that grades text against custom rulesets for AI slop, grammar, and technical documentation quality, and guides an AI agent to auto-fix violations
- [jgrep (kyu1204)](https://github.com/kyu1204/jgrep) - Semantic grep for code, git diffs and CSV rows: one Noul per 5-60 line chunk, 16 chunks per Jev request, grep-style file:line output and exit codes for CI lint rules written in English

## Research & Open Models

Independent work inspired by Jev's interface. These are not TypeSafe models.

- [jevlike](https://github.com/vinnylarouge/jevlike) - Train a small one-pass scorer that maps context + N text options to a probability per option. Includes Doom / chess vision demos and a Wikispeedia next-click example. Explicitly *not* a reproduction of TypeSafe's architecture or RLCD.
- [openjev](https://github.com/TheoLeeCJ/openjev) - Can we run something Jev-like on a home RTX 3090? Reads option logits instead of generating text. Not TypeSafe's model.
- [PocketJev](https://github.com/NullPo-jp/PocketJev) - On-device iPhone visual decisions with MLX + Qwen3-VL option logits. Camera + 3-choice, no text generation, ~1s, no photo saved.
- [jev-visual](https://github.com/hr98w/jev-visual) - Educational Jev-like visual inference on Apple Silicon: shared multimodal context, candidate scoring, sorting-factory / Breakout / gesture demos. Not TypeSafe's model
- [jevmlx](https://github.com/bnsd55/jevmlx) - Jev-style parallel constrained decisions for any MLX model on Apple Silicon: schema-valid JSON in one forward pass
- [JEVfire](https://github.com/kikoncuo/jevfire) - Jev-inspired parallel decisions for CUDA LLMs via vLLM, with a browser Mario demo (~71 ms/action locally)
- [decider](https://github.com/Mapika/decider) - Qwen3.5-2B fine-tune that emits typed decisions with calibrated probabilities in one pass. Unofficial; not TypeSafe's architecture.
- [LitJev](https://github.com/zhengxuyu/litjev) - A reproduction of Jev that turns any Qwen model into a fast decision model, serving the same `/v1/systemone` schema (Choice, Score, Noul) with no training and no generated answer text. Unofficial; not TypeSafe's model.
- [PlayJev](https://github.com/OmniJev/PlayJev) - Qwen3.5-0.8B-Base fine-tuned to play ten browser games from 448 px frames: one forward pass per move, a probability over the game's option list read off the option letters, no generated text. Open weights and a demo of all ten in the browser. Unofficial; not TypeSafe's model.
- [typesafe-ai-benchmark](https://github.com/iammrduncan/typesafe-ai-benchmark) - Side-by-side of Jev vs Qwen 3.8 27B on Cerebras for the same System One questions. Video: [Shannon](https://x.com/iamMrDuncan/status/2100467548298899918).
- [Jev Rerank Bench](https://github.com/anessbelbati/jev-rerank-bench) - Reranking comparison with raw provider responses, scoring code, uncertainty intervals, and documented limits.
- [Jev Spam Eval](https://github.com/bitnovus/jev-spam-eval) - Exploratory zero-shot spam study vs trained TF-IDF baselines, with post-hoc-tuning caveats.
- [**Jev × NASA Kepler**](https://gist.github.com/ipaulsmith/e5c3ae3a492a455435d5bfc161404312) - Independent retrospective test of Jev 1.13 on 8,054 historical Kepler Objects of Interest with NASA Exoplanet Archive dispositions hidden during prediction; 72.5% archive-disposition match vs 64.4% for a fixed 3-rule baseline, with exact requests, metrics, baseline, and caveats
- [Jev Phishing Bench](https://github.com/anisselbd/jev-phishing-bench) - 2,000 emails: Jev vs Claude Haiku 4.5 on click-or-not, with calibration, latency, and cost. Haiku wins accuracy here.
- [jev-agent-failure-benchmark](https://github.com/TokenTrim/jev-agent-failure-benchmark) - Who&When Pro (injected agent failures): Jev vs a strong LLM on who / which step / error category.
- [jev-sec-bench](https://github.com/Gaurav-Gosain/jev-sec-bench) - Blind prompt-injection and vulnerable-code detection benches on public corpora, built on jev-go.
- [Jev DSPy Lab](https://github.com/jmanhype/jev-dspy-lab) - Unofficial DSPy companion that records and replays TypeSafe calls while measuring calibration, selective risk, confidence-gated abstention, latency, tokens, and modeled cost.
- [jevcal](https://github.com/abhixhek/jevcal) - Unofficial CLI that fits a per-question confidence threshold to a target accuracy on your own labeled data, verifies it on a held-out split, shows how much traffic still needs an LLM fallback, and fails CI when a Jev update breaks the locked thresholds
- [ASSAY-001](https://github.com/jourdanlabs/assay-001) - Independent pre-registered check of Jev calibration and type safety on Banking77 / CLINC150. Split verdict, full logs. Write-up: [donttrustme.ai](https://donttrustme.ai/assay-001.html)
- [Jev search rerank eval](https://github.com/zhuyansen/jev-search-rerank-eval) - 9,831 labelled pairs: Jev rerank vs BM25 / bge-m3, with judge-circularity measured. Fusion wins; Jev alone does not beat embeddings
- [Smoking-history extraction benchmark](https://github.com/vclic/smoking-extraction-benchmark) - 1,000 synthetic notes: Jev vs OpenAI structured outputs on accuracy, cost, and latency

## Cookbooks

Official, copy-pasteable workflows. Full index: [console cookbooks](https://console.typesafe.ai/docs/cookbooks) and [docs index](https://docs.typesafe.ai/llms.txt).

- [Parallel questions](https://docs.typesafe.ai/cookbooks/parallel_questions) - Batch many questions over one state; one call instead of N.
- [Line-by-line search](https://docs.typesafe.ai/cookbooks/semantic_find) - Score hundreds of line ids against a query with Choice + a Noul “does an answer exist?” check.
- [Re-ranking](https://docs.typesafe.ai/cookbooks/rerank_typesafe) - BM25 shortlist, then one TypeSafe question per query–candidate pair.
- [Guardrails for LLMs](https://docs.typesafe.ai/cookbooks/llm_guardrails) - Screen messages in and out of an LLM; threshold probabilities in code.
- [Double-checking citations](https://docs.typesafe.ai/cookbooks/citation_check) - Choice over whether a quote’s context supports the claim; confidence gates human review.
- [Classifying RAG passages](https://docs.typesafe.ai/cookbooks/classifying_rag_passages) - Keep, flag, or drop retrieved passages (contradiction, prompt injection) before the answering model.
- [Function calling](https://docs.typesafe.ai/cookbooks/function_calling) - Map natural-language requests onto ordinary typed functions with closed-set arguments.
- [Skill suggestion](https://docs.typesafe.ai/cookbooks/skill_suggestion) - Rank an agent skill catalog, then read only the top few.
- [Hierarchical classification](https://docs.typesafe.ai/cookbooks/hierarchical_classification) - Beam search over deep taxonomies with Choice probabilities.
- [SDE cascade](https://docs.typesafe.ai/cookbooks/sde_cascade) - Two-stage structured-data-extraction cascade (mini → verify → reasoning).
- [Date extraction](https://docs.typesafe.ai/cookbooks/date_extraction_cookbook) - Ask for named date parts, resolve and validate in code.
- [Pre-parsed value extraction](https://docs.typesafe.ai/cookbooks/pre_parsed_value_extraction_cookbook) - Regex candidates, then Jev selects the requested span.
- [Knowledge graph entity alignment](https://docs.typesafe.ai/cookbooks/entity_alignment) - Score merge / leave unlinked / send to a curator.
- [Autoresearch feature discovery](https://docs.typesafe.ai/cookbooks/autoresearch_feature_discovery) - Propose TypeSafe questions as numeric features for a supervised model.
- [Classification using confidence](https://docs.typesafe.ai/cookbooks/classification_using_confidence) - Report a fine label only when confidence is high; otherwise climb the hierarchy.
- [Structure recovery](https://docs.typesafe.ai/cookbooks/autoformat) - Reconstruct Markdown from de-formatted plain text.
- [Self-consistency: nouls](https://docs.typesafe.ai/cookbooks/consistency_noul_cookbook) / [choices](https://docs.typesafe.ai/cookbooks/consistency_choice_cookbook) - Route uncertain probabilities to review without hiding the raw values.

## Patterns

Architectural recipes from the docs.

- [Speculative fan-out](https://docs.typesafe.ai/patterns/fan-out) - Ask many questions, including ones that may not apply; filter in code.
- [Confidence-gated routing](https://docs.typesafe.ai/patterns/confidence-routing) - The answer is *what*; confidence is *whether to act*.
- [Composite scoring](https://docs.typesafe.ai/patterns/composite-scoring) - Atomic scores, weights you own in code.
- [Intent routing](https://docs.typesafe.ai/patterns/intent-routing) - Classify, then hand off to logic, a specialist LLM, or a human.

See also: [How to build with TypeSafe](https://docs.typesafe.ai/concepts/how-to-build-with-system-one), [use-case map](https://docs.typesafe.ai/concepts/use-case-map), [confidence](https://docs.typesafe.ai/confidence).

## Articles

Independent measurements, experiments, and news. Official posts live under [Official](#official).

- [Mini-Vibe Check: TypeSafe's Jev Judged Everything I’ve Written in 0.7 Seconds](https://every.to/also-true-for-humans/mini-vibe-check-typesafe-s-jev-judged-everything-i-ve-written-in-0-7-seconds) - Every's Mike Taylor runs Jev over a writing corpus.
- [TypeSafe AI debuts model for machines that plays Doom](https://www.theregister.com/ai-and-ml/2026/09/16/typesafe-ai-debuts-model-for-machines-that-plays-doom/5296711) - News coverage of the launch.
- [TypeSafeのJevを正しく驚く、それってLLMでできませんか？](https://zenn.dev/nwn/articles/824026c76116e0) - Reproduces the JSON-vs-logit shortcut on Gemma and compares Jev with LLMs on the public Mario harness.
- [jev 同士に五目並べで対戦させた](https://zenn.dev/mizchi/articles/jev-plays-gomoku) - Jev vs Jev gomoku with source and timing logs.
- [Jev: one judge call, or twelve dimension scores? I measured both on three tasks](https://agentjournal.dev/blog/llm-judge-vs-feature-extraction/) - Independent measurement on three classification tasks: one direct Jev question per row against 12–14 Jev-scored dimensions with locally fitted weights, with token costs, confidence intervals, and false-positive rates.
- [Testing Jev on public and private data: classifier or filter?](https://amankumar.ai/blogs/jev-measured) - 16,000 calls vs gpt-5.4-mini and gpt-5.6-luna; where it wins, where it breaks, and a threshold procedure

## Related

- [MrJev/awesome-jev](https://github.com/MrJev/awesome-jev) - Selective list behind a 10-star bar, with hands-on reviews at [mrjev.com](https://mrjev.com/best-jev-tools/) recording what each tool sends and where.
- [typesafe-ai on PyPI](https://pypi.org/project/typesafe-ai/) - Community redirect shim. The real package is `typesafe-sdk`; this name was registered to block slopsquatting. Not affiliated with TypeSafe.

## Contribute

See [CONTRIBUTING.md](CONTRIBUTING.md). In short: open a pull request that adds a project with a link and a one-line description. Useful, interesting, and actually built on Jev (or clearly inspired by its interface).

## License

[CC0 1.0](LICENSE) — this list is dedicated to the public domain.
