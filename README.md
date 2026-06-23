# AI Skills

> 面向 Claude Code / Cursor / Codex / Trae 等 AI 编码助手的可复用 Skills 仓库。

## 包含的 Skills

| Skill                                               | 用途                                                                                                                            |
| --------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| [`harness-engineering`](skills/harness-engineering) | AI Coding 工程化完整方法论（Harness Engineering / Agentic Engineering），覆盖 0-discovery、new-project、refactoring 等 7 大场景 |
| [`designmd-generator`](skills/designmd-generator)   | 为项目生成严格、规范的 `DESIGN.md` 设计文档                                                                                     |

## 安装

本仓库兼容 [`skills` CLI](https://github.com/vercel-labs/skills)（[skills.sh](https://skills.sh) 生态），使用 `bunx` 一键安装。

### 安装全部 skills 到当前项目

```bash
bunx skills add CodarZ/ai
```

### 安装指定 skill

```bash
bunx skills add CodarZ/ai --skill harness-engineering
bunx skills add CodarZ/ai --skill designmd-generator
```

### 先列出仓库里可装的 skills

```bash
bunx skills add CodarZ/ai --list
```

### 装到全局（所有项目可用）

```bash
bunx skills add CodarZ/ai --global
```

### 指定 AI agent

```bash
bunx skills add CodarZ/ai --agent claude-code   # 也支持 cursor / codex / opencode 等 70+ 种
```

### 不用 Bun 的替代命令

```bash
npx skills add CodarZ/ai
pnpm dlx skills add CodarZ/ai
```

### 手动安装

```bash
git clone https://github.com/CodarZ/ai.git
cp -r ai/skills/<skill-name> ~/.claude/skills/
```

## 卸载

```bash
bunx skills remove --skill <skill-name>
bunx skills remove --all
```

## 目录结构

```
skills/                    # 标准 skills 位置（被 skills CLI 自动发现）
  harness-engineering/
  designmd-generator/
.agents/
  rules/                   # 通用 AI 协作规则（非 skill 内容）
```
