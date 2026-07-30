# PROJECTS.md - 项目总览

**最后更新**: 2026-07-29

---

## 项目列表

| 项目 | 类型 | 技术栈 | 状态 | 优先级 |
|------|------|--------|------|--------|
| **DEMAS** | 自动化营销系统 | Tauri + React + Python + SQLite | 维护中 | P1 |
| **螺乐好房** | 房地产小程序 | 微信小程序 + Java后端 | 设计阶段 | P1 |
| **图纸智能审查系统** | 专用车辆图纸生成+审查 | FastAPI + ezdxf + pywin32(SW COM) + Kimi K3 | 开发中 | P0 |

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

## 图纸智能审查系统 (drawing-review-system)

**定位**: 基于 AI 大模型的专用车辆工程图纸全生命周期系统 —— 从「图纸审查」扩展到「AI 生成 + 审查」闭环
**路径**: `E:\147\workspaces\drawing-review-system`

### 流程闭环

```
3D模型(SolidWorks) → AI生成DWG(视图投影/尺寸标注/BOM/技术要求)
                   → AI审查DWG(DXF解析/规则校验/Vision分析)
                   → 人工审核(确认修正/签字出图)
```

### 技术栈

| 层级 | 技术 | 说明 |
|------|------|------|
| 3D 解析 | pywin32 / trimesh | SW COM API 或 STEP 解析 |
| 2D 生成 | ezdxf + Pillow | DXF 构建 + 渲染验证 |
| DWG 转换 | ODA File Converter | DXF → DWG |
| AI 模型 | Kimi K3 / GPT-4o | Vision + Text 多模态 |
| 后端 | FastAPI + WebSocket | REST API + 进度推送 |
| 数据模型 | Pydantic 2.0+ | 类型安全 |

### 当前状态（2026-07-29）

- **M0 基线巩固**: ✅ 完成，149 项测试通过，环境/版本锁定
- **M1 框架搭建**: 🔄 进行中 — 8 步生成流水线骨架已落地（检查点/单步重跑），待接 `/api/generate` + WS 推送 + 前端页面
- **开发计划**: `docs/plans/`（M0-M6 里程碑 + 质量门禁，总览文档评审状态：待老板确认）
- **案例数据**: LB26 拉臂装置 208 个文件

### 下一步待办

| 优先级 | 任务 |
|--------|------|
| P0 | 接入 `/api/generate` 路由 + 任务管理 API（冻结契约） |
| P0 | WebSocket 进度推送协议 |
| P1 | 前端 `/generate` 页面 |
| M2 | Step3-7 执行器：几何解析→视图投影→DXF 构建端到端 |

### 风险

- 🟡 SW 试用期 30 天内需完成核心开发
- 🟡 3D 几何复杂度：先简单零件，逐步扩展

### 文档入口

- **项目总览**: `README.md` / `docs/00-项目总览.md`
- **生成方案**: `docs/01-AI生成DWG方案.md`
- **业务需求**: `docs/02-业务需求.md`
- **进度快照**: `进度状态-2026-07-28.md`

---

## 项目间关系

```
┌─────────────────────────────────────────┐
│           财神 (Cai Shen)                │
│         全栈技术负责人                    │
└─────────────────────────────────────────┘
                    │
        ┌──────────┼──────────┐
        ▼          ▼          ▼
┌───────────┐ ┌───────────┐ ┌───────────────────┐
│   DEMAS   │ │  螺乐好房  │ │  图纸智能审查系统   │
│  (维护中)  │ │  (待启动)  │ │     (开发中)       │
│           │ │           │ │                   │
│• 营销自动化│ │• 房产小程序│ │• AI 生成 DWG      │
│• 客户管理  │ │• 房源管理  │ │• AI 审查 DWG      │
│• 爬虫获客  │ │• 用户匹配  │ │• SW COM 解析      │
│• AI 画像  │ │• 交易闭环  │ │• 专用车辆上装设计   │
└───────────┘ └───────────┘ └───────────────────┘
```
