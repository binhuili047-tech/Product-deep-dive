# Product Deep Dive Skill / AI 产品深度拆解 Skill

> Build Feishu-ready AI product teardown documents with product-manager depth, evidence discipline, high-value questions, and editable architecture whiteboards.
>
> 用产品经理视角深度拆解 AI 产品，并直接输出可落地的飞书文档：包含证据分层、高价值问题、测试框架、商业/市场/技术/模型拆解，以及可编辑架构画板。

---

## English

### What Is This?

`product-deep-dive` is a Codex skill for creating long-form AI product teardown documents in Feishu/Lark Docs.

It is designed for cases where the user explicitly wants to deeply analyze an AI product and deliver the result as a Feishu document. It does not trigger for casual mentions of AI, agents, RAG, LLMs, SaaS, or product names.

The skill helps an AI product manager move beyond feature summaries and produce a structured teardown across positioning, scenarios, evaluation, market, business, user flows, application architecture, model routing, uncertainty handling, data foundations, and final architecture diagrams.

### Key Capabilities

- Creates Feishu/Lark document-style long-form product teardown articles.
- Uses a fixed 13-section deep-dive structure with a `核心结论` section before the main chapters.
- Generates 3-8 product-specific high-value questions for every numbered section.
- Adds product-manager insights as Feishu callout/highlight blocks.
- Builds concrete evaluation tables for product testing scenarios.
- Separates evidence into facts, observations, inferences, judgments, and verification gaps.
- Creates six-layer architecture views:
  - 市场层
  - 商业层
  - 用户层
  - 应用层
  - 模型层
  - 基础层
- Creates one final architecture diagram plus per-layer mini diagrams.
- Prefers editable Feishu whiteboards over static PNG/SVG images.
- Applies polished Feishu table formatting: first row and first column use gray background and bold text.

### When To Use

Use this skill when both are true:

1. The user asks for a deep teardown, deep analysis, evaluation framework, or structured framework for an AI product.
2. The user wants the output as a Feishu document, Feishu cloud document, or Feishu-style long-form teardown.

Do not use it for:

- General AI product Q&A.
- Short product opinions.
- Product recommendations.
- Coding tasks.
- Brainstorming without a Feishu document deliverable.
- Any conversation that merely mentions AI, Agent, RAG, Multi-Agent, LLM, SaaS, or AIGC.

### Installation

Clone this repository directly into your Codex skills directory:

```powershell
git clone https://github.com/<your-github-username>/product-deep-dive-skill.git "$env:USERPROFILE\.codex\skills\product-deep-dive"
```

Or copy the folder manually:

```powershell
New-Item -ItemType Directory -Force "$env:USERPROFILE\.codex\skills\product-deep-dive"
Copy-Item -Recurse -Force ".\*" "$env:USERPROFILE\.codex\skills\product-deep-dive\"
```

Restart Codex after installation so the skill index can reload.

### Requirements

For full Feishu document delivery:

- Codex skills support.
- `lark-cli` configured and authenticated.
- Feishu/Lark document create/update permissions.
- Optional but recommended: Feishu whiteboard permissions for editable architecture diagrams.
- Optional but recommended: `@larksuite/whiteboard-cli` for SVG-to-whiteboard conversion.

The skill can still produce a structured draft when Feishu or whiteboard access is unavailable, but the intended output is a real Feishu document.

### Example Prompts

```text
现在我要拆解星野产品，帮我进行框架搭建，并输出飞书文档
```

```text
帮我对这个 AI Agent 产品做深度拆解，最终写入飞书文档：https://example.com
```

```text
直接写一篇飞书文档型产品经理拆解文章，产品是 XXX
```

### Output Structure

The skill uses this default structure:

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

It also adds:

- 产品基础信息
- 核心结论
- 信息缺口清单

### Feishu Formatting Rules

The final document should be clean enough for team sharing:

- High-value questions use blockquote panels.
- Product-manager insights use Feishu callout blocks.
- Tables use gray-background bold headers for both the first row and first column.
- Architecture diagrams are inserted as editable whiteboards when possible.
- The final architecture uses six vertical layers from top to bottom, with 基础层 at the bottom.

### Repository Structure

```text
product-deep-dive/
  README.md
  SKILL.md
  evals/
```

### Notes

