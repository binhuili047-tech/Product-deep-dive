# Technical Inference Confidence

Use this reference when writing section 9 `技术层拆解`, section 10 `模型层拆解`, section 11 `不确定性处理`, or any paragraph that reverse-engineers Workflow, Agent, Multi-Agent, RAG, model routing, data pipelines, tools, plugins, or prompt structures.

## Core Principle

Technical teardown should be useful without pretending to know private implementation. The goal is to make plausible product-manager inferences while preserving evidence boundaries.

Every technical inference should answer:

- `看到什么`: visible product behavior, public documentation, error message, UI state, latency pattern, output pattern, or official disclosure.
- `推测什么`: the likely workflow, component, model capability, tool, state object, or data process.
- `为什么这么推`: reasoning chain from visible evidence to inference.
- `产品价值影响`: how the inferred mechanism changes user experience, cost/efficiency, reliability/trust, retention, or monetization.
- `置信度`: high / medium / low.
- `如何验证`: the next test, source, screenshot, network trace, docs, or interview needed to confirm it.

## Confidence Scale

| Confidence | Use When | Wording |
|---|---|---|
| High | Official docs disclose the mechanism, or repeated product behavior strongly supports one interpretation. | `可以较高置信判断...` |
| Medium | Multiple visible signals point to the same hypothesis, but no official confirmation exists. | `更可能是...` / `从体验看，可能采用...` |
| Low | The idea is a plausible architecture guess with weak evidence or many alternatives. | `一种可能的解释是...` / `仍需验证...` |

Never use high confidence only because a product is in an AI category. Category labels such as Agent, RAG, Multi-Agent, or workflow automation are not evidence by themselves.

## Evidence Types

| Evidence Type | Examples | Strength |
|---|---|---|
| Official disclosure | Docs, release notes, pricing page, API docs, security docs, model card, public interview. | Strong |
| Visible product behavior | UI steps, generated outputs, wait states, retries, tool panels, citations, memory recall. | Medium |
| Repeated test pattern | Multiple tests showing stable routing, failure mode, latency, or recovery behavior. | Medium |
| Public ecosystem signal | Integrations, SDKs, plugin pages, app store metadata, job postings, blog posts. | Medium/Low |
| Pure analogy | Similar products usually do X. | Low |

## Required Inference Table

For technical and model-layer reverse engineering, prefer this table:

```markdown
| 推测对象 | 看到什么 | 可能机制 | 产品价值影响 | 置信度 | 为什么这么推 | 如何验证 | 风险/Badcase |
|---|---|---|---|---|---|---|---|
| Workflow / Agent | ... | ... | ... | 中 | ... | ... | ... |
| RAG / 数据 grounding | ... | ... | ... | 低 | ... | ... | ... |
| 模型路由 | ... | ... | ... | 中 | ... | ... | ... |
```

## Product Value Impact

Reverse engineering is incomplete if it only names architecture. A senior AIPM teardown must explain why the inferred mechanism matters to the product.

For every important technical inference, add product-value impact:

| 技术机制 | 影响用户体验 | 影响成本/效率 | 影响可靠性/信任 | 影响留存/商业化 | 置信度 |
|---|---|---|---|---|---|
| Workflow / pipeline | Does it shorten time-to-value, make progress legible, or constrain complex tasks? | Does it reduce repeated model calls or increase orchestration overhead? | Does it make failures recoverable or hide failure causes? | Does it support repeatable jobs, templates, or paid advanced flows? | 中 |
| RAG / grounding | Does it improve factuality, personalization, or controllability? | Does retrieval add latency/storage cost? | Are sources visible enough to build trust? | Does uploaded knowledge create switching cost or enterprise value? | 低-中 |
| Model routing | Does it match tasks to the right output quality and modality? | Does it lower average cost or introduce routing overhead? | Can wrong routing cause inconsistent quality? | Does tiered quality support pricing, credits, or upsell? | 中 |

If no product-value impact can be articulated, either the inference is not important enough for the teardown or the analysis is still too technical and not product-manager useful.

## Workflow vs Agent vs Multi-Agent

Use these distinctions:

| Architecture Label | Stronger Evidence Needed | Weak Signals Are Not Enough |
|---|---|---|
| Workflow | Repeated fixed steps, deterministic stages, template-like pipeline, visible progress states. | A multi-step UI alone does not prove a backend workflow engine. |
| Single Agent | Goal-directed loop, tool selection, planning/replanning, stateful execution around one task owner. | Chat + tools alone does not prove an autonomous agent. |
| Multi-Agent | Distinct specialized roles, handoffs, parallel/subtask behavior, role-specific outputs, public docs mentioning agents. | Multiple functions or tabs do not prove multi-agent architecture. |
| Tool-Using Assistant | Tool calls are visible or strongly implied, but autonomy and role specialization are unclear. | Do not call this Multi-Agent unless specialization is visible. |

