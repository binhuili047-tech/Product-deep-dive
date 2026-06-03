# Product Deep Dive Skill

[中文](README.md) | [English](README.en.md)

![Codex Skill](https://img.shields.io/badge/Codex-Skill-111827)
![Claude Compatible](https://img.shields.io/badge/Claude-Compatible-6B46C1)
![Feishu/Lark Docs](https://img.shields.io/badge/Feishu%2FLark-Docs-00B96B)
![Whiteboard Ready](https://img.shields.io/badge/Editable-Whiteboards-7B61FF)
![Language](https://img.shields.io/badge/Language-ZH%20%2B%20EN-blue)
![License](https://img.shields.io/github/license/VioletScar-Hui/Product-deep-dive)
![Status](https://img.shields.io/badge/Status-Active-success)

`product-deep-dive` is a Codex and Claude Code compatible skill for AI product managers, product researchers, and teams that need deep product, competitor, business, technical, model, and architecture analysis. Its default output is a polished Feishu/Lark Docs long-form product teardown.

This skill is not a feature-summary template. It guides the agent to start from real product experience, then analyze positioning, evaluation, critical user paths, differentiation, capability boundaries, market structure, business logic, user scenarios, technical inference, model strategy, foundation/data assets, and a final architecture whiteboard.

This repository includes a [`LICENSE`](LICENSE) file. See [`CHANGELOG.md`](CHANGELOG.md) for version history.

---

## Visual Overview

### 1. From Product Input to Feishu Document

![Product Deep Dive overview](assets/intro-01-overview.png)

### 2. Evaluation System: Black Box to White Box

![Product Deep Dive evaluation system](assets/intro-02-evaluation.png)

### 3. Editable Six-Layer Architecture Whiteboard

![Product Deep Dive architecture whiteboard](assets/intro-03-architecture.png)

## Live Example

- Feishu document example: [Product Deep Dive sample document](https://ucn5k46k8jsn.feishu.cn/wiki/NQVuw8oPSiWIDZkvgTFcYa7XnLa)

---

## When To Use

Use this skill only when both conditions are true:

1. The user asks for a deep teardown, deep analysis, evaluation framework, or structured framework for an AI product.
2. The user wants the output delivered as a Feishu document, Feishu cloud document, or Feishu-style long-form product teardown.

Good prompts:

```text
Now I want to analyze an AI product. Build the teardown framework and output a Feishu document.
```

```text
Help me deeply analyze this AI Agent product and write the result into a Feishu document.
```

```text
Write a Feishu-style AI product manager teardown article for product XXX.
```

Do not trigger this skill merely because a conversation mentions AI, Agent, RAG, LLM, SaaS, AIGC, or a product name. If the user asks only a short product question, a recommendation, a concept explanation, or a brainstorm without Feishu document delivery intent, use a more specific answer or skill.

If intent is unclear, ask one concise question: `Do you want a Feishu-document style AI product deep dive?`

---

## Required Prerequisite: lark-cli

This skill is built around Feishu/Lark document delivery. Install and configure `lark-cli` before expecting full document creation, update, or whiteboard workflows to work.

Minimum checks:

```powershell
lark-cli auth status
lark-cli docs +create --api-version v2 --help
```

Optional version check:

```powershell
lark-cli --version
```

If `lark-cli auth status` shows no usable user login, authenticate as a user before running product teardown workflows. When Feishu returns a missing-scope error, follow the scope hint from `lark-cli` and authorize that exact scope.

Optional whiteboard check:

```powershell
npx -y @larksuite/whiteboard-cli@^0.2.11 -v
```

Without `lark-cli`, the skill can still draft a teardown framework in chat, but it cannot reliably create or update Feishu documents.

---

## Installation

### Easiest Path: Ask An AI Agent To Install From URL

If you are using Codex or Claude Code, you can send this directly to the agent:

```text
Install this skill: https://github.com/VioletScar-Hui/Product-deep-dive/tree/main/product-deep-dive
```

Chinese prompt also works:

```text
帮我安装这个 skill：https://github.com/VioletScar-Hui/Product-deep-dive/tree/main/product-deep-dive
```

Generic format:

```text
Install this skill: https://github.com/<owner>/<repo>/tree/main/<skill-name>
```

The agent should check whether a skill with the same name already exists, then install the repository's skill subdirectory into the local skills directory. For this repository, copy `product-deep-dive/`, not the repository root. Restart Codex or Claude Code after installation.

### Codex

```powershell
$repoPath = "$env:USERPROFILE\.codex\skill-repos\Product-deep-dive"
$skillPath = "$env:USERPROFILE\.codex\skills\product-deep-dive"
New-Item -ItemType Directory -Force -Path (Split-Path $repoPath) | Out-Null
if (Test-Path "$repoPath\.git") {
  Set-Location $repoPath
  git pull --ff-only
} elseif (Test-Path $repoPath) {
  Write-Error "$repoPath already exists but is not a git repository. Move it aside or choose a different repoPath."
  exit 1
} else {
  git clone https://github.com/VioletScar-Hui/Product-deep-dive.git $repoPath
}
New-Item -ItemType Directory -Force -Path $skillPath | Out-Null
Copy-Item -Path "$repoPath\product-deep-dive\*" -Destination $skillPath -Recurse -Force
```

### Claude Code

```powershell
$repoPath = "$env:USERPROFILE\.claude\skill-repos\Product-deep-dive"
$skillPath = "$env:USERPROFILE\.claude\skills\product-deep-dive"
New-Item -ItemType Directory -Force -Path (Split-Path $repoPath) | Out-Null
if (Test-Path "$repoPath\.git") {
  Set-Location $repoPath
  git pull --ff-only
} elseif (Test-Path $repoPath) {
  Write-Error "$repoPath already exists but is not a git repository. Move it aside or choose a different repoPath."
  exit 1
} else {
  git clone https://github.com/VioletScar-Hui/Product-deep-dive.git $repoPath
}
New-Item -ItemType Directory -Force -Path $skillPath | Out-Null
Copy-Item -Path "$repoPath\product-deep-dive\*" -Destination $skillPath -Recurse -Force
```

Restart Codex or Claude Code after installation so the skill index reloads.

---

## Quick Install For AI Agents

Users may ask for installation with a prompt like:

```text
Install this skill: https://github.com/VioletScar-Hui/Product-deep-dive/tree/main/product-deep-dive
```

```text
帮我安装这个 skill：https://github.com/VioletScar-Hui/Product-deep-dive/tree/main/product-deep-dive
```

They may also use the generic GitHub skill-subdirectory format:

```text
Install this skill: https://github.com/<owner>/<repo>/tree/main/<skill-name>
```

The agent should parse the GitHub URL and confirm that the target is the skill subdirectory, not the repository root. For this repository, the directory to copy into the local skills directory is `product-deep-dive/`.

If a user asks you to install this skill, first check the Feishu delivery prerequisite:

```powershell
lark-cli auth status
lark-cli docs +create --api-version v2 --help
```

Then install or update the skill and verify:

```powershell
Test-Path "$env:USERPROFILE\.codex\skills\product-deep-dive\SKILL.md"
Get-Content "$env:USERPROFILE\.codex\skills\product-deep-dive\SKILL.md" -TotalCount 8
```

For Claude Code, verify the same file under:

```powershell
Test-Path "$env:USERPROFILE\.claude\skills\product-deep-dive\SKILL.md"
Get-Content "$env:USERPROFILE\.claude\skills\product-deep-dive\SKILL.md" -TotalCount 8
```

Optional Feishu workflow verification:

```powershell
lark-cli docs +create --api-version v2 --help
npx -y @larksuite/whiteboard-cli@^0.2.11 -v
```

Finally, tell the user to restart Codex or Claude Code.

---

## First Successful Run

After installation, ask Codex or Claude Code:

```text
Now I want to analyze Xingye. Build the product teardown framework and output a Feishu document.
```

The agent should:

1. Search or read public product materials.
2. Generate a Feishu-style teardown structure.
3. Create a new Feishu document when no target document URL is provided.
4. Write core conclusions, 13 chapters, tables, layer diagrams, and the information gap checklist.
5. Return only a concise confirmation and the Feishu document link.

---

## Default Output Structure

```text
Product Deep Dive: [Product Name]

Product Basic Information
Core Conclusions

1. Product Positioning and Experience Summary
2. Testing and Evaluation System
3. Test Flow and Screenshots
4. Differentiated Positioning
5. Capability Boundaries
6. Market Layer Analysis
7. Business Layer Analysis
8. Scenario/User Layer Analysis
9. Technical Layer Analysis
10. Model Layer Analysis
11. Uncertainty Handling
12. Foundation Layer Analysis
13. Final Architecture Diagram

Information Gap Checklist
```

Every numbered chapter contains 3-8 dynamically rewritten high-value questions and ends with a product-manager insight callout.

---

## Core Capabilities

### Product Manager Depth

- Converts visible product experience into positioning, target users, scenarios, and trade-offs.
- Rewrites high-value questions for the concrete product instead of pasting a generic template.
- Ends key sections with transferable product-manager insights.

### Evidence Discipline

The document separates:

- **Facts**: official websites, screenshots, public materials, and official docs.
- **Observations**: behavior seen during actual product use.
- **Inferences**: system, workflow, or technical assumptions inferred from experience.
- **Judgments**: analyst opinions.
- **To verify**: missing evidence or follow-up tests.

### Testing and Evaluation

The skill uses three fixed main dimensions and then builds scenario-specific sub-indicators:

| Main Dimension | Evaluation Lens | Focus |
|---|---|---|
| End-to-End | Black-box evaluation | Final output, task completion, and whether the user receives a usable result. |
| Process Capability | Glass-box evaluation | Intermediate process, state changes, tool use, decision path, interaction recovery, and workflow reliability. |
| Comprehensive Evaluation | White-box evaluation | Full-process multidimensional assessment across output, process, model orchestration, cost, safety, data, and business value. |

Common second-level indicator families:

| Family | What It Evaluates |
|---|---|
| End-to-End Result Layer | Final output, task completion, delivery completeness, and user-perceived usefulness. |
| User Layer | Entry point, user path, friction, controllability, trust building, feedback, retention trigger, and Aha Moment. |
| Model/Data Layer | Model capability fit, routing, context use, RAG/data grounding, memory, data freshness, personalization, and hallucination risk. |
| Technical Layer | Workflow orchestration, agent/tool calls, state management, latency, stability, error recovery, permissions, security, and integrations. |

Every dimension should explain: `what to evaluate`, `why it matters`, and `how to score it`.

### Market and Competitor Analysis

Section 6 always includes a competitor comparison table covering the analyzed product and at least 3 main competitors:

| Column | Purpose |
|---|---|
| Platform/Company | Identifies the product, company, platform, or ecosystem entry point. |
| Main Role | Clarifies whether it is a direct competitor, substitute, platform owner, content ecosystem, tool provider, or adjacent entrant. |
| Distribution Channel | Shows where the product reaches users: app stores, web, social platforms, enterprise sales, creator communities, ecosystem bundles, and more. |
| Core Business Model | Summarizes subscription, usage-based pricing, ads, marketplace take rate, enterprise contracts, traffic conversion, or bundled service logic. |
| Latest Public Information | Uses verifiable public information; marks `to verify` when evidence is incomplete. |

The same section also includes a competitive landscape diagram. Axes are chosen dynamically for the product category.

### Six-Layer Architecture

The final architecture uses six layers:

1. Market Layer
2. Business Layer
3. User Layer
4. Application Layer
5. Model Layer
6. Foundation Layer

Each corresponding chapter can include a mini layer diagram, followed by a final six-layer architecture diagram.

Since v2.0, editable architecture diagrams must be built as native Feishu whiteboard nodes or DSL-generated raw nodes. Every visible label must be an explicit editable text node. Do not rely on SVG text conversion or rectangle-only `text` fields. After writing, the agent must query raw nodes, confirm required labels are searchable, and export preview images to verify that text actually renders.

### Feishu/Lark Polish

- High-value questions are placed in blockquote panels.
- Product-manager insights are placed in Feishu callout/highlight blocks.
- Tables use gray-background bold styling for the first row and first column.
- Architecture diagrams prefer editable Feishu whiteboards.
- The final architecture stacks layers top-to-bottom: Market -> Business -> User -> Application -> Model -> Foundation.

---

## Feishu and Whiteboard Requirements

Full Feishu document delivery requires:

- `lark-cli` installed.
- Feishu/Lark user authentication completed.
- Permission to create or update Feishu documents.
- Whiteboard node read/write permissions when editable architecture diagrams are needed.

Recommended architecture workflow:

```text
structured architecture
  -> native/DSL whiteboard nodes
  -> OpenAPI raw nodes
  -> editable Feishu whiteboard
  -> raw-node + preview verification
```

Do not treat a `<whiteboard token=...>` block as sufficient proof. The board must have editable text nodes, no zero-size image fragments, no unexpected connectors, and readable preview images.

---

## Version Highlights

| Version | Focus | What Changed |
|---|---|---|
| v2.0 | Native editable whiteboards and senior AIPM gates | Replaced SVG-text conversion with native/DSL whiteboard nodes, added raw-node and preview verification for every architecture board, and consolidated senior AIPM depth checks for key chapters. |
| v1.5 | Evaluation sub-dimensions | Expanded the testing system with scenario-specific second-level indicators such as end-to-end result, user layer, model/data layer, and technical layer, plus detailed dimension descriptions. |
| v1.4 | Market competitor analysis | Required section 6 to include a 3+ competitor comparison table and a competitive landscape diagram using product-relevant axes. |
| v1.3 | Three-layer evaluation framework | Standardized testing around end-to-end black-box output evaluation, process glass-box evaluation, and comprehensive white-box evaluation. |
| v1.2 | Documentation, distribution, and cross-agent support | Added bilingual README onboarding, `lark-cli` prerequisite checks, Codex/Claude Code install paths, license visibility, and versioned changelog navigation. |
| v1.1 | Feishu delivery, whiteboards, and formatting rules | Added Feishu document delivery defaults, editable whiteboard architecture diagrams, strict trigger discipline, dynamic high-value questions, callout rules, and gray/bold table styling. |
| v1.0 | Initial product deep-dive framework | Established the 13-section AI product teardown framework, core conclusions, evidence discipline, information gap checklist, and evaluation coverage. |

See [`CHANGELOG.md`](CHANGELOG.md) for full details.

---

## Repository Structure

```text
Product-deep-dive/
  README.md              # Default Chinese README
  README.en.md           # English README
  CHANGELOG.md           # Version history
  LICENSE                # Repository license
  assets/                # README visual assets
  product-deep-dive/
    README.md            # Skill-level guide
    SKILL.md             # Codex / Claude-compatible skill instructions
    references/          # Deep-analysis reference modules
    evals/
      evals.json         # Skill eval cases
```

---

## Updating

### Codex

```powershell
$repoPath = "$env:USERPROFILE\.codex\skill-repos\Product-deep-dive"
$skillPath = "$env:USERPROFILE\.codex\skills\product-deep-dive"
if (-not (Test-Path "$repoPath\.git")) {
  Write-Error "$repoPath is not an installed Product-deep-dive git repository. Run the install command first."
  exit 1
}
Set-Location $repoPath
git pull --ff-only
New-Item -ItemType Directory -Force -Path $skillPath | Out-Null
Copy-Item -Path "$repoPath\product-deep-dive\*" -Destination $skillPath -Recurse -Force
```

### Claude Code

```powershell
$repoPath = "$env:USERPROFILE\.claude\skill-repos\Product-deep-dive"
$skillPath = "$env:USERPROFILE\.claude\skills\product-deep-dive"
if (-not (Test-Path "$repoPath\.git")) {
  Write-Error "$repoPath is not an installed Product-deep-dive git repository. Run the install command first."
  exit 1
}
Set-Location $repoPath
git pull --ff-only
New-Item -ItemType Directory -Force -Path $skillPath | Out-Null
Copy-Item -Path "$repoPath\product-deep-dive\*" -Destination $skillPath -Recurse -Force
```

Restart Codex or Claude Code after updating.

---

## Troubleshooting

### The skill does not trigger

Make sure the request contains both:

- AI product deep-dive intent.
- Feishu document output intent.

Recommended wording:

```text
Help me deeply analyze XXX AI product and output a Feishu document.
```

### Feishu document creation fails

Check:

- `lark-cli auth status` works.
- `lark-cli docs +create --api-version v2 --help` works.
- User authentication is complete.
- The current identity is `user`, not `bot`.
- If a command returns a missing-scope hint, authorize that exact scope and retry.

### Architecture diagrams are not editable

Check:

- The document contains `<whiteboard token=...>`, not image blocks.
- Feishu whiteboard scopes are granted.
- Labels are explicit native editable text nodes, not SVG text or shape-only text.
- Raw-node query can find required labels.
- Exported preview images visibly display text.

---

## License

This repository includes a [`LICENSE`](LICENSE) file. See that file for details.
