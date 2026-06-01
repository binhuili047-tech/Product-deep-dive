# Output Quality Examples

Use this reference to judge whether the final teardown reads like work from a senior AI Product Manager, not a template fill-in.

This module is intentionally opinionated. A senior AIPM teardown should convert product evidence into product judgment, system hypotheses, user-value trade-offs, and reusable product lessons.

## Senior AIPM Quality Bar

| Level | Name | Description | Acceptable? |
|---|---|---|---|
| L1 | 模板填充型 | Fills headings with generic descriptions. Mostly repeats visible features. | No |
| L2 | 信息整理型 | Collects public facts and screenshots, but analysis is mostly descriptive. | Only as rough draft |
| L3 | 产品经理分析型 | Explains user job, product choices, trade-offs, evidence boundaries, and product lessons. | Yes |
| L4 | 研究/策略型 | Adds market logic, business mechanism, technical confidence, risk, and strategic implications. | Excellent |

Default target: L3 for normal drafts, L4 for deep teardowns with enough evidence.

## What Senior AIPM Writing Must Do

- Turn feature lists into user jobs and product trade-offs.
- Separate visible evidence from inference and judgment.
- Explain why a design choice exists, not only what the choice is.
- Identify what the product refuses to do and why that may be strategic.
- Connect market, business, user path, model/data, and technical architecture.
- Make product-manager lessons specific enough to reuse.
- Name uncertainty instead of hiding it.

## What It Must Avoid

- Empty praise such as `体验很好`, `功能丰富`, `很有潜力`.
- Category clichés such as `AI 赋能`, `降低门槛`, `提升效率` without mechanism.
- Competitor lists without distribution, role, business model, or latest public signal.
- Technical claims such as `用了多 Agent` or `接了 RAG` without evidence and confidence.
- Product-manager insights that are just slogans.
- Tables full of generic dimensions that could apply to any product.

## Critical Chapter Examples

### 1. 产品定位与体验总结

#### Low-Quality Example

```markdown
这个产品是一款 AI 工具，主要面向内容创作者和普通用户。它可以帮助用户快速生成内容，提升效率，降低创作门槛。整体体验比较流畅，适合多种场景。
```

Why it fails:

- No clear user job.
- No product trade-off.
- No evidence.
- Could describe almost any AI product.

#### Senior AIPM Example

```markdown
一句话定位：它不是单纯的 AI 生成工具，而是把“从灵感到可发布资产”的多步骤创作流程压缩成一个低门槛工作台。

核心用户并不是所有内容创作者，而是缺少专业制作能力、但有明确表达意图和发布需求的轻量创作者。它的关键产品取舍是：优先降低首次产出门槛，而不是优先提供专业级参数控制。这会让新用户更快到达 Aha Moment，但也会限制高阶用户对细节、风格一致性和批量资产管理的要求。
```

Why it works:

- Defines what the product is and is not.
- Identifies core user and non-core user.
- Names a trade-off.
- Connects experience design to Aha Moment.

### 2. 测试评估体系

#### Low-Quality Example

```markdown
评估维度包括结果质量、交互体验、稳定性、创新性，满分 100 分。结果质量 30 分，交互体验 30 分，稳定性 20 分，创新性 20 分。
```

Why it fails:

- Ignores fixed main dimensions: 端到端 / 过程能力 / 综合评测.
- No scenario.
- No `评什么 / 为什么重要 / 怎么评`.
- No product-specific second-level indicators.

#### Senior AIPM Example

```markdown
本次测试场景：用户从一个模糊创作意图出发，完成一次可发布作品生成，并尝试进行二次修改。

| 主维度 | 评测视角 | 维度说明 |
|---|---|---|
| 端到端 | 黑盒评测 | 评什么：最终作品是否可发布；为什么重要：用户真正购买的是可用结果，不是生成过程本身；怎么评：用同一输入跑 3 次，比较完成度、指令遵循、可发布性和修改后质量。 |
| 过程能力 | 玻璃盒评测 | 评什么：从输入、生成、等待、编辑到导出的过程是否可控；为什么重要：AI 输出不稳定，过程控制决定用户是否愿意迭代；怎么评：记录关键路径、等待时间、失败恢复和用户可干预点。 |
| 综合评测 | 白盒评测 | 评什么：质量、成本、安全、版权、留存和商业价值是否整体成立；为什么重要：单次生成惊艳不代表产品可持续；怎么评：结合定价、生成成本、版权边界、复用能力和数据沉淀判断。 |
```

