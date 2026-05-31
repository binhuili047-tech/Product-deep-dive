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

See [`../CHANGELOG.md`](../CHANGELOG.md) for the major changes made during the skill-building process. / 重要修改记录见 [`../CHANGELOG.md`](../CHANGELOG.md)。

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

It builds scenario-specific scoring tables covering:

- Result quality.
- Process quality.
- Aha Moment.
- Friction points.
- Safety and uncertainty handling.
- Business value.

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

### 适用场景

适合这些请求：

```text
现在我要拆解星野产品，帮我进行框架搭建，并输出飞书文档
```

```text
我要对某个 AI Agent 产品做深度拆解，直接生成飞书文档
```

```text
帮我写一篇飞书文档型 AI 产品经理拆解文章
```

不适合这些请求：

- 只问一个 AI 产品是什么。
- 只要几句话观点。
- 只做产品推荐。
- 只讨论 Agent/RAG/LLM 概念。
- 不需要飞书文档交付。

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

### 飞书排版规范

文档默认面向团队分享，因此会要求：

- 高价值问题放在引用块中。
- 产品经理启发放在飞书高亮块中。
- 表格第一行和第一列灰底加粗。
- 架构图优先使用可编辑飞书画板。
- 最终架构图按照 `市场层 -> 商业层 -> 用户层 -> 应用层 -> 模型层 -> 基础层` 从上到下排布。

### 维护建议

如果你要继续完善这个仓库，建议后续补充：

- `CONTRIBUTING.md`
- 示例飞书文档截图或公开 demo 链接
- 更多 eval cases

---

## License

This repository includes a `LICENSE` file. See `LICENSE` for details.
