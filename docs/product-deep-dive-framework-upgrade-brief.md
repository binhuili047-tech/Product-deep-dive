# Product Deep Dive Framework Upgrade Brief

BMAD-style analysis and planning document for improving `product-deep-dive`.

生成日期：2026-06-01

## 1. Executive Summary

`product-deep-dive` 已经从一个简单的 AI 产品拆解模板，进化成一个面向飞书文档交付的产品经理分析工作流。当前框架的核心优势是：触发条件明确、13 章结构稳定、支持飞书文档输出、支持可编辑白板架构图、具备证据分层意识，并且已经把测试评估、市场竞品、架构图排版等关键规则写入 skill。

下一阶段不应该继续简单堆规则，而应该把它升级为一个更模块化、更可验证、更可迁移的分析系统。BMAD 视角下，本次升级目标是：

- 把 13 章从“章节清单”升级为“章节契约”。
- 把问题库从“静态问题列表”升级为“场景化问题生成器”。
- 把测试评估体系从“评分表规则”升级为“rubric library”。
- 把飞书输出从“能写入”升级为“能被检查、能稳定复现”。
- 把 evals 从“少量行为检查”升级为“覆盖核心退化风险的回归集”。

建议将本轮升级定义为 `v2.0` 规划，不直接替换现有框架，而是在保持现有触发纪律和飞书交付能力的基础上，逐步拆分、细化、验证。

## 2. BMAD Project Framing

| Item | Recommendation |
|---|---|
| Project type | Skill / documentation-driven workflow |
| BMAD level | Level 2：中等规模功能集升级 |
| Primary users | AI 产品经理、产品研究者、创业团队、AI 产品复盘者 |
| Primary output | 飞书文档型 AI 产品深度拆解长文 |
| Upgrade mode | Analysis -> Planning -> Solutioning -> Implementation |
| Success definition | 生成结果更深、更稳定、更可验证，同时不牺牲触发纪律和交付效率 |

## 3. Analyst Diagnosis

### 3.1 Current Strengths

| Area | Strength | Why It Matters |
|---|---|---|
| Trigger discipline | 只有用户明确要求 AI 产品深度拆解并输出飞书文档时才触发 | 避免把普通 AI 问答误导成重型文档工作流 |
| Feishu delivery | 默认创建或更新飞书文档 | 直接符合用户真实使用场景，不停留在聊天草稿 |
| 13-section framework | 覆盖定位、评估、体验、差异化、能力边界、市场、商业、用户、技术、模型、基础层和架构图 | 保证拆解文章有完整骨架 |
| High-value questions | 每节 3-8 个动态问题 | 让输出更像产品经理分析，而不是资料搬运 |
| Evidence discipline | 区分事实、观察、推测、判断、待验证 | 降低 hallucination 风险 |
| Evaluation system | 已建立端到端、过程能力、综合评测三层主维度 | 从结果评估扩展到过程和系统评估 |
| Architecture diagrams | 支持六层架构和可编辑飞书白板 | 输出形态更接近团队可复用文档 |

### 3.2 Main Gaps

| Gap | Current Symptom | Impact |
|---|---|---|
| `SKILL.md` 过于集中 | 触发规则、章节结构、问题库、评测体系、飞书排版、白板逻辑都堆在一个文件里 | 后续维护成本上升，模型加载后容易遗漏某些细则 |
| 13 章没有章节契约 | 每章有问题库，但没有明确输入、分析动作、输出物、验收标准 | 章节深度不稳定，容易出现“看起来完整但分析浅” |
| 产品类型分支不足 | AI 陪伴、AI Agent、AI 视频、AI 搜索、AI 编程等共用同一套结构 | 难以针对不同产品形态生成足够尖锐的问题和评测指标 |
| eval 覆盖不足 | 当前 evals 主要覆盖触发、飞书创建、架构图、基础结构 | v1.4 竞品表、v1.5 二级指标、表格样式、白板可编辑性等缺少明确回归用例 |
| 输出质量缺少反例 | 有 Common Mistakes，但没有“低质量输出反例 / 合格输出样例” | 模型知道不能做什么，但不一定知道什么叫足够好 |
| 技术反推缺少置信度机制 | 已要求不要把推测当事实，但没有每类技术判断的置信度模板 | 容易把 Workflow、Agent、RAG、模型路由等反推写得过满 |
| 飞书渲染检查仍偏人工 | 有表格和白板检查规则，但缺少系统化 checklist 或脚本化验证建议 | 输出在飞书端可能出现格式退化 |

