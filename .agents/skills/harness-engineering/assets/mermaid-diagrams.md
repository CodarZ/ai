# 集中收录的 Mermaid 流程图

> 所有重要的可视化资产集中在此，便于查阅 / 复用 / 教学。每个图都标注了来源章节。

---

## 1. Harness 核心架构

### 1.1 REPL 容器（核心抽象）

来源：`references/02-architecture.md` § 1

```mermaid
flowchart LR
    A[Read<br/>上下文管理器] -->|结构化 Prompt| B[Eval<br/>调用拦截器]
    B -->|Function Call 意图| C[工具执行器]
    C -->|执行结果| D[Print<br/>反馈汇编器]
    D -->|观测注入| A
    style A fill:#e0f0ff
    style B fill:#fff0e0
    style C fill:#e8f5e8
    style D fill:#f0e0ff
```

### 1.2 控制平面 vs 数据平面

来源：`references/02-architecture.md` § 4

```mermaid
flowchart TB
    subgraph CP[控制平面 Control Plane]
        S1[任务调度]
        S2[资源配额]
        S3[行为规划]
        S4[策略与权限]
    end
    subgraph DP[数据平面 Data Plane]
        D1[Agent 运行实例]
        D2[状态存储]
        D3[记忆存储]
        D4[沙盒执行环境]
    end
    CP -->|策略下发| DP
    DP -->|状态上报| CP
    style CP fill:#ffe0e0
    style DP fill:#e0e0ff
```

### 1.3 四块拼图模型

来源：`references/02-architecture.md` § 3

```mermaid
graph TB
    H[完整 Harness]
    H --> A[约束与流程]
    H --> B[反馈]
    H --> C[知识库]
    H --> D[进化]
    A --> A1[Rule / Skill / Sub Agent / Workflow]
    B --> B1[Scripts / 基线对比 / 事后验证]
    C --> C1[dev-map / 任务看板]
    D --> D1[Memory 主场划分 / Rule 沉淀机制]
```

### 1.4 系统级 Memory 三层架构

来源：`references/02-architecture.md` § 7

```mermaid
flowchart TB
    Q[用户问题] --> R[Retrieval 层]
    R --> M1[短期记忆<br/>当前会话状态]
    R --> M2[长期记忆<br/>用户偏好/历史]
    R --> M3[知识检索<br/>RAG / 向量数据库]
    M1 --> CM[Context Manager]
    M2 --> CM
    M3 --> CM
    CM --> P[拼装 Prompt]
    P --> LLM
```

---

## 2. 工作流程

### 2.1 PPAF 闭环

来源：`references/03-workflow.md` § 1

```mermaid
stateDiagram-v2
    [*] --> Perception
    Perception --> Planning: 感知到任务/环境
    Planning --> Action: 制定计划
    Action --> Feedback: 执行
    Feedback --> Perception: 反思 + 更新认知
    Feedback --> [*]: 任务完成
```

### 2.2 Token 转化流水线

来源：`references/03-workflow.md` § 2

```mermaid
flowchart LR
    A[1. 信息源收集] --> B[2. 相关性排序]
    B --> C[3. 压缩与摘要]
    C --> D[4. 预算分配]
    D --> E[5. 模板组装]
    E --> P[最终 Prompt]
    style A fill:#e0f0ff
    style E fill:#fff0e0
```

### 2.3 Function Calling 生命周期

来源：`references/03-workflow.md` § 3

```mermaid
sequenceDiagram
    participant H as Harness
    participant LLM
    participant T as Tool
    H->>LLM: 1. Schema 序列化注入
    Note over LLM: 模式匹配生成调用文本
    LLM->>H: 2. 触发生成（JSON 字符串）
    Note over H: 3. 确定性反序列化<br/>(最脆弱环节)
    alt 反序列化成功
        H->>T: 调用工具
        T->>H: 执行结果
        H->>LLM: 4. 观测注入（结果封装）
    else 反序列化失败
        H->>H: 重试 / 回退自然语言
    else 工具执行失败
        H->>LLM: 交互式补充 / 反思重规划
    end
```

### 2.4 七 Agent 结构化调度

来源：`references/03-workflow.md` § 4

```mermaid
flowchart TB
    PM[PM Agent<br/>路由 / 不做专业判断]
    PM <--> R[需求分析]
    PM <--> D[方案设计]
    PM <--> G[闸门总控<br/>可行性把关]
    PM <--> Dev[开发实现]
    PM <--> CR[代码审查]
    PM <--> T[测试验证]
    R -->|清晰需求| D
    D -->|技术方案| G
    G -->|GO/NO-GO| Dev
    Dev -->|代码| CR
    CR -->|审查通过| T
    T -->|测试通过| PM
    style PM fill:#ffe0e0
    style R fill:#e0f0ff
    style D fill:#e0f0ff
    style G fill:#fff0e0
    style Dev fill:#e8f5e8
    style CR fill:#f0e0ff
    style T fill:#f0e0ff
```

