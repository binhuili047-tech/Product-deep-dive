# Changelog

All notable changes to `product-deep-dive` are documented here by version.

本文件按版本记录 `product-deep-dive` 的重要变更。

## v1.6 - BMAD Framework Upgrade Brief

### Added

- Added `docs/product-deep-dive-framework-upgrade-brief.md`, a BMAD-style analysis and planning document for improving the framework toward v2.0.
- The brief includes:
  - Analyst diagnosis of current strengths and gaps.
  - Product Manager requirements, priorities, and acceptance criteria.
  - Architect-level modular structure proposal.
  - Evaluation rubric expansion plan.
  - Evals expansion plan.
  - Implementation backlog for future modularization.

### Changed

- Updated README repository structure and maintenance guidance to point to the BMAD upgrade brief.

## v1.5 - Evaluation Sub-Dimensions and Dimension Explanations

### Added

- Expanded section 2 `测试评估体系` so the three required main dimensions now support scenario-specific second-level indicators.
- Added common second-level indicator families:
  - `端到端结果层`
  - `用户层`
  - `模型数据层`
  - `技术层`
- Required every evaluation dimension to include a detailed explanation covering:
  - `评什么`
  - `为什么重要`
  - `怎么评`
- Updated the scoring table template to include `维度说明` so the evaluation logic is explicit instead of score-only.

### Changed

- Clarified that second-level indicators are generated under the fixed main dimensions `端到端`, `过程能力`, and `综合评测`; they should not replace the main dimensions.

## v1.4 - Market Competitor Analysis

### Added

- Required section 6 `市场层拆解` to include a competitor comparison table covering the analyzed product and at least 3 main competitors.
- Standardized the market-layer competitor table columns:
  - `平台/公司`
  - `主要角色`
  - `分发渠道`
  - `核心商业模式`
  - `最新公开信息`
- Required section 6 to include a competitive landscape diagram with product-relevant axes and the analyzed product plus at least 3 competitors.

### Changed

- Clarified that `最新公开信息` should use verifiable public sources when available, and unresolved cells should be marked `待验证` and added to the information gap checklist.

## v1.3 - Three-Layer Evaluation Framework

### Changed

- Standardized section 2 `测试评估体系` around three required main dimensions:
  - `端到端`: black-box evaluation focused on final output, scenario completion, and whether the user receives a usable result.
  - `过程能力`: glass-box evaluation focused on intermediate process, state changes, tool use, decision path, interaction recovery, and workflow reliability.
  - `综合评测`: white-box evaluation focused on full-process, multidimensional assessment across output, process, model orchestration, cost, safety, data, and business value.
- Required second-level indicators to be generated dynamically under these three main dimensions based on the concrete product and testing scenario.
- Updated README guidance so humans and AI agents understand that the main evaluation dimensions are fixed, while sub-indicators and weights remain scenario-specific.

## v1.2 - Documentation, Distribution, and Cross-Agent Support

### Added

- Added repository-level bilingual README guidance inspired by mature skill repositories:
  - clear first-screen positioning
  - badges
  - AI Agent quick install
  - human quick start
  - troubleshooting
  - repository structure
  - update instructions
- Added explicit `lark-cli` prerequisite guidance before installation and usage.
- Added Claude Code support in README:
  - `Claude Compatible` badge
  - Claude Code installation path
  - Claude Code update path
  - Codex / Claude-compatible wording throughout the README
- Added repository license visibility in README:
  - GitHub license badge
  - repository structure entry for `LICENSE`
  - License section pointing to the `LICENSE` file
- Added this `CHANGELOG.md`.

### Changed

- Updated GitHub repository URL from the previous username to:
  `https://github.com/VioletScar-Hui/Product-deep-dive`
- Reworked `For AI Agents: Quick Install` into a safer sequence:
  1. check `lark-cli`
  2. install or update the skill
  3. verify `SKILL.md`
  4. optionally verify Feishu and whiteboard tooling
  5. restart Codex or Claude Code
- Reworked `Quick Start for Humans` into a first-success path:
  1. prepare `lark-cli`
  2. install the skill for Codex or Claude Code
  3. run a product teardown prompt
  4. understand expected output
- Corrected installation guidance to match the repository layout: clone/update the repository into a cache directory, then copy the `product-deep-dive/` skill subdirectory into the Codex or Claude Code skills directory.

## v1.1 - Feishu Delivery, Whiteboards, and Formatting Rules

### Added

- Added strict trigger discipline to `SKILL.md`:
  - the skill should trigger only when the user asks for AI product deep-dive analysis and Feishu-style document output
  - the skill should not trigger merely because AI, Agent, RAG, LLM, SaaS, or product names are mentioned
- Added default Feishu document delivery behavior:
  - create a new Feishu document when no target URL is provided
  - update the provided Feishu document when a target URL exists
  - avoid asking whether to write to Feishu when the user already requested Feishu output
- Added section-level high-value question rules:
  - every numbered section should contain 3-8 product-specific questions
  - questions should be dynamically rewritten based on searched or provided product information
- Added Feishu table formatting rules:
  - every table's first row uses gray background and bold text
  - every table's first column uses gray background and bold text
  - applies to product basic information, scoring tables, technical inference tables, and information gap tables
- Added editable Feishu whiteboard delivery workflow:
  - coordinate-based SVG
  - SVG to OpenAPI raw nodes via `@larksuite/whiteboard-cli`
  - write to Feishu whiteboard with `lark-cli whiteboard +update`
  - verify document contains `<whiteboard token=...>` blocks
  - handle missing whiteboard OAuth scopes

### Changed

- Changed architecture diagram requirements from static Mermaid-first diagrams to editable Feishu whiteboard-first diagrams when permissions are available.
- Standardized the final architecture diagram around six vertical layers:
  1. 市场层
  2. 商业层
  3. 用户层
  4. 应用层
  5. 模型层
  6. 基础层
- Clarified that the six layers stack from top to bottom, while each layer's internal second-level module groups are arranged left to right.
- Required per-layer mini architecture diagrams under sections 6, 7, 8, 9, 10, and 12.
- Swapped the previous section order so section 10 is `模型层拆解` and section 11 is `不确定性处理`.
- Required `产品经理启发` to use Feishu callout/highlight blocks instead of quote blocks.
- Required `本节要回答的高价值问题` to use blockquote panels.

### Documented Practice

- Built and tested a Feishu document teardown for 星野 as a representative use case.
- Reworked architecture diagram logic through multiple layout iterations:
  - avoided long horizontal strips
  - kept six layers vertically ordered
  - used colored layer backgrounds
  - preserved editable whiteboard output
  - added per-layer diagrams under the corresponding chapters

## v1.0 - Initial Product Deep-Dive Framework

### Added

- Created the initial `product-deep-dive` skill for AI product-manager teardown writing.
- Established the 13-section teardown framework:
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
- Added `核心结论` before the numbered chapters.
- Added `信息缺口清单` at the end of the document.
- Added evidence discipline:
  - facts
  - observations
  - inferences
  - judgments
  - to-verify items
- Added `evals/evals.json` for skill evaluation coverage.
