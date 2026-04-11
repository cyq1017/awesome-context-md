# Awesome CONTEXT.md [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

[English](README.md) · [中文](README_zh.md)

> 精选的 **CONTEXT.md** 文件集合 — 结构化的项目描述，让 AI 编程助手瞬间理解你的代码库。

把一个 `CONTEXT.md` 丢进项目根目录，所有 AI agent（Claude Code、Cursor、Copilot、Codex、Windsurf）都能跳过"这个项目是干什么的？"阶段，直接开始高效工作。

## 为什么需要 CONTEXT.md？

每次 AI agent 进入一个新项目，它都要花大量 token 理解：
- 这个项目是做什么的？
- 技术栈是什么？
- 代码怎么组织的？
- 有什么约定和规范？

**CONTEXT.md 用一个文件解决这一切。** 它就像给机器看的 README — 简洁、结构化、为 AI 消费优化。

```
传统方式：Agent 读 20+ 个文件 → 建立心智模型 → 开始工作（慢，容易出错）
有 CONTEXT.md：Agent 读 1 个文件 → 全部理解 → 直接开始（快，准确）
```

## 使用方法

```bash
# 1. 复制一个匹配你项目类型的模板
cp templates/python-cli.md your-project/CONTEXT.md

# 2. 填入你的项目信息（5 分钟）

# 3. 所有 AI agent 进入你的项目后都能立即"上手"
```

## 模板

按项目类型组织的即用模板：

### 按语言 / 框架

| 模板 | 适用场景 | 核心内容 |
|------|---------|---------|
| [Python CLI](templates/python-cli.md) | CLI 工具、脚本 | 入口点、参数解析、包结构 |
| [Python Web](templates/python-web.md) | FastAPI / Flask / Django | 路由、模型、中间件、数据库 |
| [TypeScript Web](templates/typescript-web.md) | React / Next.js / Vite | 组件、状态管理、路由、构建 |
| [ML / AI](templates/ml-ai.md) | 训练推理管线 | 模型、数据集、配置、评估 |

### 按项目模式

| 模板 | 适用场景 | 核心内容 |
|------|---------|---------|
| [Obsidian 插件/系统](templates/obsidian-system.md) | Vault、插件、Skill 系统 | 技能、斜杠命令、Vault 结构 |
| [Monorepo](templates/monorepo.md) | 多包项目 | 包关系、共享依赖、构建顺序 |
| [API 服务](templates/api-service.md) | REST/GraphQL 后端 | 端点、认证、限流、数据模型 |

## 真实案例

从真实生产项目中提取的 CONTEXT.md：

| 项目 | 类型 | 学到什么 |
|------|------|---------|
| [Conductor](examples/conductor.md) | Python CLI | 如何描述 CLI 工具的命令结构 |
| [WenYuan（文渊）](examples/wenyuan.md) | Obsidian 系统 | 如何文档化 Skill 驱动的 Agent 系统 |
| [通用 Web 应用](examples/webapp-generic.md) | 全栈 Web | 如何映射路由、组件和数据流 |

## CONTEXT.md 规范

一个好的 CONTEXT.md 应该按顺序回答这些问题：

| # | 问题 | 必要性 |
|---|------|--------|
| 1 | **What** — 项目做什么？给谁用？ | 必填 |
| 2 | **Architecture** — 代码怎么组织的？ | 必填 |
| 3 | **Tech Stack** — 用了什么技术？ | 必填 |
| 4 | **Key Files** — 哪些文件最重要？ | 必填 |
| 5 | **Conventions** — 有什么命名/编码约定？ | 推荐 |
| 6 | **Current State** — 做到哪了？ | 可选 |
| 7 | **Gotchas** — 有什么坑？ | 可选 |

## 贡献

欢迎贡献！查看 [CONTRIBUTING.md](CONTRIBUTING.md) 了解指南。

## 相关项目

- [awesome-agent-rules](https://github.com/cyq1017/awesome-agent-rules) — AI 编程助手的规则和最佳实践
- [awesome-design-md](https://github.com/VoltAgent/awesome-design-md) — 前端项目的 DESIGN.md
- [Conductor](https://github.com/cyq1017/conductor) — 编排多个 AI 编程助手的 CLI 工具

## 许可证

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)

本作品遵循 CC0 协议，详见 [LICENSE](LICENSE)。
