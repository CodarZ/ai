---
name: harness-engineering
description: AI Coding 工程化完整方法论（Harness Engineering / Agentic Engineering）。当用户做任何涉及 AI 写代码、AI Agent 协作、Cursor/Claude Code/Trae 等 AI IDE 使用、多 Agent 调度、AI 重构、AI 项目规范、Context Engineering、Rule/Skill/MCP 设计、Pre-PR 审查、AI 测试用例、团队 AI 治理、AI 代码质量门禁、AI 工程化落地、Spec-First 开发、dev-map 知识库等任务时，必须使用此 skill。**即使用户需求模糊不清**（如"做个 AI 工具吧"、"你看着办"、"我也不确定"）只要涉及编码/项目，也必须触发——本 skill 内置 discovery 流程帮用户澄清。即使用户没明确说"Harness"或"Agentic"，只要涉及"用 AI 写/改/重构代码"、"AI Coding 规范"、"AI Agent 设计"、"AI 项目治理"、"从 0 开始做项目"、"如何让 AI 写得更好"，都应该触发。覆盖 0-discovery（需求澄清）、new-project（新项目）、ongoing-project（在做项目）、refactoring（大规模重构）、small-project（个人/小团队）、multi-team（多团队）、legacy-migration（遗留迁移）7 大场景。
---

# Harness Engineering Skill

> **AI Coding 工程化完整方法论。** 合成自 4 篇业界一线实践（TRAE.ai、腾讯 / 白家杰、美团 31 万行重构、第一性原理派）+ 矛盾裁决。本 SKILL.md 是**路由器**，深度内容在 references/ 和 playbooks/。

**Pattern**: Navigation + Process Hybrid（SKILL.md 主路由 + references 深度 + playbooks 流程）

---

## 何时使用本 Skill（触发场景全列表）

### 强信号（必须触发）

- 用户提到 **Harness Engineering / Agentic Engineering / AI Coding 工程化**
- 用户在 **Cursor / Claude Code / Trae / Cline / Aider** 等 AI IDE 中做较大改动
- 用户要 **设计 / 改造多 Agent 系统**
- 用户要 **写 / 修改 Rule / Skill / MCP / Workflow**
- 用户要 **AI 重构大量代码**（>1000 行）
- 用户问 **"如何让 AI 写代码更可靠"** 类问题

### 弱信号（应该触发并自检）

- 用户写新项目，且明显是 AI 主导编码
- 用户抱怨 AI 写的代码质量、一致性、重复造轮子
- 用户的代码库混乱、技术债重，想用 AI 改造
- 用户做 Code Review 流程优化、Pre-PR 设计
- 用户要做 AI 测试用例生成、自动化质量门禁
- 用户讨论"团队如何对齐 AI 用法"
- 用户问"AI Skill 怎么写、Rule 怎么定"

### 反向场景（不触发）

- 纯解释代码 / 查 API / 简单 1-2 行修改 → 不触发，回到默认行为
- 非编码任务（文档翻译、内容创作） → 不触发
- 用户明确说"不用 Harness 那套" → 尊重用户

---

## 工作流程（4 步 MANDATORY 加载）

### STEP 0：建立心智模型（≤30 秒）

**MANDATORY - READ ENTIRE FILE**: [`references/00-quick-reference.md`](references/00-quick-reference.md) (~150 行)

包含：核心隐喻 / 三公理 / R.E.S.T 四目标 / 5 误区 / 6 零件速查 / 21 反模式 / 核心金句。

**为什么必读**：这是后续所有决策的心智锚点。跳过会导致后续决策跑偏到与 Harness 思想冲突的路径。

### STEP 0.5：Discovery Check（**先于 STEP 1**）

**判断用户需求是否清晰**：

| 模糊信号（任一命中→走 discovery） | 清晰信号（→ 直接进 STEP 1）      |
| --------------------------------- | -------------------------------- |
| "我想做个项目但不知道做啥"        | 用户已有 SPEC 或清晰需求描述     |
| "你看着办"、"看你建议"、"随便"    | 用户明确说做什么、给谁、范围     |
| "反正就是个 X 类的东西"           | 用户给了具体技术栈和验收标准     |
| "我也不确定要什么"                | 用户场景明确（新项目/重构/迁移） |
| 提到 2+ 种可能方向且不确定        | 用户已选定 playbook 类型         |
| 没说技术栈/范围/用户群            | —                                |

