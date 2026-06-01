# TOOLS.md - 技术环境与工具标准

## 开发环境

- **主工作区**: `/Users/liuqiao/ai/`
- **核心模型**: Kimi (Moonshot AI) - 企业账号

## 项目目录结构

```
/Users/liuqiao/ai/
├── cli-specialtrucks/demas/                    # DEMAS 自动化营销系统
│   ├── apps/
│   │   ├── server/           # 后端服务 (Port: 8000)
│   │   └── desktop/          # 桌面端 (Port: 1420)
│   └── docs/
│       ├── new/              # 新文档体系
│       └── old/              # 旧版参考
│
└── luole-haofang/            # 螺乐好房项目 (待创建)
    ├── mini-program/         # 微信小程序前端
    ├── server/               # 后端服务
    └── docs/                 # 项目文档
```

## 技术实现标准：大文件处理 (>=100MB)

**严禁全量读取内存，必须通过 Shell 指令处理：**
1. **定位**: 使用 `grep -n` 获取行号
2. **提取**: 使用 `awk 'NR>=start && NR<=end'` 获取特定行
3. **统计**: 使用 `wc -l` 快速统计

## Kimi 企业账号使用规范

1. **Token 控制**: 企业账号按量计费，精简上下文，避免冗余
2. **结构化输出**: 优先使用表格、列表，提高信息密度
3. **分步执行**: 复杂任务拆分，降低单次请求 token 消耗
4. **模板复用**: 常用提示词提取到 `skills/prompt-templates/` 复用

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
