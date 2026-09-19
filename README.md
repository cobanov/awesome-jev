# Awesome Jev [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated, source-backed list of projects built with Jev, TypeSafe AI's System One model for fast, typed, probabilistic decisions.

Jev takes program state plus typed questions and returns constrained answers with probabilities. It is designed for software decisions such as classification, routing, scoring, ranking, verification, and guardrails, rather than free-form text generation.

This list favors public source code, concrete Jev usage, clear limitations, and reproducible evidence. The latest review added **52 community projects and resources**, bringing that part of the list to **102**, alongside official resources, provider integrations, and related lists. See the [September 19 research notes](research/2026-09-19.md) for pinned source evidence and review boundaries. Review completed September 19, 2026 (Europe/Istanbul); upstream event dates below are UTC.

## Contents

- [Start here](#start-here)
- [Recent developments](#recent-developments)
- [Official resources](#official-resources)
- [Provider integrations](#provider-integrations)
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
- [Contributing](#contributing)

## Start here

- **System One shape:** text or structured state + typed questions → constrained answers + probabilities → deterministic application code.
- **Question primitives:** `Choice` selects an option, `Score` evaluates ordered rubric levels, and `Noul` returns a number from 0 to 1 representing the probability of "yes". Review or abstention behavior is defined in application code. See the [primitive reference](https://docs.typesafe.ai/primitives).
- **Input boundary:** the hosted Jev model is text-only. Browser, audio, image, and robotics projects supply extracted text or structured observations, or use separate perception models. Independent multimodal reproductions are listed separately.
- **Good fits:** semantic routing, triage, reranking, rubric scoring, moderation, verification, and low-latency decisions inside bounded workflows.
- **Important caveat:** schema-valid output is not the same as a correct decision. Validate on your own data, calibrate thresholds, keep high-impact actions behind deterministic checks, and provide a human fallback.

## Recent developments

- **September 18: Python SDK 0.7.0.** [Release notes](https://github.com/typesafe-ai/typesafe-sdk-python/releases/tag/v0.7.0) document a breaking serialization change from `msgspec` to Pydantic, a new `response_model` argument, and corrected serialization of `str` subclasses.
- **September 18: OpenRouter listing.** [Jev 1.13](https://openrouter.ai/typesafe/jev-1.13) is listed with a September 18 date. This is a provider listing date, not evidence of a separate new upstream model revision.
- **September 16: Vercel AI Gateway integration.** The [announcement](https://vercel.com/changelog/typesafe-ai-jev-now-available-on-ai-gateway) introduces typed evaluation via AI SDK's experimental `evaluate` API.
- **Current model:** [TypeSafe documents](https://docs.typesafe.ai/models) `jev-1.13.0`, with both `jev-latest` and `jev-preview` currently pointing to it. Pin the version when comparing evaluations.
- **Ecosystem refresh:** new sections cover context pruning, browser/device control, media tools, and provider integrations. Entries newly added here include both September 18 launches and earlier release-week projects missing from the initial list.

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
- [OpenRouter](https://openrouter.ai/typesafe/jev-1.13) - Provider listing for `typesafe/jev-1.13`, alongside the moving `typesafe/jev-latest` alias.
- [Vercel AI Gateway](https://vercel.com/changelog/typesafe-ai-jev-now-available-on-ai-gateway) - `typesafe-ai/jev` through AI SDK's experimental `evaluate` interface; its Boolean primitive corresponds to TypeSafe's Noul.

## SDKs and developer tools

Community-maintained clients and tools; official TypeSafe SDKs are listed above.

- [advocaat](https://github.com/pithings/advocaat) - Small type-safe client for asking Jev questions about datasets.
- [jev](https://github.com/dannote/jev) - Elixir/OTP client designed around GenServer replies and pattern matching.
- [jev-axi](https://github.com/shiftynick/jev-axi) - CLI for picking, rating, checking, ranking, triaging, and guarding from the shell.
- [jev-dsl](https://github.com/inanna-malick/jev-dsl) - Early-alpha Haskell DSL that encodes typed question packets and decodes answers; HTTP transport is left to the caller.
- [jev-mcp](https://github.com/blakestone-x/jev-mcp) - MCP server exposing classify, score, check, match, and screen tools.
- [jev-shell-history](https://github.com/mrnugget/jev-shell-history) - Ranks existing zsh history entries for inline completion; accepting a suggestion does not execute it.
- [Jevbridge](https://github.com/gamesonrblx/Jevbridge) - ACP/MCP adapter for using Jev alongside coding and chat models.
- [jevclient](https://github.com/AboveColin/jevclient) - Async Python client for typed Jev questions and probabilities.
- [jevr](https://github.com/simxnherrera/jevr) - Native R client for typed questions and provider-independent answers through TypeSafe or OpenRouter.
- [laravel-typesafe-jev](https://github.com/Butochnikov/laravel-typesafe-jev) - Laravel integration with typed responses, async requests, and testing fakes.
- [ruby_decision_model](https://github.com/obie/ruby_decision_model) - Ruby client with standard-library transport for TypeSafe and OpenRouter decision endpoints.
- [semdecide](https://github.com/sharziki/semdecide) - Typed semantic decisions for Unix pipelines and CI.
- [typesafe-go](https://github.com/zhirschtritt/typesafe-go) - Idiomatic Go SDK for the TypeSafe API.
- [typesafe-mcp](https://github.com/itsmostafa/typesafe-mcp) - MCP connector that gives agents access to Jev decisions.
- [typesafe-sdk-java](https://github.com/Premo-Cloud/typesafe-sdk-java) - Community Java 17 client for Choice, Score, and Noul, with an optional Spring Boot starter.
- [zod-jev](https://github.com/jomatsu/zod-jev) - Pairs local Zod shape validation with Jev semantic validation.

## Agents, coding, and guardrails

Source-reviewed experiments and integrations. A model judgment does not establish safety or replace the host application's permission checks.

- [agent-router](https://github.com/nidhi-singh02/agent-router) - Pre-release Herdr integration that filters eligible coding models by quota and policy before Jev ranks them.
- [blink](https://github.com/ellipsis-dev/blink) - Navigates file and directory names with Jev-guided walkers to find codebase paths for a natural-language query.
- [Canny](https://github.com/qkal/Canny) - Evidence ledger that challenges unsupported "done" claims from coding agents.
- [commit-miner](https://github.com/devanshbatham/commit-miner) - Classifies Git diffs and commit messages into change types and candidate security-fix/CWE labels for inspection.
- [foreman](https://github.com/thruwire/foreman) - Software-factory supervisor that uses Jev to keep coding agents on task.
- [jev-codex-router](https://github.com/0xNatoshi/jev-codex-router) - Per-turn Codex model, reasoning, and speed-mode routing.
- [jev-guard](https://github.com/leepokai/jev-guard) - Cross-agent tool-call risk scoring with allow, ask, and deny outcomes.
- [jev-review](https://github.com/devagrawal09/jev-review) - Staged code-review workflow with a local dashboard.
- [jev-review MCP plugin](https://github.com/NiazMorshed2007/jev-review) - Local-first continuous software-quality review for coding agents.
- [jev-router](https://github.com/gargpratyush/jev-router) - Chooses a model for each fresh Claude Code or Codex turn while wrapping the existing CLI.
- [jev-use](https://github.com/shitianfang/jev-use) - Claude Code / Codex / pi plugin where Jev answers batched noul, choice, and score questions and risk-checks tool calls, while a typed escalation contract hands writing and unsure steps back to the LLM.
- [jevwire](https://github.com/Brainwires/jevwire) - MCP tools, an embeddable decision library, and advisory or restrictive Claude Code hooks; judgments do not grant native permissions.
- [opencode-jev-orchestrator](https://github.com/aaronshaf/opencode-jev-orchestrator) - Keeps an OpenCode parent model fixed and uses Jev difficulty judgments to delegate harder turns to temporary subagents.
- [perch](https://github.com/lakeday-org/perch) - Semantic code linter that evaluates code units against configurable Jev questions.
- [pi-jev](https://github.com/y0usaf/pi-jev) - Measured tool-call gate and general typed decision layer for the Pi coding agent.
- [pi-warden](https://github.com/DevMortimer/pi-warden) - Pi extension that judges rule compliance, risky actions, stuck loops, and completion claims; enforcement depends on the hook and policy.
- [skillbox](https://github.com/kitze/skillbox) - Self-hosted skill library with optional Jev relevance recommendations over an authorized catalog.
- [skillranker](https://github.com/Dicklesworthstone/skillranker) - Rust CLI that ranks agent skills against live session context and can abstain.
- [supercov](https://github.com/supercorp-ai/supercov) - Scores source files so coding agents can prioritize code-quality work.

## Context and compaction

These tools select what reaches a model. Preserving retained text verbatim does not prove that omitted history was unnecessary.

- [fast-dev-compaction](https://github.com/leonaaardob/fast-dev-compaction) - Codex port that restores Jev-selected verbatim history around native session compaction.
- [fast-jev-compaction](https://github.com/tamaratran/fast-jev-compaction) - Claude Code plugin and library that score tool-call/result pairs for deletion or truncation while retaining selected text verbatim.
- [pi-fast-jev-compaction](https://github.com/joelhooks/pi-fast-jev-compaction) - Pi extension that prunes stale tool history and leaves summary compaction to Pi when pruning is insufficient.
- [pi-jev-context](https://github.com/kevinpita/pi-jev-context) - Opt-in Pi extension that filters older messages from model requests while preserving the original session history.
- [winnow](https://github.com/GhalebDweikat/winnow) - Judges tool results before admitting them into Claude Code context.
- [yoshi](https://github.com/compozy/yoshi) - Experimental Claude Code/Codex proxy that uses Jev to prune request context while preserving tool-call protocol structure.

## Browser and computer use

These projects can operate real browsers or devices when enabled. Published demos have task-specific success criteria and do not establish general reliability.

- [jev-browser](https://github.com/jkudish/jev-browser) - Browser-use experiment powered by Jev decisions.
- [jev-browser-use](https://github.com/wy-coliney/jev-browser-use) - Codex browser skill that uses Jev for navigation and target selection while Codex handles text entry and outcome verification.
- [jev-ultrafast](https://github.com/browser-use/jev-ultrafast) - Browser agent where Jev selects an operation and compatible DOM target, and a separate LLM supplies typed text.
- [jev-voice-browser](https://github.com/moritzkremb/jev-voice-browser) - Maps partial speech transcripts to browser intents and observed targets, with code deciding whether to act, wait, or ask.
- [mobile-jev](https://github.com/droidrun/mobile-jev) - Android agent using Mobilerun observations and bounded Jev actions; execute mode controls a real device, while the published Uber demo stops before booking.
- [typesafe-computer-use](https://github.com/awlevin/typesafe-computer-use) - macOS computer-use experiment using OCR plus bounded Jev action selection.

## Routing, data, and workflows

- [duckdb-jev](https://github.com/colliber/duckdb-jev) - DuckDB extension that exposes Jev judgments as SQL values with return types derived from the declared criteria.
- [HA-Jev](https://github.com/AboveColin/HA-Jev) - Home Assistant integration exposing typed answers as sensors, automation actions, and an Assist conversation agent.
- [hono-jev-router](https://github.com/yusukebe/hono-jev-router) - Routes Hono HTTP requests by meaning.
- [jev-curate](https://github.com/AkashPriyadarshii/jev-curate) - Streaming filter and scorer for Parquet and JSONL datasets.
- [jev-reviewer](https://github.com/choxos/jev-reviewer) - Research-document extraction aid where Jev selects and verifies source lines for verbatim quotes; findings require human review and are not clinical decisions.
- [jev-search](https://github.com/superagents-lab/jev-search) - Uses Jev to select search sources and rank Search1API results, returning source links and snippets.
- [jev-trader](https://github.com/jarrodwatts/jev-trader) - Kuru/Monad trading experiment with optional Jev buy/sell decisions; defaults to a mock model and dry-runs without a private key, but configured execution can place real orders.
- [jev-tree](https://github.com/reachjalil/jev-tree) - Recursive choice over taxonomies larger than Jev's direct option limit.
- [jevlogs](https://github.com/reachjalil/jevlogs) - OpenTelemetry log triage before more expensive analysis.
- [jevsql](https://github.com/EugeneBoondock/jevsql) - SQL-like filtering, ranking, classification, and scoring with natural-language predicates.
- [llama-index-jev](https://github.com/WiktorB2004/llama-index-jev) - LlamaIndex reranker and selector using Jev Score and Choice answers, with configurable confidence handling.
- [n8n-nodes-typesafe-jev](https://github.com/n3ndor/n8n-nodes-typesafe-jev) - Community n8n node for asking multiple typed questions over workflow state.
- [pg-jev](https://github.com/realZachi/pg-jev) - PostgreSQL extension for semantic questions over table rows.
- [pg_typesafe](https://github.com/giuliosmall/pg_typesafe) - Pre-alpha PostgreSQL C extension exposing Choice, Noul, Score, and batched judgments from SQL.
- [tax-doc-classifier](https://github.com/kyotofin/tax-doc-classifier) - Classifies text-bearing PDF pages into IRS form and page-kind candidates with a confidence gate; document triage, not tax advice, and scanned pages need OCR.
- [tiershift](https://github.com/iamvatsalpatel/tiershift) - Policy-bounded model routing for TypeScript and Python.
- [typesafe-jev-workflow](https://github.com/GiesN/typesafe-jev-workflow) - LangGraph email-intent workflow using a typed Jev choice.

## Games, robotics, and interactive demos

- [heist-one](https://github.com/AbdelStark/heist-one) - Browser stealth game where Jev judges guards while deterministic code owns the world.
- [jev-drone](https://github.com/RomanSlack/jev-drone) - Simulated MuJoCo quadrotor with Jev making slower tactical judgments from processed camera observations; deterministic code controls flight.
- [jev-experiments](https://github.com/dabit3/jev-experiments) - Collection of inspectable Jev demos, including scripted support conversations with typed intent, escalation, and suggested-response decisions.
- [JevPilot](https://github.com/standardagents/jevpilot) - Three.js driving simulation where Jev chooses among candidate paths and speeds while local code handles vehicle dynamics and geometry.
- [JevScape](https://github.com/Skyvern-AI/jevscape) - RuneBench-based RuneScape harness that maps Jev choices to a bounded game-action catalog and records tick-level results.
- [killmyidea](https://github.com/monteduro/killmyidea) - Startup-idea evaluator that chooses kill, fix, or ship.
- [tsai-sc](https://github.com/phyous/tsai-sc) - Original StarCraft shareware controlled with recorded Jev action probabilities.
- [typesafe-mario](https://github.com/fhshaik/typesafe-mario) - Super Mario Bros. agent choosing actions from structured emulator state.
- [typesafe-snake](https://github.com/sorrycc/typesafe-snake) - Snake autoplayer with one typed decision per tick and code-generated legal moves.

## Media and creative tools

- [jevmeter](https://github.com/ChetasLua/jevmeter) - Scores every sentence in a video and renders the result as an overlay.
- [Jevthoven](https://github.com/cocktailpeanut/jevthoven) - Symbolic-music studio where Jev chooses plans, instruments, and bar patterns, and code renders editable music and MIDI.
- [SlidePilot](https://github.com/harshil1712/slidepilot) - Experimental Slidev controller that judges speech transcripts for slide completion, with deterministic checks and manual navigation.
- [Sponsor Skip](https://github.com/trungdq88/youtube-sponsor-detection) - Finds sponsor reads in YouTube transcripts or transcribed audio while code owns timestamps and playback skipping.
- [unclutter](https://github.com/kitze/unclutter) - Browser extension that uses Jev to identify page clutter and saves reusable, reversible hiding rules.
- [Vibe Check for X](https://github.com/RafalWilinski/vibecheck) - Chrome extension that scores draft posts and reply context before posting; optional media descriptions come from a separate vision model.

## Open reproductions and research

These projects explore Jev-like interfaces or open implementations. They are independent efforts, not official TypeSafe releases or verified reproductions of its proprietary architecture, RLCD training, or calibration.

- [Jev Visual](https://github.com/hr98w/jev-visual) - Educational MLX/Qwen vision-language experiment sharing image context across candidate-scoring questions; its probabilities are not calibrated correctness estimates.
- [Jevlike](https://github.com/vinnylarouge/jevlike) - Trainable encoder and option-attention head for variable candidate sets, with separate visual game experiments.
- [jevmlx](https://github.com/bnsd55/jevmlx) - Jev-style parallel constrained decisions for MLX models on Apple Silicon.
- [kev](https://github.com/jaredpalmer/kev) - Qwen2.5-0.5B adapter and decision head with training code, released weights, and parallel typed-question inference.
- [NanoJev](https://github.com/TianyuCodings/NanoJev) - Small parallel-decision model with dynamic candidates, a training pipeline, and recorded game comparisons that include shared code planning.
- [openjev](https://github.com/zhihz/openjev) - Local bilingual probability decisions from context, questions, and candidate answers.
- [OpenJev (DiffusionGemma)](https://github.com/razorback16/openjev) - Independent Jev-compatible server over DiffusionGemma/vLLM; the documented setup requires custom vLLM patches.
- [openjev-sglang](https://github.com/ekzhang/openjev-sglang) - Jev-compatible API endpoint backed by open models and prefill-only inference.
- [openvons](https://github.com/genai-craft/openvons) - Open decision layer for finite options across text, images, and Japanese voice commands.
- [parallelConstraintDecoding](https://github.com/stephanj/parallelConstraintDecoding) - Java and llama.cpp experiments in parallel constrained decoding.
- [reflex](https://github.com/kshetrajna12/reflex) - Open-model decision engine with shared-state inference, isolated question branches, and a WebGPU demo; browser and Python configurations differ.
- [SemIf](https://github.com/TheoLeeCJ/SemIf) - Formerly OpenJev: an independent study of typed option readout from frozen open models, with shared-prefix experiments and a WebGPU demo.
- [Simple Jev](https://github.com/featherless-ai/simple-jev) - Transforms compatible open-model logits into typed decisions without a separately trained classifier head; model compatibility is constrained.
- [Verdict-open-jev](https://github.com/Heman10x-NGU/Verdict-open-jev) - ModernBERT decision engine with calibrated uncertainty and a WebGPU playground.

## Evaluation and calibration

Results belong to each project's dataset, prompts, model version, and measurement setup. Inclusion means the evidence is inspectable, not that benchmarks were independently rerun.

- [Janus](https://github.com/FirasSX914/Janus) - Measures when to use Jev versus other models and routes accordingly.
- [jev-behavior-study](https://github.com/RINNECODER/jev-behavior-study) - Independent synthetic-task study of Jev 1.13.0 framing sensitivity and failures, with raw responses and offline report checks.
- [jev-benchmarks](https://github.com/AbdelStark/jev-benchmarks) - Reproducible evaluation for calibration, selective risk, and latency.
- [jev-eval](https://github.com/4esv/jev-eval) - Independent Jev versus GPT-5.6 Terra comparison on three labeled classification tasks, reporting accuracy, calibration, latency, and cost.
- [jev-eval-agent](https://github.com/vinilana/jev-eval-agent) - Compares LLM tool selection with Jev routing in a personal-assistant harness containing 100 mocked tools.
- [jev-korean-benchmark](https://github.com/mahlernim/jev-korean-benchmark) - Small Korean/English sample study with recorded responses, including medical-text questions; not a clinical validation.
- [jev-search-rerank-eval](https://github.com/zhuyansen/jev-search-rerank-eval) - Chinese/English retrieval evaluation comparing Jev reranking with lexical, embedding, and fusion baselines, including judge-circularity analysis.
- [jevcal](https://github.com/abhixhek/jevcal) - Fits and drift-checks confidence thresholds against labeled data.
- [typesafe-ai-benchmark](https://github.com/iammrduncan/typesafe-ai-benchmark) - LLM gateway that mimics the System One output shape for comparison work.

## Guides and cookbooks

- [Building with Jev](https://github.com/dbreunig/building-with-jev-skill) - Community agent skill covering question design, state preparation, confidence thresholds, and debugging decisions.
- [Classifying RAG passages](https://docs.typesafe.ai/cookbooks/classifying_rag_passages) - Official example of judging retrieved passages before passing them to an answering model.
- [Date extraction](https://docs.typesafe.ai/cookbooks/date_extraction_cookbook) - Official pattern separating typed extraction from date validation and arithmetic in code.
- [Double-checking citations](https://docs.typesafe.ai/cookbooks/citation_check) - Official example of checking whether source context supports a claim.
- [Parallel questions](https://docs.typesafe.ai/cookbooks/parallel_questions) - Official worked example of evaluating many questions over shared state in one request.
- [Skill suggestion](https://docs.typesafe.ai/cookbooks/skill_suggestion) - Official two-stage workflow that selects a skill and can reject the shortlist.

## Related lists

- [awesome-jev-by-typesafe](https://github.com/Anil-matcha/awesome-jev-by-typesafe) - Evidence-backed use cases, patterns, prompts, and starter code.
- [awesome-jev](https://github.com/hellogumbo/awesome-jev) - Large community directory with a searchable companion site.
- [yibie/awesome-jev](https://github.com/yibie/awesome-jev) - High-signal field guide organized by decision domain.
- [awesome-typesafe](https://github.com/AbdelStark/awesome-typesafe) - Broader TypeSafe and System One ecosystem list.
- [OmniJev/awesome-jev](https://github.com/OmniJev/awesome-jev) - Papers, open reproductions, independent evaluations, and technical lineage.

## Contributing

Built something with Jev? Read [CONTRIBUTING.md](CONTRIBUTING.md) and open a pull request. Small projects are welcome when the source clearly shows a concrete Jev decision loop.

## License

[CC0 1.0 Universal](LICENSE). Linked projects keep their own licenses.

## Acknowledgements

Discovery used public GitHub search, TypeSafe and provider documentation, and the related community lists above. Descriptions added in this refresh were checked against pinned project READMEs and relevant source files; the [research notes](research/2026-09-19.md) record those sources. Inclusion is not an endorsement by TypeSafe AI or a claim of production readiness.