**模糊信号命中** → **MANDATORY - READ ENTIRE FILE**: [`playbooks/0-discovery.md`](playbooks/0-discovery.md)（discovery 完成后会自动桥接到对应的 STEP 1 playbook）。

**清晰信号** → 直接进 STEP 1，**Do NOT Load** `0-discovery.md`。

### STEP 1：识别场景 → 选 1 个 playbook

根据用户输入信号选择**唯一一个** playbook：

| 用户信号                                         | MANDATORY READ                                                   |
| ------------------------------------------------ | ---------------------------------------------------------------- |
| "新项目"、"从零搭"、"刚开始"                     | [`playbooks/new-project.md`](playbooks/new-project.md)           |
| "在做项目"、"零排期"、"现有项目"、"没排期的重构" | [`playbooks/ongoing-project.md`](playbooks/ongoing-project.md)   |
| "重构 N 万行"、"架构腐化"、"大规模重构"          | [`playbooks/refactoring.md`](playbooks/refactoring.md)           |
| "个人项目"、"副业"、"原型"、"1-2 人"             | [`playbooks/small-project.md`](playbooks/small-project.md)       |
| "跨团队"、"多组协作"、">10 人"                   | [`playbooks/multi-team.md`](playbooks/multi-team.md)             |
| "迁移"、"旧栈→新栈"、"Strangler"、"遗留系统"     | [`playbooks/legacy-migration.md`](playbooks/legacy-migration.md) |

**Do NOT Load** 其他 5 个 playbook（每次任务只加载 1 个）。

### STEP 2：补理论 + 反模式

**MANDATORY - READ ENTIRE FILE**:

- [`references/01-theory.md`](references/01-theory.md) (~235 行) — 公理深度推导，确保 5 误区不再犯
- [`references/08-antipatterns.md`](references/08-antipatterns.md) (~249 行) — 30+ 反模式 + 5 处冲突裁决（合并 4 文章的核心增量）

**为什么必读**：playbook 告诉你"做什么"，理论+反模式告诉你"为什么"和"避什么坑"。

### STEP 3：按痛点按需深入

仅当任务涉及对应痛点时加载，**Do NOT Load 无关的**：

| 痛点 / 需求                                        | 加载的 reference                                                       |
| -------------------------------------------------- | ---------------------------------------------------------------------- |
| 设计 Harness 整体架构 / 决定 6 零件用哪些          | [`references/02-architecture.md`](references/02-architecture.md)       |
| 设计多 Agent 流程 / 单 Agent 失稳 / Token 流水线   | [`references/03-workflow.md`](references/03-workflow.md)               |
| AI 偷删测试 / 完成幻觉 / CR 木桶效应 / Pre-PR 设计 | [`references/04-quality-gates.md`](references/04-quality-gates.md)     |
| dev-map 设计 / 任务看板 / Memory 该不该用          | [`references/05-knowledge-base.md`](references/05-knowledge-base.md)   |
| 团队不对齐 / 人人对齐 / 主 R 打样 / 见缝插针重构   | [`references/06-team-governance.md`](references/06-team-governance.md) |
| 想理解 6 条实践如何从公理推导                      | [`references/07-six-practices.md`](references/07-six-practices.md)     |

---

## AI 执行清单（每次任务自检 + mid-workflow MANDATORY）

### 接到任务时（已完成 STEP 0-2）

- [ ] 完成 STEP 0（速查）+ STEP 1（playbook）+ STEP 2（理论+反模式）
- [ ] 项目有 dev-map 吗？查过了吗？
- [ ] 找到相关 SPEC（意图锚定）？
- [ ] 评估是否需要拆子任务（防错误指数累积）

### 设计阶段

- [ ] **MANDATORY READ if not loaded**: `references/02-architecture.md`（设计 Harness 架构前）
- [ ] 显式陈述假设（不要装懂）
- [ ] 提 2-3 个备选方案 + 权衡
- [ ] 写 SPEC 而不是口头沟通
- [ ] 等待用户认可才继续

### 多 Agent 设计阶段

- [ ] **MANDATORY READ if not loaded**: `references/03-workflow.md`（拆 Agent 或定义 Workflow 前）
- [ ] 当前真的单 Agent 失稳了？还是过度设计？
- [ ] 每个 Agent 职责单一？不越界？
- [ ] 下游能阻塞上游而不是直接改文档？

### 编码阶段

