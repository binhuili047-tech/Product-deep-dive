# Chapter Contracts

Use this reference when building or improving the 13-section product teardown structure. A chapter contract defines what each chapter must do, not only what title it has.

## Contract Grammar

Each numbered chapter should be treated as a mini product-analysis unit with:

| Field | Meaning |
|---|---|
| Purpose | The product judgment this chapter should help the reader make. |
| Inputs | Materials needed: official pages, screenshots, tested paths, public reports, pricing, help docs, user notes, or inferred behavior. |
| Analysis Actions | The reasoning moves the AI should perform instead of simply listing facts. |
| Required Outputs | Concrete blocks that must appear in the chapter. |
| Evidence Rules | What can be stated as fact, observation, inference, judgment, or `待验证`. |
| Acceptance Criteria | What makes the chapter good enough for a product manager teardown. |
| Failure Modes | Common shallow outputs to avoid. |

## Universal Chapter Requirements

Every numbered section must include:

- `本节要回答的高价值问题` as a blockquote panel with 3-8 product-specific questions.
- A substantive `分析` section.
- Evidence-aware wording when making inferences.
- A `产品经理启发` callout/highlight block at the end.
- Screenshots or screenshot placeholders when the section depends on real experience.

## 1. 产品定位与体验总结

| Field | Contract |
|---|---|
| Purpose | Explain what the product is, whom it serves, and why the first experience matters. |
| Inputs | Official website, product intro, onboarding, first-run flow, app store copy, user-provided screenshots. |
| Analysis Actions | Compress product positioning into one sentence; identify core user; map primary use scenarios; identify the product's promised value, hidden trade-offs, anti-positioning, substitutes, and positioning assumptions. |
| Required Outputs | One-sentence positioning, anti-positioning, core user, non-core user, substitutes, usage scenarios, positioning assumptions, first-experience summary, strongest/weakest experience points. |
| Evidence Rules | Use official wording only when visible; infer target users from entry points and feature emphasis. |
| Acceptance Criteria | A reader can tell who the product is for, who it intentionally avoids, what users would otherwise use, what job it solves, and what must be true for this positioning to remain defensible. |
| Failure Modes | Generic category labels, vague users such as “everyone”, feature lists without positioning judgment, or positioning that never explains what the product refuses to become. |

## 2. 测试评估体系

| Field | Contract |
|---|---|
| Purpose | Build a scenario-specific evaluation system that moves from black-box output checks to glass-box process checks to white-box full-system assessment. |
| Inputs | Target scenario, user goal, critical path, product promise, visible outputs, process observations, technical inferences. |
| Analysis Actions | Define test scenario; preserve three main dimensions: `端到端`, `过程能力`, `综合评测`; generate second-level indicators by scenario; explain each dimension; assign weights. |
| Required Outputs | Evaluation dimension explanation table, scenario scoring table, score placeholders or tested scores, evidence/gap notes. |
| Evidence Rules | Scores are `待实测` unless actual testing happened; inferred technical criteria must be marked as inference or pending validation. |
| Acceptance Criteria | The table explains `评什么`, `为什么重要`, and `怎么评`; second-level indicators are concrete to the product category. |
| Failure Modes | Replacing the three main dimensions with arbitrary labels, using fixed weights for all products, or giving scores without scoring logic. |

## 3. 测试流程具体截图

| Field | Contract |
|---|---|
| Purpose | Record the real user path and identify Aha Moment and friction. |
| Inputs | Screenshots, screen recordings, tested prompts, generated outputs, wait states, errors, user notes. |
| Analysis Actions | Map step-by-step flow; identify critical path; locate trust-building moments, Aha Moment, waiting points, editing points, and recovery paths. |
| Required Outputs | Step table, screenshot placeholders, Aha Moment, friction points, evidence notes. |
| Evidence Rules | Do not invent screenshots; use placeholders when missing. |
| Acceptance Criteria | Another product manager can reproduce the test path. |
| Failure Modes | Only describing ideal flow, omitting failed/waiting states, or not naming screenshot needs. |