Why it works:

- Starts from a real scenario.
- Preserves the three main dimensions.
- Explains what, why, and how.
- Converts scoring into product judgment.

### 6. 市场层拆解

#### Low-Quality Example

```markdown
这个赛道竞争激烈，主要竞品有 A、B、C。它们都在做 AI 生成，未来市场空间很大。
```

Why it fails:

- No competitor role.
- No distribution channel.
- No business model.
- No latest public information.
- No competitive map.

#### Senior AIPM Example

```markdown
这个产品处在“轻量 AI 创作工具”和“专业生产力平台”的夹层：它如果只比生成质量，会被底层模型和大平台挤压；如果只比模板数量，又容易变成素材站。因此市场层关键问题不是“竞品是谁”，而是它想站在哪条价值链上。

| 平台/公司 | 主要角色 | 分发渠道 | 核心商业模式 | 最新公开信息 |
|---|---|---|---|---|
| 被拆解产品 | 垂直场景 AI 创作工具 | Web / App / 社交传播 | 订阅 + 高级生成额度 | 待验证 |
| 竞品 A | 通用生成平台 | Web / API / 创作者社区 | 订阅 + API 用量 | 以官网/公开资料为准 |
| 竞品 B | 专业工作流工具 | Web / 企业销售 | 团队订阅 | 待验证 |
| 竞品 C | 内容平台/分发入口 | App / 社区 | 流量与增值服务 | 待验证 |

竞争格局图建议坐标轴：横轴“轻量娱乐 -> 专业生产力”，纵轴“单次生成 -> 持续工作流”。这两个轴比单纯按功能分类更有效，因为它们能解释用户留存和付费意愿的差异。
```

Why it works:

- Defines competitive logic.
- Uses required competitor table fields.
- Explains why the landscape axes matter.
- Connects competition to retention and monetization.

### 7. 商业层拆解

#### Low-Quality Example

```markdown
商业模式主要是会员订阅，未来可以通过广告、增值服务和企业版变现。护城河是技术和用户数据。
```

Why it fails:

- Lists monetization options without mechanism.
- Claims moat without evidence.
- Does not analyze growth, retention, cost, or willingness to pay.

#### Senior AIPM Example

```markdown
它的商业化不应只看“有没有订阅”，而要看用户是否持续遇到同一类高频问题。若用户只是偶尔尝鲜，订阅会很难成立；若产品能沉淀项目、角色、风格、资产或团队协作关系，订阅才有留存基础。

当前更可能成立的商业路径是：免费低门槛试用带来首次 Aha Moment，再用生成额度、历史资产、风格库、批量能力或高级模型把用户推向付费。成本结构上，模型调用和素材存储会直接影响毛利，因此产品需要通过模板化、缓存、额度控制或分层模型路由降低边际成本。
```

Why it works:

- Links monetization to usage frequency.
- Explains willingness to pay.
- Discusses cost structure.
- Avoids unsupported moat claims.

### 9. 技术层拆解

#### Low-Quality Example

```markdown
这个产品背后应该是多 Agent 架构，接了 RAG，并使用模型路由来选择不同模型。主 Agent 负责理解用户需求，其他 Agent 负责执行任务。
```

Why it fails:

- Overclaims Multi-Agent, RAG, and routing.
- No visible evidence.
- No confidence labels.
- No verification path.

#### Senior AIPM Example