When uncertain, write:

```markdown
从可见体验看，它更像是「Workflow + Tool-Using Assistant」而不是强自主 Multi-Agent；是否存在多个内部 Agent 仍需通过更多任务日志或官方说明验证。
```

## RAG / Knowledge / Memory Inference

Do not claim RAG just because the product answers with facts.

| Claim | Evidence Needed |
|---|---|
| RAG | Citations, document upload retrieval, source snippets, knowledge-base configuration, repeatable grounding to provided docs. |
| Long-term memory | Cross-session recall, memory settings, saved user profile, visible memory updates. |
| Context window use | Recent conversation/file content affects output without durable recall. |
| Personalization | User history, preferences, projects, or assets shape future outputs. |
| Style library | Visible presets, saved style profiles, reusable templates, brand kits. |

If evidence is thin, say `可能存在检索增强或上下文注入机制` rather than `接了 RAG`.

## Model Routing Inference

Model routing is often invisible. Use cautious language.

| Signal | Possible Inference | Confidence |
|---|---|---|
| Different output modes with different latency/quality | Task-specific model routing or pipeline stages | Medium |
| Official model names in UI/docs | Disclosed model selection | High |
| Pricing differs by generation type | Cost-based routing or model tiering | Medium |
| Output modality switches text/image/video/voice | Multi-model orchestration | Medium |
| No visible evidence | Unknown | Low |

Avoid naming a specific proprietary model unless the product or provider discloses it.

## Model Commoditization and Product Moat

Model capability is often borrowed infrastructure. Do not treat strong model output as product moat unless the product converts it into owned value.

Ask:

- Is the capability external commodity model performance, or something the product owns through workflow, data, context, distribution, assets, community, integrations, or UX lock-in?
- If the underlying model improves for everyone, does the product's advantage expand, stay flat, or disappear?
- Does the product accumulate user projects, preferences, style libraries, prompt assets, evaluation data, or feedback that improves the next experience?
- Does model routing reduce cost/latency enough to create pricing flexibility or better margins?
- Could a platform owner, foundation model provider, or distribution channel copy the core experience quickly?

Use this table when writing model-layer judgment:

```markdown
| 模型能力 | 产品如何使用 | 是否商品化风险 | 产品自有价值 | 护城河强度 | 待验证 |
|---|---|---|---|---|---|
| 意图理解 | ... | 高/中/低 | Workflow / 数据 / 分发 / 资产 / 社区 / 无明显自有价值 | 强/中/弱 | ... |
```

## Prompt Reconstruction Rules

Only reconstruct prompts as product-manager hypotheses.

Allowed wording:

- `可能的提示词结构`
- `根据输入输出可以反推的指令框架`
- `用于理解产品设计的 prompt-like hypothesis`

Forbidden wording:

- `它的真实系统提示词是`
- `内部 prompt 如下`
- `可以确定它用了这个 prompt`

Prompt reconstruction should include:

```markdown
### 可能的提示词结构
- Role:
- Inputs:
- Constraints:
- Tools:
- Output format:
- Safety rules:
- Badcase handling:

### 置信度
- 置信度：
- 依据：
- 待验证：
```

## Badcase Analysis

Every technical inference should ask what can break:

| Area | Badcase Examples |
|---|---|
| Workflow | Step skipped, state lost, task restarts from scratch, user cannot resume. |
| Agent/tool use | Wrong tool, permission failure, unbounded action, weak recovery. |
| RAG/data | Stale sources, irrelevant retrieval, citation mismatch, private data leakage. |
| Model routing | Wrong model for task, inconsistent quality, high latency, cost spike. |
| Memory/context | Wrong user preference, outdated memory, over-personalization, context pollution. |
| Safety | Unsafe content generation, over-refusal, copyright risk, prompt injection. |

## Writing Pattern

Use this structure when the section contains non-trivial technical inference:

```markdown
### 技术反推总览
一句话说明：这是事实、观察、推测还是判断混合分析。

| 推测对象 | 看到什么 | 可能机制 | 产品价值影响 | 置信度 | 为什么这么推 | 如何验证 | 风险/Badcase |
|---|---|---|---|---|---|---|---|
| ... | ... | ... | ... | 中 | ... | ... | ... |

### 关键判断
- 较高置信：
- 中等置信：
- 低置信 / 待验证：
```

## Common Mistakes

- Calling any AI workflow `Multi-Agent` without visible role specialization.
- Calling any factual answer `RAG` without source grounding evidence.
- Naming a specific model without official disclosure.
- Presenting prompt reconstruction as real internal prompt.
- Treating model capability as product moat without explaining owned workflow, data, context, distribution, assets, or UX lock-in.
- Describing a technical mechanism without explaining its product-value impact.
- Ignoring badcases after proposing a plausible architecture.
- Omitting `如何验证`, which leaves the reader with no way to close the evidence gap.