### 2.5 AI 全链条参与

来源：`references/03-workflow.md` § 7

```mermaid
flowchart LR
    A[需求阶段] --> B[设计阶段]
    B --> C[编码阶段]
    C --> D[验证阶段]
    A1[AI 引导者<br/>结构化提问] -.辅助.- A
    B1[AI 协作者<br/>分析权衡] -.辅助.- B
    C1[AI 执行者<br/>写代码] -.辅助.- C
    D1[AI 闸门<br/>验证 + 修复建议] -.辅助.- D
    A --> Q1[清晰需求文档]
    B --> Q2[技术方案]
    C --> Q3[代码]
    D --> Q4[通过/不通过]
    Q1 -.作为上下文.-> B1
    Q2 -.作为上下文.-> C1
    Q3 -.作为上下文.-> D1
```

---

## 3. 质量门禁

### 3.1 Scripts 三大类检查

来源：`references/04-quality-gates.md` § 2

```mermaid
graph TD
    Scripts[Scripts 总验证]
    Scripts --> A[A 类: 静态规范]
    Scripts --> B[B 类: 基础交付]
    Scripts --> C[C 类: 工程一致性]
    A --> A1[编码风格]
    A --> A2[命名规范]
    A --> A3[本地化合规]
    A --> A4[禁用 API 检查]
    A --> A5[硬编码 UI 文本]
    A --> A6[日志前缀]
    B --> B1[编译过]
    B --> B2[测试全过]
    B --> B3[测试数不能减少]
    C --> C1[规则多格式同步]
    C --> C2[.cs 都进 .csproj]
    C --> C3[流程定义一致]
```

### 3.2 基线对比机制

来源：`references/04-quality-gates.md` § 3

```mermaid
sequenceDiagram
    participant Dev as 开发者
    participant Scripts
    Note over Dev,Scripts: 开发前
    Dev->>Scripts: 跑总验证（基线模式）
    Scripts->>Dev: 当前失败列表 = baseline.json
    Note over Dev,Scripts: 开发中
    Dev->>Dev: AI 写代码
    Note over Dev,Scripts: 开发后
    Dev->>Scripts: 跑总验证（对比模式）
    Scripts->>Scripts: 当前失败 - baseline = 新增问题
    alt 有新增失败/告警/违规
        Scripts->>Dev: 必须修
    else 没新增
        Scripts->>Dev: 通过
    end
```

### 3.3 Pre-PR 机制

来源：`references/04-quality-gates.md` § 4

```mermaid
flowchart LR
    A[RD 写完代码] --> B[AI 多轮自查]
    B --> B1{6 维度自查}
    B1 -->|规范| B
    B1 -->|Bug| B
    B1 -->|异常| B
    B1 -->|一致性| B
    B1 -->|可扩展性| B
    B1 -->|性能| B
    B --> C[AI 生成标准 PR 文档]
    C --> D[改动点 + 影响范围 + Review 重点]
    D --> E[人工 Reviewer]
    E -->|聚焦业务语义| F[CR 通过]
    E -->|有问题| A
```

### 3.4 Human-in-the-loop 测试 5 步 SOP

来源：`references/04-quality-gates.md` § 5

```mermaid
flowchart LR
    S1[Step1<br/>建立范围] --> S2[Step2<br/>风险分级]
    S2 --> S3[Step3<br/>设计分组]
    S3 --> S4[Step4<br/>生成步骤]
    S4 --> S5[Step5<br/>验证覆盖]
```

---

## 4. 演进与团队治理

### 4.1 渐进引入顺序

来源：`references/02-architecture.md` § 8

```mermaid
flowchart LR
    S1[1. SPEC<br/>设计规格] --> S2[2. Rule<br/>底线红线]
    S2 --> S3[3. Skill<br/>高频动作]
    S3 --> S4[4. Sub Agent<br/>单 Agent 失稳后拆]
    S4 --> S5[5. Workflow<br/>多 Agent 复杂后定义]
    S5 --> S6[6. dev-map<br/>持续迭代时建]
    S6 --> S7[7. MCP<br/>想外推时接]
```

### 4.2 主 R 打样 → SOP 分发

来源：`references/06-team-governance.md` § 3