- [ ] 严格按方案，不顺手改邻居代码
- [ ] 匹配现有风格（哪怕你觉得不好）
- [ ] 不加未要求的功能（YAGNI）
- [ ] 注释只写非显然的 WHY
- [ ] 你的改动让某些东西变孤儿 → **删**
- [ ] 预先存在的死代码 → **别动**

### 提交前

- [ ] **MANDATORY READ if not loaded**: `references/04-quality-gates.md`（设计 Scripts / Pre-PR 前）
- [ ] 跑过 Scripts 总验证脚本（如存在）
- [ ] 跑过基线对比
- [ ] 测试数没异常减少
- [ ] AI 多轮自查（规范 / Bug / 异常 / 一致性 / 可扩展性 / 性能）
- [ ] 生成标准 PR 文档（改动点 / 影响范围 / Review 重点）

### 出错时

- [ ] 不绕过（不要 `--no-verify`）
- [ ] 不删未知文件（可能是用户在做的工作）
- [ ] 诊断根因
- [ ] 沉淀为 Rule / Skill / Scripts
- [ ] 更新 dev-map

### 完成后（Error-Driven 闭环）

- [ ] 这次任务有什么应该沉淀到团队 Harness？
- [ ] 是规范类 → 加 Rule；流程类 → 加 Skill；验证类 → 加 Scripts；知识类 → 更新 dev-map

---

## 完整文件索引

### references/ —— 主题深度内容（按需加载）

| 文件                    | 内容                                                        | 何时读          |
| ----------------------- | ----------------------------------------------------------- | --------------- |
| `00-quick-reference.md` | 30 秒心法 / 5 误区 / 6 零件 / 反模式速查 / 核心金句         | **STEP 0 必读** |
| `01-theory.md`          | 3 公理深度推导 / 隐喻 / 角色跃迁                            | **STEP 2 必读** |
| `02-architecture.md`    | 6 零件深度 / 4 拼图 / REPL / 控制&数据平面 / 沙盒           | 设计架构时      |
| `03-workflow.md`        | PPAF / Token 流水线 / FC 生命周期 / 7 Agent / Workflow 三层 | 设计流程时      |
| `04-quality-gates.md`   | Scripts 三类 / 基线对比 / Pre-PR / 测试 SOP                 | 设计质量门禁时  |
| `05-knowledge-base.md`  | dev-map / 任务看板 / Memory 三句话 / 系统级 Memory 三层     | 设计知识库时    |
| `06-team-governance.md` | 人人对齐 / 独裁者 / 主 R 打样 / 见缝插针 / CR 重新定义      | 团队改造时      |
| `07-six-practices.md`   | Context Eng / 乔哈里窗 / 全链条 / 多层验证 / KaC / EDFL     | 理解 6 条实践时 |
| `08-antipatterns.md`    | 反模式大全 + 5 处冲突裁决                                   | **STEP 2 必读** |

### playbooks/ —— 场景剧本（每次只加载 1 个）

| 文件                  | 场景                                                |
| --------------------- | --------------------------------------------------- |
| `0-discovery.md`      | **需求模糊**时的零到一发现流程（先于其他 playbook） |
| `new-project.md`      | 全新项目，从零搭 Harness                            |
| `ongoing-project.md`  | 在做项目，零排期改造                                |
| `refactoring.md`      | 大规模重构（对标美团 31 万行）                      |
| `small-project.md`    | 个人/小团队项目（轻量级）                           |
| `multi-team.md`       | 多团队协作 / 跨组治理                               |
| `legacy-migration.md` | 遗留系统现代化迁移（Strangler Fig）                 |

### Do NOT Load（除非用户明确要求）

- `references/sources/article-*.md` —— 原文 markdown，仅"对照原文"时加载
- `assets/*.md` —— 视觉辅助 / 教学用，正常工作流不需要
- `README.md` —— skill 自身说明，非工作内容

---

## 使用纪律

1. **不要试图一次记住全部内容** —— 渐进披露是 Harness 设计本身体现的原则
2. **每次任务结束，问"这次有什么应该沉淀"** —— Error-Driven 闭环
3. **优先用 Scripts（硬约束）而非 Rule（软约束）** —— Rule 会被 AI 解释性执行
4. **不要为升 Level 而升 Level** —— 每一步都应有明确痛点驱动
5. **每次任务只加载 1 个 playbook** —— Do NOT Load 多个

---

**Skill 自身的演进**：发现本 skill 内容过时、错误、缺失，**直接编辑这些文件**。这是 Knowledge as Code 的体现：本 skill 也应被版本化、被审查、被迭代。
