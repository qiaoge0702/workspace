# TOOLS.md - 技术环境与工具标准

## 开发环境

- **主工作区**: `/Users/liuqiao/ai/workspace/`
- **核心模型**: Kimi (Moonshot AI) - 企业账号 (锁死单次工具返回高水位限额)

## 项目目录结构

```
/Users/liuqiao/ai/workspace/
├── cli-specialtrucks/demas/                    # DEMAS 自动化营销系统
│   ├── apps/
│   │   ├── server/           # 后端服务 (Port: 8000)
│   │   └── desktop/          # 桌面端 (Port: 1420)
│   └── docs/
│       ├── new/              # 新文档体系
│       └── old/              # 旧版参考
│
└── luolehaofang-old/            # 螺乐好房项目 (待创建)
    ├── mini-program/         # 微信小程序前端
    ├── server/               # 后端服务
    └── docs/                 # 项目文档
```

## 技术实现标准：大文件处理 (>=100MB)与代码审阅

**严禁全量读取内存，必须通过 Shell 指令处理：**
1. **行号定位**: 先使用 `grep -n "关键词" 路径` 锁定目标。
2. **切片提取**: 使用 `sed -n '开始行号,结束行号p' 路径` 或 `awk` 提取核心代码段。
3. **日志截断**: 工具返回的终端报错信息如果过长，一律使用 `head -n 50` 截取头部前 50 行抛给 Kimi。

## 执行规范

1. **默认只读**: 所有 write/edit/exec 操作前，必须输出方案等用户确认
2. **用户说"执行"后**: 才调用工具执行已确认的方案

## Kimi 企业账号使用规范

1. **代码 Diff 优先**: 严禁让 Kimi 完整重印未修改的代码大段，必须以标准的 Git Diff 或增量函数片段输出。
2. **信息流去噪**: 抛弃长篇大论的架构宏观原理解释，优先使用 Markdown 列表、对比表格。

## 常用脚本 (Context)

### DEMAS
- 数据库路径: `/Users/liuqiao/.demas/db/main.sqlite`

### 螺乐好房
- 待补充

## 技术栈参考

| 类型 | 技术 | 适用项目 |
|------|------|----------|
| 桌面端 | Tauri + React + TS | DEMAS |
| 后端 | Python + FastAPI | DEMAS |
| 小程序 | 微信小程序原生 / Taro | 螺乐好房 |
| 数据库 | SQLite / PostgreSQL | 通用 |
| 缓存 | Redis | 通用 |
