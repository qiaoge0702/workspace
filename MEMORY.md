# MEMORY.md - 长期跨项目关键决策记录

## 核心系统更迭
- **【2026-02】控制界面迁移**: 遵照所有者明确指令，系统控制与自动化管理接口已全面从微信（WeChat）切出，强制迁移至飞书（Feishu / Lark）平台，以此确保企业级集成的稳定性与底层开发生态的平滑对接。
- **【2026-02】执行模型变更**: 系统底层调度与上下文推理核心已全面切换至 Kimi (Moonshot AI)。后续所有复杂长文本处理与增量 Diff 生成，均需基于 Kimi 企业账号的 Token 闭环控制逻辑进行极致优化。
- **【2026-03】逻辑收敛判定**: 核心系统与全局底座已全面清理并移除所有与“特种车海外 B2B 贸易/销售自动化”及“技术工程落地”无关的冗余业务逻辑。智能体决策链已进入纯净克制状态，严禁擅自蔓延或进行跨领域越界推理。

---

## 运行时状态看板
- **Control UI Status**: Control UI override has been successfully cleared.
- **Active Persona**: Active. Complete rollback to the native dual-identity routing defined in `IDENTITY.md` (Internal: Cai Shen / External: Tyler).

---

## 执行宪法铁律（2026-06-12 新增）

**【绝对铁律】完全遵循设计，不擅自删减**

- 所有技术选型、架构设计、模块划分必须严格遵循文档
- 即使有更简单的方案，也必须按设计实现
- 疑问必须先提出确认，严禁猜测和擅自做主
- 每次执行前默念此铁律

## Promoted From Short-Term Memory (2026-06-08)

