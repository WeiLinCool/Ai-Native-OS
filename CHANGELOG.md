# Changelog

All notable changes to AI-Native OS. The format is based on [Keep a Changelog](https://keepachangelog.com);
AI-Native OS uses date-based versions since it is a living framework, not shipped software.

## [3.2.1] - 2026-10 — sandbox path fix

### Fixed
- The tool sandbox now refuses Windows-style drive paths (`C:/...`) as absolute on every
  platform, not only on Windows — on POSIX such a path used to be treated as repository-relative.
  [tests.test_tools](runtime/tests/test_tools.py) passes again: `python runtime/run_tests.py` →
  222/222 OK, so the runtime CI job is green.

## [3.2] - 2026-10 — bilingual READMEs

Every README now ships with a Chinese counterpart and a machine-checked consistency record.

### Added
- **Bilingual README triplets** — 106 x `README.md` + `README.zh.md` + `README.i18n.yaml`, with a
  language switcher on line 3 of every pair. Scope and rules live in [docs-constraint.yaml](docs-constraint.yaml)
  and [CONTRIBUTING.md](CONTRIBUTING.md#bilingual-documentation).
- **Documentation gates** — the dependency-free doc-constraint toolchain in [scripts/](scripts/):
  [`run-gates.ts`](scripts/run-gates.ts) dispatches the enabled gates, and
  [`verify-translation-pairing.ts`](scripts/verify-translation-pairing.ts) enforces counterpart existence,
  a matching structural signature (headings, code blocks, tables, lists) and recorded git blob hashes.
- **[`scripts/i18n-record.py`](scripts/i18n-record.py)** — re-records the `.i18n.yaml` hashes after an edit.
- **CI job** — `bilingual-docs` in [.github/workflows/docs-check.yml](.github/workflows/docs-check.yml)
  runs the gates on every push and PR.

### Changed
- [scripts/check-structure.py](scripts/check-structure.py) ignores `*.zh.md` counterparts when counting
  agent specs, and [STRUCTURE.md](STRUCTURE.md) documents the new tooling and config.

## [3.1] - 2026-10 — renamed to Ai-Native-OS

The framework was forked from [rojenwai/CompanyOS](https://github.com/rojenwai/CompanyOS) and
rebranded. Branding, repository URLs, and every runtime identifier were renamed; no guidance,
standard, agent spec, or orchestration rule changed.

### Changed
- **Brand** — the framework is now **AI-Native OS** (repository `WeiLinCool/Ai-Native-OS`, root
  folder label `ai-native-os`). Every document, index, and diagram was updated.
- **Runtime package** — `runtime/companyos/` → [`runtime/ai_native_os/`](runtime/ai_native_os/), so
  imports read `from ai_native_os import Orchestrator, RuntimeConfig`.
- **CLI** — `python -m companyos …` → `python -m ai_native_os …`; the installed console script is
  `ai-native-os` (package metadata: `ai-native-os-runtime`).
- **Environment & paths** — `COMPANYOS_ROOT` → `AI_NATIVE_OS_ROOT`; the config file
  `companyos.json` → `ai-native-os.json`; run traces `.companyos/runs/` → `.ai-native-os/runs/`.
- **Links** — all GitHub URLs now point at `WeiLinCool/Ai-Native-OS`; the upstream copyright notice
  is retained in [LICENSE](LICENSE) and credited in the [README](README.md#credits).

### Unchanged
- The 107 agent specs, 20 department manuals, governance, standards, playbooks, templates, and the
  orchestration behaviour are identical — the runtime still reads the specs as they are.

## [3.0] - 2026-09 — the runtime

AI-Native OS stops being only a specification. The agent specs are now executed.

### Added
- **[runtime/](runtime/README.md)** — a dependency-free Python package that reads the
  [agent specs](ai/agents/README.md) and orchestrates them for a request:
  plan → decompose → select → spawn → execute in parallel → aggregate → review → synthesize.
  ```bash
  python -m ai_native_os run "Design and implement authentication for a web application."
  ```
- **[ai/orchestration/runtime.md](ai/orchestration/runtime.md)** — the distinction the runtime rests
  on: an **agent definition** is a template in `ai/agents/`; an **agent instance** is a temporary
  agent handling one task. A run instantiates only the agents it needs, then terminates them. There
  are never 107 agents running.
- **Agent Registry** — discovers all 117 definitions (107 specs + the kernel agents) by parsing their
  Markdown. Capabilities, division, reporting line, and tool grants are derived from each spec's own
  text, so **adding an agent needs no code** — write the 11-section spec and it becomes selectable.
- **Capability-based selection** — scored against the registry rather than routed through a hardcoded
  table, with `python -m ai_native_os select` to inspect why an agent won.
- **Parallel execution** — independent subtasks run concurrently; dependent ones cannot. A failed
  branch skips only its own dependents, and the gap is stated in the answer rather than hidden.
- **Reviewer loop** — the [reviewer](ai/orchestration/reviewer.md),
  [QA](ai/orchestration/qa-reviewer.md), [security](ai/orchestration/security-reviewer.md), and
  [documentation](ai/orchestration/documentation-reviewer.md) agents run in parallel over the results;
  rejected work returns to its author with the findings attached. A Security Reviewer block sets the
  run to `AWAITING_APPROVAL` and is never auto-cleared, per the
  [approval engine](ai/orchestration/approval-engine.md).
- **Agent Map** — the live execution graph as JSON (`--map`), ready for a UI, plus a terminal renderer.
- **Provider abstraction** — Anthropic, OpenAI, any OpenAI-compatible local server, and an offline
  deterministic mock. No vendor SDK, no orchestration code aware of the provider.
- **Safeguards** — caps on spawned agents, task depth, review iterations, concurrency, attempts,
  timeouts, tokens, tool calls, and context size. Each enforced in code and covered by a test.
- **Tool boundaries** — default-deny. Spawned agents get no shell, no network, and no filesystem
  writes; reads are sandboxed to the spec tree; memory writes are proposals, never direct.
- **220 tests** (`python runtime/run_tests.py`) — stdlib `unittest`, mocked providers, no API keys.
  Added as a second CI job alongside the documentation checks.

### Changed
- [ai/orchestration/README.md](ai/orchestration/README.md), [ai/README.md](ai/README.md),
  [README.md](README.md), and [STRUCTURE.md](STRUCTURE.md) now point at the runtime and explain the
  `ai/` (specification) versus `runtime/` (implementation) split.
- No agent spec, memory document, or governance rule was modified. The runtime reads them as they are.

## [2.3] - 2026-07 — the executive layer

### Added
- **[ai/agents/executive/](ai/agents/executive/README.md)** — the AI C-suite (14 new specs, 107 total).
  Until now department agents reported to a "CTO" that existed only as prose in
  [roles.md](handbook/company/roles.md); now every executive is a real agent that owns named divisions.
  - **[AI Co-Founder](ai/agents/executive/ai-cofounder-agent.md)** — the founder's counterpart. Owns the
    thesis, the one-way doors, and the standing case *against* the current plan. Distinct from the
    [CEO Agent](ai/orchestration/ceo-agent.md), which orchestrates execution: the Co-Founder decides
    what is worth executing.
  - [CTO](ai/agents/executive/cto-agent.md) · [CPO](ai/agents/executive/cpo-agent.md) ·
    [COO](ai/agents/executive/coo-agent.md) · [CFO](ai/agents/executive/cfo-agent.md) ·
    [CRO](ai/agents/executive/cro-agent.md) · [CMO](ai/agents/executive/cmo-agent.md) ·
    [Chief Designer](ai/agents/executive/chief-designer-agent.md) ·
    [Chief Scientist](ai/agents/executive/chief-scientist-agent.md) ·
    [CDO](ai/agents/executive/chief-data-officer-agent.md) ·
    [CSO](ai/agents/executive/chief-security-officer-agent.md) ·
    [CLO](ai/agents/executive/chief-legal-officer-agent.md) ·
    [CPeO](ai/agents/executive/chief-people-officer-agent.md) ·
    [Chief of Staff](ai/agents/executive/chief-of-staff-agent.md).
- **Three hard blocks** no agent may override — security (known-exploitable work), legal (unlawful
  action), and money (no agent commits funds). Only the human founder can waive them, in writing.

### Changed
- [handbook/company/roles.md](handbook/company/roles.md) and [structure.md](handbook/company/structure.md)
  now map every executive to the divisions it owns, and state the four things that always stay human.

## [2.2] - 2026-07 — roadmap complete

### Added
- **5 more starter kits** (16 total): [fintech](starter-kits/fintech/), [healthtech](starter-kits/healthtech/),
  [climate-tech](starter-kits/climate-tech/), [gaming](starter-kits/gaming/), [edtech](starter-kits/edtech/).
- **3 more cross-department playbooks** (11 total): handling a customer complaint, scaling a team,
  international expansion.
- **4 more document templates** (17 total): employment agreement, DPA, sales proposal, QBR.
- **Deeper worked examples** — a second example for engineering (RFC), product (user stories), sales
  (objection handling), hr (interview debrief), and finance (budget variance).
- **[scripts/scaffold.py](scripts/scaffold.py)** — a CLI to scaffold a new department or agent from the templates.
- **[scripts/check-conventions.py](scripts/check-conventions.py)** — a third CI check: every folder
  self-indexes, no placeholder text, markdown hygiene. Now wired into `docs-check.yml`.
- **Stale-issue bot** (`.github/workflows/stale.yml`).
- A **"How to customize"** section in the root README, and `README.md` files for all 20 agent divisions
  and `post-launch/technical-debt/`.

### Changed
- [ROADMAP.md](ROADMAP.md) rewritten: every previously planned direction is now built.

## [2.1] - 2026-07

### Changed — repository split into two sides, for easy customization
- **`handbook/`** now holds everything humans read: `company/`, `governance/`, all 20 department
  manuals under `handbook/departments/`, `workflows/`, `standards/`, `playbooks/`, `templates/`, and
  `guides/` (formerly `docs/`).
- **`ai/`** now holds everything the AI workforce runs on: `agents/` (93 specs), `orchestration/`, and
  `memory/`.
- The AI *department* (the discipline of building AI products) was renamed to
  `handbook/departments/ai-engineering/` to free the top-level `ai/` name for the agent workforce.
  Its agent folder moved to `ai/agents/ai-engineering/`.
- `docs/ROADMAP.md` moved to `ROADMAP.md` at the repository root.
- All ~4,200 internal links were remapped; both CI checks pass.

### Added
- **[CUSTOMIZE.md](CUSTOMIZE.md)** — a step-by-step guide to making the repo your own: what to edit
  always, what to tune, what to read, and what to leave alone; plus how to add or remove a department
  or an agent.
- Index pages for each side: [handbook/README.md](handbook/README.md),
  [handbook/departments/README.md](handbook/departments/README.md), and [ai/README.md](ai/README.md).
- A folder-structure diagram in the root README.

### Fixed
- Updated GitHub URLs after the repository was renamed.

## [2.0] - 2026-07

### Added
- **Complete department coverage.** All 20 departments built to the full 18-file structure with
  subfolders: engineering, product, post-launch, design, research, ai, strategy, security, devops,
  finance, legal, hr, operations, marketing, sales, customer-success, data, documentation, hardware,
  investor-relations.
- **93 AI agent specifications**, each following the 11-section [standard spec](ai/agents/agent-template.md).
- **11 starter kits** - ai-startup (exemplar) plus saas, developer-tools, enterprise-b2b, marketplace,
  consumer-app, robotics, drone, embedded, iot, research-lab.
- **The [Company-Building Guide](handbook/guides/company-building-guide.md)** - skills to learn and steps to build
  and manage a company; plus [onboarding paths](handbook/guides/onboarding-paths.md), [goals & OKRs](handbook/guides/okrs.md),
  and an [end-to-end worked example](handbook/guides/example-company.md).
- **Community health & CI** - `.github/` (issue/PR templates, code of conduct, security, support,
  funding) and docs-check workflows (link integrity + structure conformance).
- **More document templates** (OKR, offer letter, board update, one-pager) and **cross-department
  playbooks** (hiring an engineer, running a sprint, fundraising).
- Root [MIT LICENSE](LICENSE).

### Changed
- Repurposed the single-file operating manual into the modular AI-Native OS: kernel (orchestration +
  memory + agents), governance, standards, workflows, templates, and playbooks.
- Upgraded the four seeded departments (design, research, ai, strategy) to full structure.

## [1.0]

### Added
- The original single-file "AI Company Operating Manual" (8 parts), preserved in git history.