```markdown
从可见体验看，它更像是“固定 Workflow + Tool-Using Assistant”的组合，而不是可以高置信判断为 Multi-Agent。原因是用户路径呈现出明确的阶段：输入意图 -> 生成候选 -> 编辑/重试 -> 导出；但目前没有看到多个专门角色、并行子任务或明确 handoff 的证据。

| 推测对象 | 看到什么 | 可能机制 | 置信度 | 为什么这么推 | 如何验证 | 风险/Badcase |
|---|---|---|---|---|---|---|
| Workflow | 体验路径呈现固定阶段 | 预设生成管线 | 中 | 多次任务都按相似步骤推进 | 测试不同输入是否仍走同一阶段 | 复杂任务可能被固定流程限制 |
| RAG / 数据 grounding | 暂未看到引用、知识库或上传检索证据 | 可能只是上下文注入 | 低 | 缺少 source/citation/KB 配置证据 | 测试文档上传和引用一致性 | 幻觉或事实错误难以追踪 |
| 模型路由 | 不同生成类型可能有不同等待时间 | 可能存在任务级模型选择 | 低-中 | 只有延迟差异，缺少官方说明 | 查看官方模型披露或多任务质量差异 | 错路由导致质量不稳定或成本过高 |
```

Why it works:

- Gives a useful hypothesis without pretending it is fact.
- Uses confidence.
- Gives verification paths.
- Includes badcases.

### 10. 模型层拆解

#### Low-Quality Example

```markdown
它应该用了 GPT-4、Stable Diffusion 和多模态模型，所以能力比较强。
```

Why it fails:

- Names models without evidence.
- No task-to-model mapping.
- No capability boundary.

#### Senior AIPM Example

```markdown
目前不能确认具体底层模型，因此模型层更适合按“能力需求”而不是“模型名称”拆解。该产品至少需要三类能力：意图理解、生成执行、质量评估/重写。若产品支持图片、视频或语音，还需要额外的多模态生成与后处理能力。

高价值判断不是“它用了哪个模型”，而是“它是否把不同任务分给了合适的能力模块”。如果所有任务都依赖同一通用模型，产品会更简单但质量波动较大；如果存在任务级路由，产品可能在成本和质量之间做了更精细的权衡，但也会引入路由错误和一致性问题。
```

Why it works:

- Avoids unsupported model naming.
- Uses model-capability mapping.
- Explains trade-off.

### 产品经理启发

#### Low-Quality Example

```markdown
产品经理启发：AI 产品要重视用户体验，提升效率，降低门槛。
```

Why it fails:

- Generic.
- Not derived from the product.
- No reusable design principle.

#### Senior AIPM Example

```markdown
**产品经理启发**

这个产品真正值得学习的不是“用了 AI 生成”，而是它把不稳定的模型能力包装成了一个可被用户理解和反复尝试的工作流。对 AI PM 来说，关键不是让模型一次生成完美结果，而是设计一个能承接失败、鼓励迭代、保留用户控制感的过程。

可迁移原则：当底层能力不稳定时，产品设计要把“不确定性”变成可操作的步骤，例如候选结果、局部编辑、风格锁定、历史版本、失败恢复和可解释等待。
```

Why it works:

- Insight comes from product behavior.
- Names a product design mechanism.
- Offers a reusable principle.

## Senior AIPM Self-Check

Before final delivery, ask:

- Does each critical chapter contain a judgment, not only a description?
- Did the analysis explain why the product made a choice?
- Are facts, observations, inferences, judgments, and pending validations separated enough?
- Does the evaluation table explain scoring logic?
- Does market analysis include roles, channels, business models, and latest public signals?
- Does technical inference include confidence and validation paths?
- Are product-manager insights specific, transferable, and grounded in the analyzed product?

## Pressure-Test Prompts

Use these mental checks while reviewing output:

- If the product name were removed, would the paragraph still apply to any AI product? If yes, it is too generic.
- Is this sentence a feature, an observation, an inference, or a judgment? If unclear, rewrite it.
- Does every strong claim have evidence or a confidence boundary?
- Does every product-manager lesson tell the reader what to do differently next time?