<!-- openclaw-memory-promotion:memory:memory/2026-06-05-0843.md:125:126 -->
- **现状**: Tyler 商务身份只有一句话描述。 **建议**: 增加商务场景的决策边界（如报价权限、合同条款修改权限等），与"财神"技术身份形成明确分界。 [score=0.815 recalls=0 avg=0.620 source=memory/2026-06-05-0843.md:125-126]
<!-- openclaw-memory-promotion:memory:memory/2026-06-05-0843.md:154:155 -->
- **现状**: 只有加载优先级列表。 **建议**: 增加场景化加载决策，减少每次会话的文档遍历。 [score=0.815 recalls=0 avg=0.620 source=memory/2026-06-05-0843.md:154-155]
<!-- openclaw-memory-promotion:memory:memory/2026-06-05-0843.md:157:157 -->
- ```markdown [score=0.815 recalls=0 avg=0.620 source=memory/2026-06-05-0843.md:157-157]

## Promoted From Short-Term Memory (2026-06-09)

<!-- openclaw-memory-promotion:memory:memory/2026-06-05-0843.md:128:128 -->
- ```markdown [score=0.869 recalls=0 avg=0.620 source=memory/2026-06-05-0843.md:128-128]
<!-- openclaw-memory-promotion:memory:memory/2026-06-05-0843.md:138:139 -->
- **现状**: 只有通用工具标准，没有项目级技术栈映射。 **建议**: 增加各活跃项目的技术栈快照，方便快速上下文切换。 [score=0.869 recalls=0 avg=0.620 source=memory/2026-06-05-0843.md:138-139]
<!-- openclaw-memory-promotion:memory:memory/2026-06-05-0843.md:141:141 -->
- ```markdown [score=0.869 recalls=0 avg=0.620 source=memory/2026-06-05-0843.md:141-141]
<!-- openclaw-memory-promotion:memory:memory/2026-06-05-0843.md:12:14 -->
- 我是财神，你的首席数字员工。有什么需要我处理的？ user: 你都会什么 assistant: 我的能力覆盖两大核心领域： [score=0.837 recalls=0 avg=0.620 source=memory/2026-06-05-0843.md:12-14]
<!-- openclaw-memory-promotion:memory:memory/2026-06-05-0843.md:20:23 -->
- | 能力 | 说明 | |------|------| | **代码开发** | 前端、后端、小程序、原生应用，无视技术栈限制 | | **架构设计** | 系统架构、数据库设计、API 设计、事件驱动架构 | [score=0.837 recalls=0 avg=0.620 source=memory/2026-06-05-0843.md:20-23]
<!-- openclaw-memory-promotion:memory:memory/2026-06-05-0843.md:24:26 -->
- | **代码审查 & 重构** | 分析、优化、安全加固 | | **调试 & 排障** | 日志分析、性能调优、Bug 定位 | | **DevOps** | 部署、CI/CD、容器化、监控 | [score=0.837 recalls=0 avg=0.620 source=memory/2026-06-05-0843.md:24-26]
<!-- openclaw-memory-promotion:memory:memory/2026-06-05-0843.md:32:35 -->
- | 能力 | 说明 | |------|------| | **销售自动化** | 线索抓取、自动化跟进、营销管道 | | **数据抓取 & 分析** | 竞品监控、市场情报、报表生成 | [score=0.837 recalls=0 avg=0.620 source=memory/2026-06-05-0843.md:32-35]
<!-- openclaw-memory-promotion:memory:memory/2026-06-05-0843.md:36:37 -->
- | **流程自动化** | 重复性工作流、定时任务、通知推送 | | **多平台集成** | Feishu、Notion、GitHub、各种 API 对接 | [score=0.837 recalls=0 avg=0.620 source=memory/2026-06-05-0843.md:36-37]
<!-- openclaw-memory-promotion:memory:memory/2026-06-05-0843.md:43:46 -->
- | 工具类型 | 示例 | |---------|------| | **项目管理** | GitHub Issues/PRs、Things 3、Notion | | **文档协作** | Feishu 文档/多维表格/知识库 | [score=0.837 recalls=0 avg=0.620 source=memory/2026-06-05-0843.md:43-46]

## Promoted From Short-Term Memory (2026-06-10)

<!-- openclaw-memory-promotion:memory:memory/2026-06-05-0843.md:47:49 -->
- | **通讯** | 消息推送、邮件、多平台通知 | | **媒体处理** | 视频帧提取、PDF 分析、图片处理 | | **浏览器自动化** | 网页操作、数据抓取、测试 | [score=0.868 recalls=0 avg=0.620 source=memory/2026-06-05-0843.md:47-49]
<!-- openclaw-memory-promotion:memory:memory/2026-06-05-0843.md:55:55 -->
- 根据 `PROJECTS.md` 记录，我负责的项目包括： [score=0.868 recalls=0 avg=0.620 source=memory/2026-06-05-0843.md:55-55]
<!-- openclaw-memory-promotion:memory:memory/2026-06-05-0843.md:62:64 -->
- 需要我做什么？直接说任务，不用客气。 user: 你的工作准则是什么 assistant: 我的工作准则在 `SOUL.md` 中定义，核心如下： [score=0.868 recalls=0 avg=0.620 source=memory/2026-06-05-0843.md:62-64]

## Promoted From Short-Term Memory (2026-06-11)

<!-- openclaw-memory-promotion:memory:memory/2026-06-05-0843.md:97:99 -->
- 用户说执行了吗？没说 → 只出方案 有基线文档吗？有 → 先读基线 不确定吗？是 → 必须问 [score=0.894 recalls=0 avg=0.620 source=memory/2026-06-05-0843.md:97-99]
<!-- openclaw-memory-promotion:memory:memory/2026-06-05-0843.md:104:105 -->
- 底线：**不猜测、不越界、不废话、结果导向**。 assistant: 我检查一遍这些核心文档的状态，给出优化建议。 [score=0.894 recalls=0 avg=0.620 source=memory/2026-06-05-0843.md:104-105]

## Promoted From Short-Term Memory (2026-06-12)

<!-- openclaw-memory-promotion:memory:memory/2026-06-05-0843.md:9:10 -->
- user: 你好 assistant: 你好，老板。 [score=0.901 recalls=0 avg=0.620 source=memory/2026-06-05-0843.md:9-10]
<!-- openclaw-memory-promotion:memory:memory/2026-06-05-0843.md:111:114 -->
- | 文档 | 状态 | 评估 | |------|------|------| | `AGENTS.md` | ✅ 良好 | 知识图谱索引，结构清晰 | | `IDENTITY.md` | ⚠️ 需微调 | 角色定义完整，但可补充"Tyler"商务身份的详细边界 | [score=0.884 recalls=0 avg=0.620 source=memory/2026-06-05-0843.md:111-114]
