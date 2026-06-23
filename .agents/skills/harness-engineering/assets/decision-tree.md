# 完整决策树（场景 → 行动）

> 接到 AI Coding 任务，该读哪个 reference / playbook？这是详细版决策树。

---

## 第一层：识别任务类型

```
接到 AI Coding 任务
   │
   ▼
┌──────────────────────────────┐
│ 这是什么类型的任务？           │
└──────────────────────────────┘
   │
   ├─ 编码工作 ──────────────────┐
   │                            │
   ├─ 设计 Harness 系统 ────────┤
   │                            │
   ├─ 重构 / 迁移 ──────────────┤
   │                            │
   ├─ 质量问题诊断 ─────────────┤
   │                            │
   └─ 团队治理 ─────────────────┘
```

---

## 第二层：进一步识别

### 编码工作

```
编码工作
   │
   ▼
需求是否清晰？
   │
   ├─ 模糊 ("做个 X 吧"/"你看着办"/"我不确定")
   │     └─→ 📘 playbooks/0-discovery.md (先走 discovery)
   │            │
   │            ▼ SPEC 收敛后桥接 ↓
   │
   ▼
项目状态？
   │
   ├─ 新项目 ─→ 📘 playbooks/new-project.md
   │
   ├─ 在做项目 ─→ 📘 playbooks/ongoing-project.md
   │
   ├─ 小项目 (1-3 人 / <5000 行) ─→ 📘 playbooks/small-project.md
   │
   └─ 多团队共享 ─→ 📘 playbooks/multi-team.md

必读补充：
   - 📖 references/07-six-practices.md (6 条核心实践)
   - 📖 references/08-antipatterns.md (反模式 + 冲突裁决)
```

### 设计 Harness 系统

```
设计 Harness
   │
   ▼
设计什么？
   │
   ├─ 整体架构 ─→ 📖 references/02-architecture.md
   │              (6 零件 / 4 拼图 / REPL / 控制&数据平面)
   │
   ├─ 多 Agent 流程 ─→ 📖 references/03-workflow.md
   │                   (PPAF / 7 Agent / Workflow 三层)
   │
   ├─ 质量门禁 ─→ 📖 references/04-quality-gates.md
   │              (Scripts / 基线对比 / Pre-PR / 测试 SOP)
   │
   ├─ 知识库 ─→ 📖 references/05-knowledge-base.md
   │            (dev-map / 任务看板 / Memory 定位)
   │
   └─ 团队结构 ─→ 📖 references/06-team-governance.md
                   (人人对齐 / 独裁者 / 主 R 打样)
```

### 重构 / 迁移

```
重构/迁移
   │
   ▼
规模？
   │
   ├─ 同栈大规模 (>5 万行) ─→ 📘 playbooks/refactoring.md
   │                          (对标美团 31 万行)
   │
   ├─ 跨栈迁移 ─→ 📘 playbooks/legacy-migration.md
   │              (Strangler Fig 模式)
   │
   └─ 小重构 ─→ 📘 playbooks/ongoing-project.md
                 (见缝插针)

必读补充：
   - 📖 references/04-quality-gates.md (Scripts + 基线对比)
   - 📖 references/06-team-governance.md (主 R 打样)
```

### 质量问题诊断

```
质量问题
   │
   ▼
症状？
   │
   ├─ AI 老犯同错 ─→ 📖 references/08-antipatterns.md
   │                  Error-Driven 闭环
   │
   ├─ 完成幻觉 ─→ 📖 references/04-quality-gates.md
   │              Scripts 闸机 + 基线对比
   │
   ├─ AI 偷删测试 ─→ 📖 references/04-quality-gates.md
   │                 § 2.B "测试数不能减少"
   │
   ├─ CR 木桶效应 ─→ 📖 references/04-quality-gates.md § 4
   │                 Pre-PR 机制
   │
   ├─ 代码风格混乱 ─→ 📖 references/06-team-governance.md
   │                  人人对齐 + 独裁者
   │
   └─ 上下文淹没 ─→ 📖 references/05-knowledge-base.md
                     dev-map 索引化
```

### 团队治理

```
团队治理
   │
   ▼
团队规模？
   │
   ├─ 单团队 ─→ 📖 references/06-team-governance.md
   │
   ├─ 跨团队 ─→ 📘 playbooks/multi-team.md
   │
   └─ 想了解理论 ─→ 📖 references/01-theory.md
                     (3 公理 + 5 误区)
```

---

## 第三层：场景 × 痛点交叉表

| 场景 \ 痛点  | AI 写得乱                        | 验证缺失                       | 知识漂移                            | 团队不一致                        |
| ------------ | -------------------------------- | ------------------------------ | ----------------------------------- | --------------------------------- |
| **新项目**   | 📘new-project § Step 2 (补 Rule) | 📘new-project § Step 7 后置    | 📘new-project § Step 6 (建 dev-map) | 📘new-project § 决策 1 (工具统一) |
| **在做项目** | 📘ongoing § 阶段 2 (升级 Rule)   | 📘ongoing § Scripts 闸机       | 📘ongoing § dev-map 渐进            | 📘ongoing § Pre-PR                |
| **重构**     | 📘refactoring § Action 1         | 📘refactoring § Scripts + 基线 | 📘refactoring § dev-map 迁移        | 📘refactoring § 主 R 打样         |
| **小项目**   | 📘small-project § 最小 Rule      | 📘small-project § check.sh     | 📘small-project § 简单 INDEX.md     | n/a                               |
| **多团队**   | 📘multi-team § 分层标准          | 📘multi-team § Pre-PR 跨团队版 | 📘multi-team § Cross-team dev-map   | 📘multi-team § Chief Architect    |
| **遗留迁移** | 📘legacy § 新栈 Rule             | 📘legacy § 双跑校验            | 📘legacy § 新 dev-map               | 📘legacy § 主 R 打样              |

---

## 第四层：紧急情况快速导航

| 问题                | 应急参考                                      |
| ------------------- | --------------------------------------------- |
| AI 在多步任务迷路   | references/03-workflow.md § PPAF              |
| AI 改了不该改的文件 | references/08-antipatterns.md § AI 解释性执行 |
| AI 删了关键测试     | references/04-quality-gates.md § 测试数检查   |
| AI 借口"本来就有"   | references/04-quality-gates.md § 基线对比     |
| 不知道改哪个文件    | references/05-knowledge-base.md § dev-map     |
| 团队 Rule 各执一词  | references/06-team-governance.md § 独裁者     |
| 重构永远做不完      | playbooks/refactoring.md § 见缝插针           |

---

## 第五层：从零到精通的学习路径

### 新手（第 1 周）

1. SKILL.md（速查）
2. references/01-theory.md（公理 + 5 误区）
3. references/02-architecture.md § 1-2（REPL + 6 零件）
4. 任选一个对应自己场景的 playbook

### 进阶（第 2-4 周）

1. references/03-workflow.md
2. references/04-quality-gates.md
3. references/07-six-practices.md
4. 完整读你场景的 playbook

### 精通（第 2 月+）

1. references/05-knowledge-base.md
2. references/06-team-governance.md
3. references/08-antipatterns.md
4. references/sources/ 原始文章对照阅读

---

## 关键认知

> 不要试图一次读完所有内容。**渐进披露**是 Harness 设计本身体现的原则。
> 当前任务需要什么，就读什么。