```mermaid
flowchart LR
    A[主 R 亲自跑通<br/>2 个最复杂模块] --> B[沉淀 AI 可执行的 SOP]
    B --> C[其他人按 SOP<br/>指导 AI 完成剩余模块]
    C --> D[主 R 只做<br/>业务语义验收 + CR]
```

### 4.3 见缝插针式重构

来源：`references/06-team-governance.md` § 4

```mermaid
flowchart LR
    Need[高优业务需求] --> Plan[拆解需求]
    Plan --> Need2[纯业务部分]
    Plan --> Tech[技术债部分<br/>顺带做]
    Need2 --> Done[完成]
    Tech --> Done
```

### 4.4 美团 31 万行重构三阶段

来源：`references/06-team-governance.md` § 7

```mermaid
flowchart TB
    Phase1[Phase 1<br/>痛点定位]
    Phase2[Phase 2<br/>共识与规范]
    Phase3[Phase 3<br/>主 R 打样]
    Phase4[Phase 4<br/>全组并行]
    Phase5[Phase 5<br/>持续演进]
    Phase1 --> Phase2
    Phase2 --> Phase3
    Phase3 --> Phase4
    Phase4 --> Phase5
    Phase5 -->|发现新痛点| Phase1
```

---

## 5. 实践模型

### 5.1 6 条实践协同关系

来源：`references/07-six-practices.md` § 8

```mermaid
flowchart TB
    Theory[3 公理]
    Theory --> P1[实践 1<br/>Context Eng]
    Theory --> P2[实践 2<br/>人机分工]
    Theory --> P3[实践 3<br/>全链条]
    P1 --> P4[实践 4<br/>多层验证]
    P2 --> P4
    P3 --> P4
    P4 --> P5[实践 5<br/>Knowledge as Code]
    P5 --> P6[实践 6<br/>Error-Driven 闭环]
    P6 -->|新错误沉淀| P5
    P6 -.->|反馈| P1
```

### 5.2 Error-Driven 反馈闭环

来源：`references/04-quality-gates.md` § 6 + `references/07-six-practices.md` § 7

```mermaid
flowchart LR
    A[AI 犯错] --> B[诊断根因]
    B --> C{是哪类问题}
    C -->|规范| D[加入 Rule]
    C -->|流程| E[改进 Skill]
    C -->|验证| F[加入 Scripts]
    C -->|知识| G[更新 dev-map]
    D --> H[预防同类复发]
    E --> H
    F --> H
    G --> H
```

### 5.3 角色跃迁路径

来源：`references/01-theory.md` § 4

```mermaid
flowchart TB
    P1[Phase 1<br/>写代码工人] --> P2[Phase 2<br/>用 AI 加速的代码工人]
    P2 --> P3[Phase 3<br/>建立 Skill 的 AI 用户]
    P3 --> P4[Phase 4<br/>完整 Harness 系统设计师]
```

---

## 6. 场景流程图

### 6.1 决策树（高层）

来源：`SKILL.md`

```mermaid
flowchart TB
    Start[接到 AI Coding 任务]
    Start --> Q1{项目状态?}
    Q1 -->|新项目| NP[playbooks/new-project.md]
    Q1 -->|在做项目| OP[playbooks/ongoing-project.md]
    Q1 -->|大规模重构| RP[playbooks/refactoring.md]
    Q1 -->|个人/小项目| SP[playbooks/small-project.md]
    Q1 -->|多团队/遗留| MT[playbooks/multi-team.md<br/>+ legacy-migration.md]
```

### 6.2 遗留系统迁移 Strangler Fig

来源：`playbooks/legacy-migration.md`

```mermaid
flowchart LR
    subgraph Old[旧系统]
        O1[模块 A]
        O2[模块 B]
        O3[模块 C]
    end
    subgraph New[新系统]
        N1[新模块 A]
    end
    User --> Router{路由层}
    Router -->|模块 A 流量| N1
    Router -->|其他| Old
    style N1 fill:#90EE90
    style O1 fill:#FFB6B6
```

### 6.3 影子流量校验

来源：`playbooks/legacy-migration.md` § Step 6

```mermaid
flowchart LR
    User --> Router
    Router --> Old
    Router -.影子.-> New
    Old --> Response[返回给用户]
    Old --> Compare[对比器]
    New --> Compare
    Compare --> Diff[行为差异报警]
```

---

## 用法

- **教学**：用图给团队解释 Harness 核心概念
- **设计**：作为模板对照你的项目架构
- **检查**：定期看看你的项目"画得出来吗"

每个图都有源 reference 链接，深入了解去看源文档。
