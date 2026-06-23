# Harness Engineering Skill

> AI Coding 工程化完整方法论。合并自 4 篇业界一线实践 + 矛盾裁决，自包含可执行。

## 这是什么

一个 Claude / Cursor / Trae 等 AI 工具可用的 **Skill**，让 AI 在做 AI Coding 任务时遵循 Harness Engineering 的工程方法论。

合成来源：

1. 《理解 Harness Engineering，看这一篇就够了》—— TRAE.ai
2. 《从第一性原理思考 Agentic Engineering》—— 腾讯云开发者
3. 《Harness Engineering 如何工程化落地？》—— 腾讯云开发者 / 白家杰
4. 《用 Agent 评测思路管理 AI Coding —— 31 万行代码 AI 重构的实践》—— 美团技术团队

合成处理：

- ✅ 提取共识
- ✅ 裁决 5 处冲突（Memory 地位 / AI 自主程度 / 方法论起点 / Sub-Agent 数量 / CR 价值）
- ✅ 去除冗余表述
- ✅ 按"理论→架构→流程→治理→演进→反模式→决策"重组
- ✅ 自包含，无外部引用

## 目录结构

```
harness-engineering/
├── SKILL.md                  # 主入口（pushy description + 速查 + 决策树）
├── README.md                 # 本文件
│
├── references/               # 按主题组织的深度内容
│   ├── 01-theory.md          # 公理 / 误区 / 隐喻
│   ├── 02-architecture.md    # 6 零件 / 4 拼图 / REPL / 沙盒
│   ├── 03-workflow.md        # PPAF / Token 流水线 / 7 Agent
│   ├── 04-quality-gates.md   # Scripts / Pre-PR / 测试 SOP
│   ├── 05-knowledge-base.md  # dev-map / 任务看板 / Memory
│   ├── 06-team-governance.md # 人人对齐 / 主 R 打样 / 见缝插针
│   ├── 07-six-practices.md   # Context Eng / 乔哈里窗 / KaC
│   ├── 08-antipatterns.md    # 反模式大全 + 冲突裁决
│   └── sources/              # 原文 markdown（可追溯）
│       ├── article-1.md
│       ├── article-2.md
│       ├── article-3.md
│       └── article-4.md
│
├── playbooks/                # 按场景组织的剧本
│   ├── 0-discovery.md        # 需求模糊时的零到一发现（先于其他 playbook）
│   ├── new-project.md        # 新项目从零搭
│   ├── ongoing-project.md    # 在做项目改造（零排期）
│   ├── refactoring.md        # 大规模重构（对标美团 31 万行）
│   ├── small-project.md      # 个人/小团队（轻量级）
│   ├── multi-team.md         # 多团队协作 / 跨组治理
│   └── legacy-migration.md   # 遗留系统迁移（Strangler Fig）
│
└── assets/                   # 视觉资产
    ├── decision-tree.md      # 完整决策树
    ├── 6-components-table.md # 6 零件详细对照表
    ├── harness-maturity-levels.md  # L0–L5 成熟度自检
    └── mermaid-diagrams.md   # 集中收录的 mermaid 流程图
```

## 怎么用

### 作为 Skill 自动触发（推荐）

放在 `~/.claude/skills/harness-engineering/`，Claude 在以下场景会自动加载：

- 用户提到 Harness Engineering / Agentic Engineering / AI Coding 工程化
- 用户在 AI IDE 中做较大改动
- 用户讨论多 Agent / Rule / Skill / MCP 设计
- 用户做 AI 重构 / Pre-PR / 测试 SOP

详见 SKILL.md frontmatter 的 description。

### 作为参考文档手动使用

```bash
# 想了解 Harness 是什么 → 从根本读起
cat references/01-theory.md

# 我要做 X 场景 → 直接读 playbook
cat playbooks/refactoring.md

# 想避坑 → 反模式大全
cat references/08-antipatterns.md
```

### 推荐学习路径

**新手（第 1 周）**：

1. SKILL.md（速查）
2. references/01-theory.md（公理 + 5 误区）
3. references/02-architecture.md § 1-2（REPL + 6 零件）
4. 对应你场景的 playbook

**进阶（第 2-4 周）**：

1. references/03-workflow.md
2. references/04-quality-gates.md
3. references/07-six-practices.md

**精通（第 2 月+）**：

1. references/05-knowledge-base.md
2. references/06-team-governance.md
3. references/08-antipatterns.md
4. references/sources/ 对照原文

## 核心思想速记

> **AI Agent = SOTA 模型（野马）+ Harness（缰绳）= 千里马**

> 三公理：**意图损耗链 / LLM 三特征 / 认知稀缺**

> 六实践：**Context Eng / 人机分工 / 全链条 / 多层验证 / KaC / EDFL**

> R.E.S.T 四目标：**Reliability / Efficiency / Security / Traceability**

> 六零件：**Rule / Skill / Sub Agent / Workflow / Scripts / MCP**

> 四拼图：**约束流程 / 反馈 / 知识库 / 进化**

> 渐进顺序：**SPEC > Rule > Skill > Agent > Workflow > dev-map > MCP**

## 关键纪律

1. **不要试图一次记住所有内容** —— 渐进披露是 Harness 设计本身体现的原则
2. **每次任务结束，问"这次有什么应该沉淀"** —— Error-Driven 闭环
3. **优先用 Scripts（硬约束）而非 Rule（软约束）** —— Rule 会被 AI 解释性执行
4. **不要为升 Level 而升 Level** —— 每一步都应有明确痛点驱动

## 演进

发现本 skill 内容过时、错误、缺失 → **直接编辑这些文件**。

这是 Knowledge as Code 的体现：本 skill 本身也应被版本化、被审查、被迭代。

## 适用范围

- ✅ Claude Code / Cursor / Trae / Aider / Cline 等 AI IDE
- ✅ Claude API 应用开发
- ✅ 团队 AI Coding 治理
- ✅ AI 重构项目
- ✅ 新项目用 AI 主导开发
- ✅ 多团队协作
- ✅ 遗留系统迁移

## 不在范围

- ❌ 非 AI Coding 的工程方法论（如 DevOps 通用实践）
- ❌ 具体编程语言 / 框架技巧（这是 IDE/工具的事）
- ❌ AI 模型本身的训练 / 微调

## 引用

如果你引用本 skill 的某些概念，请同时引用原始来源：

- TRAE.ai - Harness Engineering 定义与系统架构
- 腾讯云开发者 / 白家杰 - 6 零件 / 4 拼图 / JK Launcher 实战
- 腾讯云开发者 - 第一性原理 / 6 条实践
- 美团技术团队 - 31 万行重构 / Pre-PR / 主 R 打样

完整原文在 `references/sources/`。