This skill is opinionated. It is optimized for AI product-manager teardown work, not generic product research. Its default behavior is to create or update a Feishu document directly when the user asks for a Feishu deliverable.

---

## 中文

### 这是什么？

`product-deep-dive` 是一个 Codex Skill，用于帮助 AI 产品经理对 AI 产品进行深度拆解，并直接输出为飞书云文档。

它适用于用户明确提出“对 AI 产品进行深度拆解/深度分析/框架搭建，并输出飞书文档”的场景。它不会因为对话中随便出现 AI、Agent、RAG、LLM、SaaS、AIGC 或产品名就自动触发。

这个 skill 的核心目标不是复述功能，而是帮助产品经理从真实体验出发，拆出产品定位、用户场景、评估体系、市场机会、商业逻辑、用户路径、应用架构、模型路由、不确定性处理、基础数据层和最终架构图。

### 核心能力

- 生成飞书文档型长文产品拆解。
- 默认使用 13 章深度拆解结构，并在 13 章前增加 `核心结论`。
- 每个编号章节生成 3-8 个与具体产品相关的高价值问题。
- 每节末尾用飞书高亮块输出 `产品经理启发`。
- 针对具体测试场景生成评估表和权重表。
- 区分事实、观察、推测、判断和待验证信息。
- 使用六层产品架构视角：
  - 市场层
  - 商业层
  - 用户层
  - 应用层
  - 模型层
  - 基础层
- 生成最终架构图，并在对应章节下生成分层小图。
- 优先使用可编辑飞书画板，而不是静态 PNG/SVG 图片。
- 所有飞书表格默认进行样式优化：第一行和第一列灰底加粗。

### 什么时候使用？

只有同时满足以下两个条件时才使用：

1. 用户要对某个 AI 产品做深度拆解、深度分析、评估框架或结构化框架搭建。
2. 用户希望最终输出为飞书文档、飞书云文档，或飞书文档型长文拆解。

不要在以下场景使用：

- 普通 AI 产品问答。
- 简短产品观点。
- 产品推荐。
- 编程任务。
- 不要求飞书文档交付的头脑风暴。
- 只是提到了 AI、Agent、RAG、Multi-Agent、LLM、SaaS 或 AIGC。

### 安装方式

将仓库直接 clone 到 Codex skills 目录：

```powershell
git clone https://github.com/<your-github-username>/product-deep-dive-skill.git "$env:USERPROFILE\.codex\skills\product-deep-dive"
```

或者手动复制：

```powershell
New-Item -ItemType Directory -Force "$env:USERPROFILE\.codex\skills\product-deep-dive"
Copy-Item -Recurse -Force ".\*" "$env:USERPROFILE\.codex\skills\product-deep-dive\"
```

安装后重启 Codex，让 skill 索引重新加载。

### 依赖

如果要完整输出飞书文档，需要：

- Codex skills 支持。
- 已配置并登录的 `lark-cli`。
- 飞书文档创建/更新权限。
- 推荐开通飞书画板权限，用于写入可编辑架构图。
- 推荐安装或允许运行 `@larksuite/whiteboard-cli`，用于 SVG 转飞书画板节点。

如果飞书或画板权限不可用，skill 仍可生成结构化草稿，但它的默认目标是创建真实飞书文档。

### 示例 Prompt

```text
现在我要拆解星野产品，帮我进行框架搭建，并输出飞书文档
```

```text
帮我对这个 AI Agent 产品做深度拆解，最终写入飞书文档：https://example.com
```

```text
直接写一篇飞书文档型产品经理拆解文章，产品是 XXX
```

### 默认输出结构

默认使用以下结构：

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

同时会增加：

- 产品基础信息
- 核心结论
- 信息缺口清单

### 飞书排版规范

最终文档应能直接用于团队分享：

- 高价值问题使用引用块展示。
- 产品经理启发使用飞书高亮块展示。
- 所有表格的第一行和第一列使用灰底加粗。
- 架构图尽量使用可编辑飞书画板。
- 最终架构图按照六层从上到下排列，基础层固定在最底部。

### 仓库结构

```text
product-deep-dive/
  README.md
  SKILL.md
  evals/
```

### 说明

这个 skill 是强观点型的。它不是通用产品研究模板，而是面向 AI 产品经理的深度拆解工作流。默认行为是在用户提出飞书文档交付时，直接创建或更新飞书文档。