## 4. 差异化定位

| Field | Contract |
|---|---|
| Purpose | Explain how the product differs from market convention and why that difference matters. |
| Inputs | Competitor info, product flows, pricing, feature set, public positioning, user reviews. |
| Analysis Actions | Compare mental model, workflow, distribution, business model, and capability boundaries; identify non-obvious choices. |
| Required Outputs | Differentiation table, industry convention broken, reason for choice, copyability assessment. |
| Evidence Rules | Keep competitor claims traceable; mark strategic interpretation as judgment. |
| Acceptance Criteria | The reader understands whether differentiation is real user value or marketing language. |
| Failure Modes | Listing features as differentiation without explaining user impact. |

## 5. 能力边界

| Field | Contract |
|---|---|
| Purpose | Identify what the product cannot do and whether limits are technical, product, cost, compliance, data, or UX choices. |
| Inputs | Failed tests, docs, help center, pricing tier limits, output errors, unavailable workflows. |
| Analysis Actions | Separate current limitation from deliberate positioning; map blocked adoption cases; identify missing capabilities that should not be built yet. |
| Required Outputs | Boundary table, cause classification, user impact, near-term/long-term priority. |
| Evidence Rules | Use `待验证` for untested edge cases. |
| Acceptance Criteria | The chapter helps decide what not to build as much as what to build. |
| Failure Modes | Treating every missing feature as a bug or weakness. |

## 6. 市场层拆解

| Field | Contract |
|---|---|
| Purpose | Situate the product in a market category, competition map, and trend context. |
| Inputs | Official sites, competitor pages, app stores, pricing, public announcements, credible media, market reports. |
| Analysis Actions | Define category; compare at least 3 competitors; identify substitutes; choose axes for competitive landscape; explain trend drivers. |
| Required Outputs | Market category, competitor table, competitive landscape diagram, trend analysis, market assumptions. |
| Evidence Rules | `最新公开信息` must be verifiable or marked `待验证`. |
| Acceptance Criteria | The reader can see who competes with the product, through which channel, and why the market is timely. |
| Failure Modes | Generic market report without competitors, or competition analysis without concrete distribution/business model comparison. |

## 7. 商业层拆解

| Field | Contract |
|---|---|
| Purpose | Explain why the product can grow, retain, and monetize. |
| Inputs | Pricing, plans, app store monetization, public metrics, funding, community, traffic sources, observed paywalls. |
| Analysis Actions | Map growth loop, retention mechanism, monetization path, payment trigger, unit economics, cost structure, channel leverage, supply-demand relationship, and moat evidence. |
| Required Outputs | Growth-retention-monetization analysis, payment trigger, unit economics hypothesis, cost drivers, margin pressure, supply-demand logic, moat evidence strength, business risk. |
| Evidence Rules | Mark revenue/funding/usage metrics as fact only when sourced. |
| Acceptance Criteria | The chapter explains why the product can or cannot become a sustainable business, including whether growth, retention, monetization, and cost structure reinforce or fight each other. |
| Failure Modes | Saying “subscription” without explaining willingness to pay, payment timing, growth loop, retention mechanism, unit economics, or cost structure. |

## 8. 场景/用户层拆解

| Field | Contract |
|---|---|
| Purpose | Explain user entry, path, motivation, and feature-module relationship. |
| Inputs | Onboarding, navigation, feature modules, tested tasks, user screenshots, community behavior. |
| Analysis Actions | Map entry -> intent -> action -> feedback -> output -> retention; classify user segments and jobs. |
| Required Outputs | User path, feature-module map, scenario segmentation, friction and retention triggers. |
| Evidence Rules | Distinguish observed flows from inferred user motivation. |
| Acceptance Criteria | The reader understands the user loop and where product value compounds. |
| Failure Modes | Listing modules without explaining user path or motivation. |

## 9. 技术层拆解