## 4. Product Manager Planning

### 4.1 v2.0 Product Goal

让 `product-deep-dive` 从“能生成一篇完整拆解文档的 skill”，升级为“能稳定引导 AI 产品经理做深度分析、可复盘、可验证、可持续演进的 AI 产品研究系统”。

### 4.2 Target User Jobs

| User Job | Desired Outcome |
|---|---|
| 我想快速搭建某个 AI 产品的拆解框架 | 生成结构完整、问题尖锐、可继续补资料的飞书文档 |
| 我想判断一个 AI 产品为什么能火 | 能从市场、商业、用户、技术、模型和基础层解释增长原因 |
| 我想复用某个产品的设计方法 | 能提炼产品经理启发，而不是只复述功能 |
| 我想反推一个 AI 产品背后的系统设计 | 能明确区分事实、观察、推测、判断和待验证项 |
| 我想把拆解文章作为团队材料 | 飞书文档排版稳定，表格、callout、白板图可读可编辑 |

### 4.3 Functional Requirements

| ID | Requirement | Priority | Acceptance Criteria |
|---|---|---|---|
| FR1 | 为 13 个章节建立章节契约 | Must | 每章都有输入、分析动作、输出物、验收标准和常见失败模式 |
| FR2 | 建立产品类型 playbook | Must | 至少覆盖 AI 陪伴、AI Agent、AI 视频、AI 搜索、AI 编程五类产品 |
| FR3 | 建立评测 rubric library | Must | 端到端、过程能力、综合评测下可按场景生成二级指标、维度说明和评分逻辑 |
| FR4 | 强化市场层与商业层深挖 | Must | 市场层包含竞品表和竞争格局图；商业层包含增长、留存、变现、成本、供需关系 |
| FR5 | 强化技术/模型反推置信度 | Should | 技术层和模型层每个推断都能标注证据来源和置信度 |
| FR6 | 增加飞书输出自检清单 | Should | 写入前后检查标题、表格灰底加粗、callout、白板、信息缺口清单 |
| FR7 | 扩展 evals | Must | 覆盖触发、飞书输出、竞品表、评测二级指标、白板图、证据纪律和直接写场景 |
| FR8 | 增加优秀/低质样例 | Could | 每类关键章节至少有一个合格样例和一个常见失败反例 |

### 4.4 Non-Functional Requirements

| Category | Requirement |
|---|---|
| Maintainability | 主 skill 文件应逐步减少重复规则，把重参考拆到 `references/` |
| Traceability | 重要分析结论应能追溯到事实、观察、推测、判断或待验证 |
| Usability | 用户仍然最多只需要回答 3 个关键问题；“直接写”仍然能生成草稿 |
| Reliability | 每次改动必须更新或新增 eval case，防止核心行为退化 |
| Delivery quality | 飞书输出优先，聊天输出只作为 fallback |
| Trigger safety | 不因为普通 AI 名词、产品名、技术讨论而误触发 |

## 5. Architect Solutioning

### 5.1 Proposed Modular Structure

建议保持 `product-deep-dive/SKILL.md` 作为入口和流程编排文件，把重规则逐步拆到 `references/`。

```text
product-deep-dive/
  SKILL.md
  README.md
  references/
    chapter-contracts.md
    product-type-playbooks.md
    evaluation-rubrics.md
    market-business-analysis.md
    technical-inference.md
    feishu-formatting.md
    whiteboard-architecture.md
    output-quality-examples.md
  evals/
    evals.json
```

`SKILL.md` 应保留：

- Trigger discipline
- Before writing
- Research first
- Required structure
- Section execution loop
- Feishu delivery policy
- Final self-check

`references/` 应承载：

- 详细问题库
- 章节契约
- 产品类型 playbook
- 飞书 XML / Markdown 细节
- 白板图构建细节
- 评测 rubrics
- 低质输出反例

### 5.2 Chapter Contract Template

每个章节建议统一成以下契约：

| Field | Description |
|---|---|
| Purpose | 这一章解决什么产品判断问题 |
| Inputs | 需要哪些资料：官网、截图、体验路径、公开资料、用户反馈等 |
| Analysis Actions | 模型需要执行哪些分析动作，而不是只填表 |
| Required Outputs | 本章必须输出哪些内容 |
| High-Value Questions | 本章问题生成方向 |
| Evidence Rules | 哪些内容必须可溯源，哪些可以推测 |
| PM Insight | 本章产品经理启发应该聚焦什么 |
| Acceptance Criteria | 什么算本章合格 |
| Failure Modes | 常见低质输出是什么 |

