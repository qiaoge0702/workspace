# TOOLS.md - 技术环境与工具标准

> 行为铁律见 SOUL.md。本文档只列技术规范。

---

## 开发环境

- **主工作区**: `/Users/liuqiao/ai/workspace/`
- **核心模型**: Kimi (Moonshot AI) - 企业账号

## 项目目录

```
/Users/liuqiao/ai/workspace/
├── cli-specialtrucks/demas/          # DEMAS (Port: 8000/1420)
└── luolehaofang-new/                  # 螺乐好房 (待创建)
```

## 代码读取策略

| 文件类型 | 工具 | 限制 |
|----------|------|------|
| 文档 (*.md) | `read` | 无限制 |
| 代码 <200行 | `read` | 可完整读取 |
| 代码 ≥200行 | `exec(grep/sed/awk)` | **单次切片 ≤50行** |

**强制规则**:
1. ≥200行禁止 `read`，先 `grep -n` 定位
2. 单次 `sed/awk` ≤50行
3. `grep` 后报行号范围，直接执行

## Kimi 企业账号

- **代码 Diff 优先**: 禁止完整重印未修改代码，用 Git Diff 或增量片段
- **信息流去噪**: 表格 > 段落，抛弃长篇架构解释

## 常用路径

- DEMAS 数据库: `/Users/liuqiao/.demas/db/main/*.db`

## 技术栈参考

| 类型 | 技术 | 项目 |
|------|------|------|
| 桌面端 | Tauri + React + TS | DEMAS |
| 后端 | Python + FastAPI | DEMAS |
| 小程序 | 微信小程序 / Taro | 螺乐好房 |
| 数据库 | SQLite / PostgreSQL | 通用 |
