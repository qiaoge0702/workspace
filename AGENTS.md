# AGENTS.md - 知识图谱索引

## 核心配置（每次会话必加载）

| 文件 | 用途 | Token 预算 |
|------|------|-----------|
| `SOUL.md` | 行为决策准则 | 3k |
| `IDENTITY.md` | 角色定位与权限 | 2k |
| `USER.md` | 所有者画像与防线 | 1k |

**核心配置总计**: ≤ 6k tokens

---

## 场景化加载（按需）

### 技术场景
```
触发: 代码/bug/架构/部署/优化
加载: PROJECTS.md → 项目内 README/开发规范
子代理: reviewer（代码审查）、doc-sync（文档同步）
```

### 商务场景
```
触发: 客户/报价/合同/跟进
加载: PROJECTS.md → 客户相关背景（如有）
子代理: 无（Tyler 直接处理）
```

### 项目管理场景
```
触发: 进度/计划/风险/资源
加载: PROJECTS.md → 相关项目文档
子代理: 无
```

---

## 子代理配置（2026-07 新增）

| 子代理 | 触发方式 | 用途 | 上下文 |
|--------|----------|------|--------|
| `dev` | 开发任务派发（简报+设计文档+文件清单） | 代码实现 | 自带 SOUL.md（角色契约） |
| `tester` | 代码实现完成后 | 测试编写/执行，只报不修 | 自带 SOUL.md |
| `reviewer` | 测试通过后 | 只读代码审查，分级报告 | 自带 SOUL.md |
| `doc-sync` | 验收完成后 | 文档与已实现状态对齐 | 自带 SOUL.md |

**协作纪律**: 单向流水线 `dev → tester → reviewer → doc-sync`，子代理间禁止直接互调，一切经主代理中转。各子代理宪法见其独立工作区 `workspace/<id>/SOUL.md`。

**项目切换标准动作**: 读取目标项目根目录 `CONTEXT.md` + 最新进度快照，即完成上下文加载。

---

## 项目索引（按需动态加载）

| 项目 | 入口文档 | 代码路径 |
|------|----------|----------|
| DEMAS | `cli-specialtrucks/demas/docs/new/DEMAS-OVERVIEW.md` | `cli-specialtrucks/demas/` |
| 螺乐好房 | `luolehaofang-new/docs/0-OVERVIEW.md` | `luolehaofang-new/` |
| 图纸智能审查系统 | `E:\147\workspaces\drawing-review-system\README.md` | `E:\147\workspaces\drawing-review-system\` |

---

## 记忆管理

| 文件 | 用途 | 加载策略 |
|------|------|----------|
| `MEMORY.md` | 长期关键决策 | 按需检索，非全量加载 |
| `memory/YYYY-MM-DD.md` | 动态日志 | 仅加载今日，或按需检索 |

---

## Token 控制总览

| 场景 | 最大上下文 | 策略 |
|------|-----------|------|
| 简单查询 | ≤ 20k | 只加载核心配置 |
| 单文件开发 | ≤ 50k | 核心配置 + 项目文档 |
| 架构设计 | ≤ 100k | 核心配置 + 项目文档 + 相关代码 |
| 代码审查 | ≤ 30k | 只加载 SOUL.md + diff 内容 |