| Field | Contract |
|---|---|
| Purpose | Reverse-engineer visible workflow, tools, agents, orchestration, and integration logic. |
| Inputs | User-visible steps, latency, outputs, error messages, docs, API/integration pages, app behavior. |
| Analysis Actions | Infer workflow vs single agent vs multi-agent; identify tools, state objects, RAG, external plugins, preprocessing/postprocessing, badcases. |
| Required Outputs | Technical inference table, confidence level, workflow/agent hypothesis, badcase analysis. |
| Evidence Rules | Never present inferred architecture as fact; attach confidence and evidence basis. |
| Acceptance Criteria | The reader can see a plausible system design without confusing it for confirmed implementation. |
| Failure Modes | Overclaiming Agent/RAG/Multi-Agent without evidence. |

## 10. 模型层拆解

| Field | Contract |
|---|---|
| Purpose | Explain model capability matching, routing, and task specialization. |
| Inputs | Output types, latency, quality patterns, model disclosures, pricing, release notes, failure cases. |
| Analysis Actions | Infer model families, routing strategy, task-to-model mapping, capability bottlenecks, uncertainty around model choices. |
| Required Outputs | Model routing hypothesis, capability fit table, model-layer risks, pending validation. |
| Evidence Rules | Official model claims are facts; model inference is judgment or `待验证`. |
| Acceptance Criteria | The chapter explains why certain model capabilities are required and how they may be orchestrated. |
| Failure Modes | Treating one product output as proof of a specific model. |

## 11. 不确定性处理

| Field | Contract |
|---|---|
| Purpose | Analyze how the product handles uncertainty in input, generation, user intent, safety, and output quality. |
| Inputs | Ambiguous prompts, retries, regenerate/edit flows, safety messages, fallback behavior, errors. |
| Analysis Actions | Identify uncertainty sources; map control mechanisms; assess transparency, recovery, and safety trade-offs. |
| Required Outputs | Uncertainty source table, handling mechanism, user impact, product design lesson. |
| Evidence Rules | Use tested examples where possible; mark untested safety claims as `待验证`. |
| Acceptance Criteria | The reader understands whether uncertainty is hidden, exposed, controlled, or productized. |
| Failure Modes | Treating uncertainty only as model hallucination and ignoring UX/process uncertainty. |

## 12. 基础层拆解

| Field | Contract |
|---|---|
| Purpose | Explain context, knowledge, style libraries, data assets, feedback loops, and long-term defensibility. |
| Inputs | Account/project memory, style presets, templates, asset libraries, feedback mechanisms, docs, data policies. |
| Analysis Actions | Identify data assets, knowledge bases, context stores, style systems, personalization, feedback loops, data compounding effects, switching costs, and compliance/copyright constraints. |
| Required Outputs | Foundation-layer map, data/knowledge table, what gets accumulated, how accumulation improves the next experience, switching-cost analysis, data flywheel judgment, moat or weakness analysis. |
| Evidence Rules | Treat data moat claims cautiously unless there is visible accumulation or official evidence. |
| Acceptance Criteria | The reader understands what the product accumulates over time, why users would keep feeding it data/assets/context, whether that accumulation improves future outputs, and whether it creates real defensibility. |
| Failure Modes | Confusing model capability with product-owned data or context infrastructure, treating storage as a data moat, or claiming a data flywheel without explaining compounding improvement. |

## 13. 最终架构图

| Field | Contract |
|---|---|
| Purpose | Synthesize the product into a six-layer architecture board. |
| Inputs | Insights from sections 6, 7, 8, 9, 10, and 12. |
| Analysis Actions | Extract layer modules, normalize naming, preserve six-layer order, add expansion slots, ensure no contradictions with mini diagrams. |
| Required Outputs | Final six-layer diagram: 市场层, 商业层, 用户层, 应用层, 模型层, 基础层; editable Feishu whiteboard when possible. |
| Evidence Rules | Diagram labels can include inferred modules if the analysis text makes uncertainty clear. |
| Acceptance Criteria | The architecture is readable, near-square, multi-color, vertically stacked, and has no arrows/connectors. |
| Failure Modes | Drawing a flowchart, using one color, putting 基础层 anywhere except the bottom, or making mini diagrams contradict the final diagram. |
