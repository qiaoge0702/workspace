# PROJECTS.md - 项目总览

**最后更新**: 2026-06-11

---

## 项目列表

| 项目 | 类型 | 技术栈 | 状态 | 优先级 |
|------|------|--------|------|--------|
| **DEMAS** | 自动化营销系统 | Tauri + React + Python + SQLite | 维护中 | P1 |
| **螺乐好房** | 房地产小程序 | 微信小程序 + Java后端 | 设计阶段 | P1 |

---

## DEMAS 系统

**全称**: Digital Employee Managed Automation System  
**路径**: `cli-specialtrucks/demas/`

### 子系统

| 子系统 | 全称 | 功能 | 状态 |
|--------|------|------|------|
| DEMAS-SS | Scraping System | 自动化爬虫获客 | 运行中 |
| DEMAS-CRM | Customer Relationship Management | 桌面级客户管理系统 | 运行中 |
| DEMAS-MS | Marketing System | 自动化营销与跟进 | 运行中 |
| DEMAS-PS | Profiling System | AI 驱动的客户画像与评分 | 运行中 |
| DEMAS-ASE | Adaptive Scraping Engine | 自适应数据源采集引擎 | 开发中 |

### 文档入口

- **索引**: `cli-specialtrucks/demas/docs/DEMAS-INDEX.md`
- **开发规范**: `cli-specialtrucks/demas/docs/new/DEVELOPMENT-STANDARDS.md`
- **系统总览**: `cli-specialtrucks/demas/docs/new/DEMAS-OVERVIEW.md`

---

## 螺乐好房

**定位**: 房地产小程序，对标贝壳找房  
**路径**: `luolehaofang-new/`

### 技术方案

| 层级 | 技术 |
|------|------|
| 前端 | 微信小程序原生 + TypeScript + MobX |
| 管理端 | React 18 + Ant Design Pro 5 + Zustand |
| 后端 | Java 17 + Spring Boot 3.2 + MyBatis-Plus |
| 数据库 | MySQL 8.0 + Redis 7.x |
| 搜索 | Elasticsearch 8.x |
| 消息队列 | RocketMQ 5.x |
| 文件存储 | MinIO |

### 文档进度

| 阶段 | 状态 | 完成度 |
|------|------|--------|
| 第一步：项目规划 | ✅ 完成 | 1/1 |
| 第二步：架构设计 | ✅ 完成 | 3/3 |
| 第三步：开发规范 | ✅ 完成 | 6/6 |
| 第四步：详细需求 | ✅ 完成 | 17/17 |

### 待办

- [x] 创建项目目录结构
- [x] 确定技术栈细节
- [x] 编写项目文档（第一阶段）
- [ ] 完成剩余详细需求文档（6个模块）
- [ ] 搭建开发环境
- [ ] 启动代码开发

---

## 项目间关系

```
┌─────────────────────────────────────────┐
│           财神 (Cai Shen)                │
│         全栈技术负责人                    │
└─────────────────────────────────────────┘
                    │
        ┌──────────┴──────────┐
        ▼                     ▼
┌───────────────┐     ┌───────────────┐
│    DEMAS      │     │  螺乐好房      │
│  (维护中)      │     │  (待启动)      │
│               │     │               │
│ • 营销自动化   │     │ • 房产小程序   │
│ • 客户管理     │     │ • 房源管理     │
│ • 爬虫获客     │     │ • 用户匹配     │
│ • AI 画像     │     │ • 交易闭环     │
└───────────────┘     └───────────────┘
```
