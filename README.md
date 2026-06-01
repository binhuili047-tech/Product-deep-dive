# Product Deep Dive Skill

![Codex Skill](https://img.shields.io/badge/Codex-Skill-111827)
![Claude Compatible](https://img.shields.io/badge/Claude-Compatible-6B46C1)
![Feishu/Lark Docs](https://img.shields.io/badge/Feishu%2FLark-Docs-00B96B)
![Whiteboard Ready](https://img.shields.io/badge/Editable-Whiteboards-7B61FF)
![Language](https://img.shields.io/badge/Language-ZH%20%2B%20EN-blue)
![License](https://img.shields.io/github/license/VioletScar-Hui/Product-deep-dive)
![Status](https://img.shields.io/badge/Status-Active-success)

**AI product teardown, packaged as a Feishu/Lark document workflow.**

`product-deep-dive` is a Codex and Claude-compatible skill for AI product managers who want to deeply analyze AI products and deliver polished Feishu/Lark Docs with structured questions, evaluation tables, business/market/user/technical/model analysis, and editable architecture whiteboards.

`product-deep-dive` 是一个同时支持 Codex 和 Claude 的 Skill，面向 AI 产品经理，用于对 AI 产品进行深度拆解，并直接输出为飞书文档型长文：包含高价值问题、测试评估表、市场/商业/用户/技术/模型/基础层拆解，以及可编辑架构画板。

Includes a `LICENSE` file in the GitHub repository. / GitHub 仓库已包含 `LICENSE` 文件。

See [`CHANGELOG.md`](CHANGELOG.md) for the major changes made during the skill-building process. / 重要修改记录见 [`CHANGELOG.md`](CHANGELOG.md)。

---

## Version Highlights

| Version | Focus | What Changed |
|---|---|---|
| v1.5 | Evaluation sub-dimensions | Expanded the testing system with scenario-specific second-level indicators such as end-to-end result, user layer, model/data layer, and technical layer, plus detailed dimension descriptions. |
| v1.4 | Market competitor analysis | Required section 6 to include a 3+ competitor comparison table and a competitive landscape diagram using product-relevant axes. |
| v1.3 | Three-layer evaluation framework | Standardized testing around `端到端` black-box output evaluation, `过程能力` glass-box process and decision-path evaluation, and `综合评测` white-box full-process multidimensional evaluation. |
| v1.2 | Documentation, distribution, and cross-agent support | Added bilingual README onboarding, `lark-cli` prerequisite checks, Codex/Claude Code install paths, license visibility, and versioned changelog navigation. |
| v1.1 | Feishu delivery, whiteboards, and formatting rules | Added Feishu document delivery defaults, editable whiteboard architecture diagrams, strict trigger discipline, dynamic high-value questions, callout rules, and gray/bold table styling. |
| v1.0 | Initial product deep-dive framework | Established the 13-section AI product teardown framework, core conclusions, evidence discipline, information gap checklist, and evaluation coverage. |

See [`CHANGELOG.md`](CHANGELOG.md) for full details.

---

## Required Prerequisite: lark-cli

This skill is built around Feishu/Lark document delivery. Install and configure `lark-cli` before expecting full document creation, update, or whiteboard workflows to work.

Minimum checks:

```powershell
lark-cli --version
lark-cli auth status
lark-cli docs +create --api-version v2 --help
```

If `lark-cli auth status` shows no usable user login, authenticate as a user before running product teardown workflows. When Feishu returns a missing-scope error, follow the scope hint from `lark-cli` and authorize that exact scope.

Optional whiteboard check:

```powershell
npx -y @larksuite/whiteboard-cli@^0.2.10 -v
```

Without `lark-cli`, the skill can still draft a teardown framework in chat, but it cannot reliably create or update Feishu documents.

---

## For AI Agents: Quick Install

If a user asks you to install this skill, first check the Feishu delivery prerequisite:

```powershell
lark-cli --version
lark-cli auth status
```

If `lark-cli` is missing, tell the user to install and configure it before expecting Feishu document output. Then install or update the skill:

For Codex:

```powershell
$repoPath = "$env:USERPROFILE\.codex\skill-repos\Product-deep-dive"
$skillPath = "$env:USERPROFILE\.codex\skills\product-deep-dive"
if (Test-Path $repoPath) {
  Set-Location $repoPath
  git pull
} else {
  git clone https://github.com/VioletScar-Hui/Product-deep-dive.git $repoPath
}
New-Item -ItemType Directory -Force $skillPath | Out-Null
Copy-Item -Path "$repoPath\product-deep-dive\*" -Destination $skillPath -Recurse -Force
```

For Claude Code:

```powershell
$repoPath = "$env:USERPROFILE\.claude\skill-repos\Product-deep-dive"
$skillPath = "$env:USERPROFILE\.claude\skills\product-deep-dive"
if (Test-Path $repoPath) {
  Set-Location $repoPath
  git pull
} else {
  git clone https://github.com/VioletScar-Hui/Product-deep-dive.git $repoPath
}
New-Item -ItemType Directory -Force $skillPath | Out-Null
Copy-Item -Path "$repoPath\product-deep-dive\*" -Destination $skillPath -Recurse -Force
```

Then verify:

```powershell
Test-Path "$env:USERPROFILE\.codex\skills\product-deep-dive\SKILL.md"
Get-Content "$env:USERPROFILE\.codex\skills\product-deep-dive\SKILL.md" -TotalCount 8
```

For Claude Code, verify the same file under `$env:USERPROFILE\.claude\skills\product-deep-dive\SKILL.md`.

Optional Feishu workflow verification:

```powershell
lark-cli docs +create --api-version v2 --help
npx -y @larksuite/whiteboard-cli@^0.2.10 -v
```

Finally, tell the user to restart Codex or Claude Code so the skill index reloads.

---

## Quick Start for Humans

### 1. Prepare lark-cli

Install and log in to `lark-cli` first. Then check:

```powershell
lark-cli --version
lark-cli auth status
lark-cli docs +create --api-version v2 --help
```

For editable architecture whiteboards, also check:

```powershell
npx -y @larksuite/whiteboard-cli@^0.2.10 -v
```

### 2. Install the skill

For Codex:

```powershell
$repoPath = "$env:USERPROFILE\.codex\skill-repos\Product-deep-dive"
$skillPath = "$env:USERPROFILE\.codex\skills\product-deep-dive"
if (Test-Path $repoPath) {
  Set-Location $repoPath
  git pull
} else {
  git clone https://github.com/VioletScar-Hui/Product-deep-dive.git $repoPath
}
New-Item -ItemType Directory -Force $skillPath | Out-Null
Copy-Item -Path "$repoPath\product-deep-dive\*" -Destination $skillPath -Recurse -Force
```

For Claude Code:

```powershell
$repoPath = "$env:USERPROFILE\.claude\skill-repos\Product-deep-dive"
$skillPath = "$env:USERPROFILE\.claude\skills\product-deep-dive"
if (Test-Path $repoPath) {
  Set-Location $repoPath
  git pull
} else {
  git clone https://github.com/VioletScar-Hui/Product-deep-dive.git $repoPath
}
New-Item -ItemType Directory -Force $skillPath | Out-Null
Copy-Item -Path "$repoPath\product-deep-dive\*" -Destination $skillPath -Recurse -Force
```

Restart Codex or Claude Code after installation.

### 3. Ask for a Feishu product teardown

```text
现在我要拆解星野产品，帮我进行框架搭建，并输出飞书文档
```

```text
帮我对这个 AI Agent 产品做深度拆解，最终写入飞书文档：https://example.com
```

```text
直接写一篇飞书文档型产品经理拆解文章，产品是 XXX
```

### 4. Expected result

Codex or Claude Code should create or update a Feishu/Lark document containing:

- A product-manager style long-form teardown.
- A `核心结论` section before the main chapters.
- 13 structured analysis chapters.
- 3-8 high-value questions per numbered chapter.
- Evaluation tables with weighted scoring.
- Product-manager insight callouts.
- Layer mini diagrams and a final architecture diagram.
- A final information gap checklist.

---

## When This Skill Triggers

Use this skill only when both are true:

1. The user asks for a deep teardown, deep analysis, evaluation framework, or structured framework for an AI product.
2. The user wants the output as a Feishu document, Feishu cloud document, or Feishu-style long-form product teardown.

Do not use this skill merely because a conversation mentions:

- AI
- Agent
- AIGC
- RAG
- Multi-Agent
- LLM
- SaaS
- model routing
- product names

If the user only asks a short product question, a recommendation, a coding task, or a brainstorm without Feishu-document delivery, answer normally or use a more specific skill.

---

## What It Produces

The default document structure is:

```text
产品深度拆解：[产品名]

产品基础信息
核心结论

1. 产品定位与体验总结
2. 测试评估体系
3. 测试流程具体截图
4. 差异化定位
5. 能力边界
6. 市场层拆解
7. 商业层拆解
8. 场景/用户层拆解
9. 技术层拆解
10. 模型层拆解
11. 不确定性处理
12. 基础层拆解
13. 最终架构图

信息缺口清单
```

---

## Core Features

### Product Manager Depth

- Converts product experience into positioning, target users, scenarios, and trade-offs.
- Uses product-specific questions instead of generic templates.
- Ends every major section with a reusable product-manager insight.

### Evidence Discipline

The skill separates:

- **Facts**: official websites, screenshots, docs, public materials.
- **Observations**: behavior seen during actual product use.
- **Inferences**: system or workflow assumptions from visible behavior.
- **Judgments**: analyst opinions.
- **To verify**: missing evidence or follow-up tests.

### Testing and Evaluation

It builds scenario-specific scoring tables with three required main dimensions:

| Main Dimension | Evaluation Style | Focus |
|---|---|---|
| 端到端 | Black-box evaluation | Final output, scenario completion, and whether the product solves the user's visible task. |
| 过程能力 | Glass-box evaluation | Intermediate process, decision path, state handling, tool use, interaction recovery, and workflow reliability. |
| 综合评测 | White-box evaluation | Full-process multidimensional assessment across output, process, model orchestration, cost, safety, data, and business value. |

Second-level indicators are generated dynamically under these three main dimensions based on the concrete product and testing scenario. Common second-level families include:

| Second-Level Family | What It Evaluates |
|---|---|
| 端到端结果层 | Final output, scenario completion, delivery completeness, and user-perceived usefulness. |
| 用户层 | Entry point, user path, friction, controllability, trust building, feedback, retention trigger, and Aha Moment. |
| 模型数据层 | Model capability fit, routing, context use, RAG/data grounding, memory, data freshness, personalization, and hallucination risk. |
| 技术层 | Workflow orchestration, agent/tool calls, state management, latency, stability, error recovery, permissions, security, and integrations. |

Each evaluation dimension should explain what it measures, why it matters, and how to score it.

### Market and Competitor Analysis

Section 6 always includes a competitor comparison table covering at least 3 main competitors:

| Column | Purpose |
|---|---|
| 平台/公司 | Identifies the product, company, or platform being compared. |
| 主要角色 | Clarifies whether it is a direct competitor, substitute, platform owner, content ecosystem, tool provider, or adjacent entrant. |
| 分发渠道 | Shows where the product reaches users: app stores, social platforms, web, enterprise sales, creator communities, ecosystem bundles, and so on. |
| 核心商业模式 | Summarizes subscription, usage-based pricing, ads, marketplace take rate, enterprise contracts, traffic conversion, or bundled service logic. |
| 最新公开信息 | Captures the latest verifiable public signal, or marks `待验证` when evidence is incomplete. |

The same section also includes a competitive landscape diagram. The axes are chosen dynamically for the product category, and the analyzed product plus at least 3 competitors are placed on the map.

### Six-Layer Architecture

The final architecture uses six layers:

1. 市场层
2. 商业层
3. 用户层
4. 应用层
5. 模型层
6. 基础层

Each layer can also appear as a mini diagram under its corresponding chapter.

### Feishu/Lark Polish

The document formatting rules include:

- High-value questions as blockquote panels.
- Product-manager insights as Feishu callout blocks.
- Tables with gray-background bold first rows and first columns.
- Editable whiteboards for architecture diagrams when permissions are available.
- No static PNG architecture diagrams when editable whiteboards can be written.

---

## Feishu and Whiteboard Requirements

For full document delivery, `lark-cli` is required. Before running a teardown, verify:

```powershell
lark-cli --version
lark-cli auth status
lark-cli docs +create --api-version v2 --help
```

Required:

- Feishu/Lark user authentication.
- Feishu document create/update permissions.
- User identity when writing to personal cloud documents.

Optional for editable architecture diagrams:

- Feishu whiteboard node read/write scopes.
- `@larksuite/whiteboard-cli` for SVG-to-whiteboard conversion.

The preferred architecture diagram flow is:

```text
structured architecture
  -> coordinate-based SVG
  -> @larksuite/whiteboard-cli OpenAPI nodes
  -> editable Feishu whiteboard
  -> verification in the Feishu document
```

If Feishu access is unavailable, the skill should still produce a useful draft and list missing delivery steps.

---

## Example Use Cases

Use this skill to analyze:

- AI companion products.
- AI Agent products.
- AIGC tools.
- AI social apps.
- AI creator tools.
- AI workflow products.
- Emerging AI applications that need product-manager level teardown.

Good prompt:

```text
现在我要拆解猫箱产品，帮我进行框架搭建，并输出飞书文档
```

Better prompt with target:

```text
我要拆解这个 AI 产品：https://example.com
目标是给团队做产品经理拆解分享，请直接输出飞书文档。
```

---

## Repository Structure

```text
Product-deep-dive/
  README.md          # Bilingual project guide
  CHANGELOG.md       # Notable changes and iteration history
  LICENSE            # Repository license
  docs/
    product-deep-dive-framework-upgrade-brief.md
  product-deep-dive/
    README.md        # Skill-level guide
    SKILL.md         # Codex / Claude-compatible skill instructions
    evals/
      evals.json     # Skill evaluation cases
```

---

## Updating

If you already installed the skill:

For Codex:

```powershell
$repoPath = "$env:USERPROFILE\.codex\skill-repos\Product-deep-dive"
$skillPath = "$env:USERPROFILE\.codex\skills\product-deep-dive"
Set-Location $repoPath
git pull
Copy-Item -Path "$repoPath\product-deep-dive\*" -Destination $skillPath -Recurse -Force
```

For Claude Code:

```powershell
$repoPath = "$env:USERPROFILE\.claude\skill-repos\Product-deep-dive"
$skillPath = "$env:USERPROFILE\.claude\skills\product-deep-dive"
Set-Location $repoPath
git pull
Copy-Item -Path "$repoPath\product-deep-dive\*" -Destination $skillPath -Recurse -Force
```

Restart Codex or Claude Code after updating.

---

## Troubleshooting

### The skill does not trigger

Make sure the user request contains both:

- an AI product deep-dive intent
- a Feishu document output intent

For example:

```text
帮我对 XXX AI 产品做深度拆解，并输出飞书文档
```

### Feishu document creation fails

Check:

- `lark-cli --version` works.
- `lark-cli docs +create --api-version v2 --help` works.
- User authentication is complete.
- The current identity is `user`, not `bot`, when writing to the user's cloud documents.
- The required Feishu document scopes are granted. If a command returns a missing-scope hint, authorize that exact scope and retry.

### Whiteboard diagrams are not editable

Check:

- The document contains `<whiteboard token=...>` blocks, not image blocks.
- Feishu whiteboard scopes are granted.
- SVG diagrams are converted to OpenAPI/raw whiteboard nodes before writing when exact editability is required.

---

## 中文说明

### 这是什么？

`product-deep-dive` 是一个同时支持 Codex 和 Claude Code 的 AI 产品深度拆解 Skill。它会引导 AI 产品经理从真实体验出发，拆解产品定位、测试评估、关键路径、差异化、能力边界、市场、商业、用户、技术、模型、基础数据和最终架构图，并默认输出为飞书文档。

它的重点不是“复述功能”，而是把一个 AI 产品拆成可讨论、可复盘、可学习、可迁移的产品分析框架。

### 版本更新摘要

| 版本 | 重点 | 更新内容 |
|---|---|---|
| v1.5 | 评测二级指标细化 | 在三大主维度下增加场景化二级指标要求，例如端到端结果层、用户层、模型数据层、技术层，并要求对每个维度写清楚评什么、为什么重要、怎么评。 |
| v1.4 | 市场竞品分析增强 | 要求市场层固定加入至少 3 个主要竞品的对比表，并基于产品相关坐标轴绘制竞争格局图。 |
| v1.3 | 测试评估体系升级 | 将测试场景主维度固定为“端到端、过程能力、综合评测”，从黑盒结果评测扩展到玻璃盒过程/决策路径评测，再到白盒全流程多维综合评估。 |
| v1.2 | 文档化、分发和跨 Agent 支持 | 补充双语 README、`lark-cli` 前置条件、Codex/Claude Code 安装路径、LICENSE 展示、版本化 Changelog 和安装结构修正。 |
| v1.1 | 飞书交付、可编辑画板和排版规则 | 增加飞书文档默认创建/更新、可编辑飞书白板架构图、严格触发条件、动态高价值问题、产品经理启发高亮块和表格灰底加粗规则。 |
| v1.0 | 初始产品拆解框架 | 建立 13 章 AI 产品深度拆解框架、核心结论、证据分层、信息缺口清单和基础 eval 覆盖。 |

完整记录见 [`CHANGELOG.md`](CHANGELOG.md)。

### 适用场景

只有同时满足以下两个条件时才应该触发这个 skill：

1. 用户要对某个 AI 产品做深度拆解、深度分析、评估框架或结构化框架搭建。
2. 用户希望最终输出为飞书文档、飞书云文档，或飞书文档型长文拆解。

适合的请求示例：

```text
现在我要拆解星野产品，帮我进行框架搭建，并输出飞书文档
```

```text
我要对某个 AI Agent 产品做深度拆解，直接生成飞书文档
```

```text
帮我写一篇飞书文档型 AI 产品经理拆解文章
```

不适合的请求：

- 只问一个 AI 产品是什么。
- 只要几句话观点。
- 只做产品推荐。
- 只讨论 Agent/RAG/LLM 概念。
- 不需要飞书文档交付。
- 只是提到了 AI、Agent、RAG、LLM、SaaS、AIGC 或某个产品名。

如果意图不明确，应该先问一句：`你是想生成一篇飞书文档型 AI 产品深度拆解吗？`

### 前置条件：lark-cli

这个 skill 的目标产物是飞书文档，因此完整使用前需要先安装并登录 `lark-cli`：

```powershell
lark-cli --version
lark-cli auth status
lark-cli docs +create --api-version v2 --help
```

如果 `lark-cli` 没有登录用户身份，先完成用户授权；如果飞书命令返回缺少 scope，按命令提示授权对应 scope 后重试。

如需生成可编辑架构画板，建议额外检查：

```powershell
npx -y @larksuite/whiteboard-cli@^0.2.10 -v
```

### 安装

Codex:

```powershell
$repoPath = "$env:USERPROFILE\.codex\skill-repos\Product-deep-dive"
$skillPath = "$env:USERPROFILE\.codex\skills\product-deep-dive"
if (Test-Path $repoPath) {
  Set-Location $repoPath
  git pull
} else {
  git clone https://github.com/VioletScar-Hui/Product-deep-dive.git $repoPath
}
New-Item -ItemType Directory -Force $skillPath | Out-Null
Copy-Item -Path "$repoPath\product-deep-dive\*" -Destination $skillPath -Recurse -Force
```

Claude Code:

```powershell
$repoPath = "$env:USERPROFILE\.claude\skill-repos\Product-deep-dive"
$skillPath = "$env:USERPROFILE\.claude\skills\product-deep-dive"
if (Test-Path $repoPath) {
  Set-Location $repoPath
  git pull
} else {
  git clone https://github.com/VioletScar-Hui/Product-deep-dive.git $repoPath
}
New-Item -ItemType Directory -Force $skillPath | Out-Null
Copy-Item -Path "$repoPath\product-deep-dive\*" -Destination $skillPath -Recurse -Force
```

安装后重启 Codex 或 Claude Code。

### 第一次成功运行

安装完成后，可以直接对 Codex 或 Claude Code 说：

```text
现在我要拆解星野产品，帮我进行框架搭建，并输出飞书文档
```

正常情况下，Agent 应该：

1. 检索或读取产品公开资料。
2. 生成飞书文档型产品拆解结构。
3. 在没有目标文档 URL 时创建新的飞书文档。
4. 在文档中写入核心结论、13 章正文、表格、分层架构图和信息缺口清单。
5. 最终只返回简短确认和飞书文档链接。

### 输出内容

默认生成：

- 产品基础信息。
- 核心结论。
- 13 章产品深度拆解。
- 每节 3-8 个高价值问题。
- 产品经理启发高亮块。
- 测试评估表。
- 分层架构小图。
- 最终六层架构图。
- 信息缺口清单。

默认结构为：

```text
产品深度拆解：[产品名]

产品基础信息
核心结论

1. 产品定位与体验总结
2. 测试评估体系
3. 测试流程具体截图
4. 差异化定位
5. 能力边界
6. 市场层拆解
7. 商业层拆解
8. 场景/用户层拆解
9. 技术层拆解
10. 模型层拆解
11. 不确定性处理
12. 基础层拆解
13. 最终架构图

信息缺口清单
```

### 核心能力

#### 产品经理深度

- 从可见体验反推产品定位、核心用户、使用场景和产品取舍。
- 不使用固定模板硬套问题，而是根据具体产品动态改写高价值问题。
- 每个关键章节都输出可复用的产品经理启发，帮助沉淀方法论。

#### 证据分层

文档会尽量区分：

- **事实**：官网、截图、公开资料、官方文档中明确可见的内容。
- **观察**：真实体验路径中看到的行为。
- **推测**：基于体验和产品形态反推的系统、流程或技术判断。
- **判断**：分析者的产品观点。
- **待验证**：缺少资料、需要后续实测或访谈确认的内容。

#### 测试评估

Skill 会先固定三个主维度，再根据具体产品和测试场景生成二级指标，而不是复用固定权重：

| 主维度 | 评测视角 | 关注重点 |
|---|---|---|
| 端到端 | 黑盒评测 | 仅关注最终输出结果、任务完成度，以及用户是否拿到了可用结果。 |
| 过程能力 | 玻璃盒评测 | 关注中间过程、状态变化、工具调用、决策路径、交互恢复和流程稳定性。 |
| 综合评测 | 白盒评测 | 从全流程、多维度综合评估输出质量、过程质量、模型编排、成本、安全、数据沉淀和商业价值。 |

二级指标会根据具体场景动态生成，例如角色陪伴、AI Agent、AI 视频生成、AI 搜索、AI 编程等场景会有不同的任务完成度、可控性、稳定性、成本、安全和留存指标。常见二级指标族包括：

| 二级指标族 | 主要评估内容 |
|---|---|
| 端到端结果层 | 最终输出、任务完成度、交付完整性、用户感知可用性。 |
| 用户层 | 入口、路径、摩擦、控制感、信任建立、反馈机制、留存触发点和 Aha Moment。 |
| 模型数据层 | 模型能力匹配、模型路由、上下文使用、RAG/数据 grounding、记忆、数据新鲜度、个性化和幻觉风险。 |
| 技术层 | Workflow 编排、Agent/工具调用、状态管理、延迟、稳定性、异常恢复、权限、安全和集成深度。 |

每个维度都需要写清楚：`评什么`、`为什么重要`、`怎么评`，避免只给分数不解释评估逻辑。

#### 市场与竞品分析

市场层会固定加入主要竞品对比表，至少覆盖 3 个主要竞品。表格维度包括：

| 维度 | 说明 |
|---|---|
| 平台/公司 | 对比对象，可以是产品、公司、平台或生态入口。 |
| 主要角色 | 判断它是直接竞品、替代方案、平台方、内容生态、工具提供商还是相邻入局者。 |
| 分发渠道 | 说明产品主要通过 App Store、Web、社交平台、企业销售、创作者社区、生态捆绑等方式触达用户。 |
| 核心商业模式 | 拆解订阅、按量付费、广告、交易抽成、企业合同、流量转化或捆绑服务等变现逻辑。 |
| 最新公开信息 | 只写可验证的公开信息；证据不足时标记为 `待验证` 并进入信息缺口清单。 |

市场层还会绘制竞争格局图。坐标轴不固定，会根据具体赛道选择，例如工具属性/情感内容属性、轻量娱乐/高生产力、封闭生态/开放生态、低门槛/高专业度等，并把被拆解产品和至少 3 个竞品放入图中。

#### 六层架构

最终架构图默认使用六层：

1. 市场层
2. 商业层
3. 用户层
4. 应用层
5. 模型层
6. 基础层

每一层会尽量在对应章节下生成小图，最后再生成一张总架构图。

### 飞书排版规范

文档默认面向团队分享，因此会要求：

- 高价值问题放在引用块中。
- 产品经理启发放在飞书高亮块中。
- 表格第一行和第一列灰底加粗。
- 架构图优先使用可编辑飞书画板。
- 最终架构图按照 `市场层 -> 商业层 -> 用户层 -> 应用层 -> 模型层 -> 基础层` 从上到下排布。

### 飞书与画板依赖

完整飞书文档交付需要：

- 已安装 `lark-cli`。
- 已完成飞书/Lark 用户身份登录。
- 具备飞书文档创建/更新权限。
- 当需要写入可编辑架构图时，建议开通飞书画板节点读写权限。
- 当需要把 SVG 转成可编辑白板节点时，建议允许运行 `@larksuite/whiteboard-cli`。

推荐的架构图写入流程是：

```text
结构化架构内容
  -> 坐标化 SVG
  -> @larksuite/whiteboard-cli 转 OpenAPI 节点
  -> 写入可编辑飞书白板
  -> 检查文档中是否为 <whiteboard token=...>
```

如果飞书权限不可用，skill 仍然可以生成结构化草稿，但无法可靠创建或更新飞书文档。

### 示例场景

适合用来分析：

- AI 陪伴产品。
- AI Agent 产品。
- AIGC 工具。
- AI 社交产品。
- AI 创作者工具。
- AI Workflow 产品。
- 需要产品经理视角深度拆解的新兴 AI 应用。

更好的 prompt 示例：

```text
我要拆解这个 AI 产品：https://example.com
目标是给团队做产品经理拆解分享，请直接输出飞书文档。
```

### 更新方式

Codex：

```powershell
$repoPath = "$env:USERPROFILE\.codex\skill-repos\Product-deep-dive"
$skillPath = "$env:USERPROFILE\.codex\skills\product-deep-dive"
Set-Location $repoPath
git pull
Copy-Item -Path "$repoPath\product-deep-dive\*" -Destination $skillPath -Recurse -Force
```

Claude Code：

```powershell
$repoPath = "$env:USERPROFILE\.claude\skill-repos\Product-deep-dive"
$skillPath = "$env:USERPROFILE\.claude\skills\product-deep-dive"
Set-Location $repoPath
git pull
Copy-Item -Path "$repoPath\product-deep-dive\*" -Destination $skillPath -Recurse -Force
```

更新后重启 Codex 或 Claude Code。

### 常见问题

#### Skill 没有触发

确认请求中同时包含：

- AI 产品深度拆解意图。
- 飞书文档输出意图。

推荐说法：

```text
帮我对 XXX AI 产品做深度拆解，并输出飞书文档
```

#### 飞书文档创建失败

检查：

- `lark-cli --version` 是否可用。
- `lark-cli docs +create --api-version v2 --help` 是否可用。
- 是否已完成用户身份授权。
- 当前身份是否为 `user`，而不是只能访问机器人资源的 `bot`。
- 如果命令返回缺少 scope，按提示授权对应 scope 后重试。

#### 架构图不是可编辑画板

检查：

- 文档里是否是 `<whiteboard token=...>`，而不是图片块。
- 飞书画板权限是否已授权。
- SVG 是否已经通过 `whiteboard-cli` 转为 OpenAPI/raw 节点后写入。

### 仓库结构

```text
Product-deep-dive/
  README.md
  CHANGELOG.md
  LICENSE
  product-deep-dive/
    README.md
    SKILL.md
    evals/
      evals.json
```

### 维护建议

如果你要继续完善这个仓库，建议后续补充：

- `CONTRIBUTING.md`
- 示例飞书文档截图或公开 demo 链接
- 更多 eval cases
- 根据 [`docs/product-deep-dive-framework-upgrade-brief.md`](docs/product-deep-dive-framework-upgrade-brief.md) 推进 v2.0 模块化升级

---

## License

This repository includes a `LICENSE` file. See `LICENSE` for details.