### 5.3 Product-Type Playbooks

| Product Type | Extra Focus |
|---|---|
| AI 陪伴 / 角色互动 | 情感留存、角色设定、长期记忆、内容安全、付费动机、人格一致性 |
| AI Agent / Workflow | 工具调用、状态管理、任务分解、失败恢复、人机协作边界、过程透明度 |
| AI 视频 / 图片生成 | 生成质量、可控性、风格一致性、生产效率、素材资产管理、版权风险 |
| AI 搜索 / 研究 | 信息源质量、引用可追溯性、答案综合能力、事实更新、幻觉控制 |
| AI 编程 / DevTool | 代码质量、上下文理解、仓库级操作、测试闭环、开发者工作流嵌入 |

### 5.4 Evaluation Rubric Expansion

当前 v1.5 的三层主维度是正确方向。下一步建议把它做成可复用 rubric：

| Main Dimension | Second-Level Families | Typical Evidence |
|---|---|---|
| 端到端 | 端到端结果层、任务完成度、最终交付质量 | 最终输出、用户目标达成、可用性判断 |
| 过程能力 | 用户层、模型数据层、技术层、决策路径、异常恢复 | 截图路径、交互过程、工具调用表现、等待/失败/修改路径 |
| 综合评测 | 安全、成本、留存、商业价值、系统可扩展性 | 定价、模型成本推测、增长路径、长期数据沉淀、风险边界 |

每个指标必须包含：

- 评什么
- 为什么重要
- 怎么评
- 权重/满分
- 当前得分或待验证
- 证据来源

### 5.5 Evals Expansion Plan

| Eval ID | Scenario | Expected Guardrail |
|---|---|---|
| E1 | 用户只说“拆解某 AI 产品并输出飞书文档” | 不追问超过 3 个问题，默认创建飞书文档 |
| E2 | 用户给出飞书文档 URL | 更新指定文档，不新建文档 |
| E3 | 用户没有截图 | 加截图占位和信息缺口，不阻塞写作 |
| E4 | 市场层生成 | 至少 3 个竞品、固定竞品表字段、竞争格局图 |
| E5 | 测试评估体系生成 | 三大主维度不被替换，二级指标按场景展开 |
| E6 | 技术层反推 | 区分事实、观察、推测、判断、待验证 |
| E7 | 白板图生成 | 六层顺序正确、基础层在底部、可编辑白板优先 |
| E8 | 飞书表格 | 第一行和第一列灰底加粗 |

## 6. Implementation Backlog

### Phase 1: Framework Stabilization

| Task | Priority | Output |
|---|---|---|
| Create `references/chapter-contracts.md` | Must | 13 章章节契约 |
| Create `references/evaluation-rubrics.md` | Must | 测试评估 rubric library |
| Create `references/product-type-playbooks.md` | Must | 5 类 AI 产品 playbook |
| Update `SKILL.md` to reference modular docs | Must | 入口文件变轻，规则更清楚 |

### Phase 2: Quality and Evidence

| Task | Priority | Output |
|---|---|---|
| Create `references/technical-inference.md` | Should | 技术反推置信度规则 |
| Create `references/output-quality-examples.md` | Should | 合格/低质输出样例 |
| Expand `evals/evals.json` | Must | 覆盖 v1.4/v1.5 关键行为 |
| Add pre-delivery self-check checklist | Should | 飞书写入前后检查项 |

### Phase 3: Delivery Polish

| Task | Priority | Output |
|---|---|---|
| Document whiteboard generation patterns | Should | 更稳定的可编辑画板规则 |
| Add example output snippets to README | Could | 提升用户理解和安装后成功率 |
| Add public demo or screenshot placeholders | Could | 提升 GitHub 首屏可信度 |

## 7. Recommended Next Step

下一步建议执行 Phase 1，先不做大面积行为变更，而是建立三个核心 reference 文件：

1. `references/chapter-contracts.md`
2. `references/evaluation-rubrics.md`
3. `references/product-type-playbooks.md`

随后再精简 `SKILL.md`，让它从“所有规则的堆叠文件”变成“稳定的工作流入口 + 少量关键约束 + reference 路由器”。

这样能保持现有 skill 可用，同时让后续每次新增规则都有明确归属。
