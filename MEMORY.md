# MEMORY.md - 长期跨项目关键决策记录

## 核心系统更迭
- **【2026-02】控制界面迁移**: 遵照所有者明确指令，系统控制与自动化管理接口已全面从微信（WeChat）切出，强制迁移至飞书（Feishu / Lark）平台，以此确保企业级集成的稳定性与底层开发生态的平滑对接。
- **【2026-02】执行模型变更**: 系统底层调度与上下文推理核心已全面切换至 Kimi (Moonshot AI)。后续所有复杂长文本处理与增量 Diff 生成，均需基于 Kimi 企业账号的 Token 闭环控制逻辑进行极致优化。
- **【2026-03】逻辑收敛判定**: 核心系统与全局底座已全面清理并移除所有与“特种车海外 B2B 贸易/销售自动化”及“技术工程落地”无关的冗余业务逻辑。智能体决策链已进入纯净克制状态，严禁擅自蔓延或进行跨领域越界推理。

---

## 运行时状态看板

### 🔄 会话续读快照（2026-08-02 11:40，老板将重启 session，新会话必读）

**项目**: drawing-review-system（图纸智能审查系统），方案B（SW 原生 SLDDRW）重建期

**🔄 会话续读快照（2026-08-02 18:20 收工，新会话必读）**

| 项 | 状态 |
|---|---|
| B-M1 智能骨架 | ✅ 代码+单测已交付：type_recognition.py（5类识别）+ view_strategy.py（视图策略库）+ 布局算法；简报 B-M1_DELIVERY_REPORT.md；未提交 git |
| 标题栏 | 属性键已改“质量”（老板实证模板绑 $PRPSHEET:{质量}）；比例格 1:100 是页比例，**不是 bug 不改** |
| 待办① | **老板真机自验 B-M1**：SW 跑 LB26，看比例大小/四视图（主右俯轴测）/布局/占位符删除 |
| 待办② | 验收过 → git 提交 → 派 B-M2（Step5 原生BOM+球标、Step6 InsertNote） |
| 待办③ | 其他 4 类零件（标准件/板类/焊接件/小装配）各补一个案例图，给一个验一类 |

**本期新纪律（18:20 版）**：①老板没回复前禁止派活；②执行任务前先反思设计、需求不明先沟通；③弱化真机测试——dev 只写代码+单测（mock COM），真机验收归老板自己看；④禁止读参考 DWG 文件（模板已从案例提取）；⑤骨架用规则不用 AI（AI 留 B-M3/B-M4）；⑥子代理完成事件可能不推送（会话可见性受限），主代理改用 git 文件系统核实交付物。

**历史状态**
- 文档体系 | 已重编：docs/00索引+01总计划+02方案B设计+03业务需求+04图纸参考+assets/资产手册（分册）；老方案全套在 archive/2026-08-02-DXF路线/ |
| git 基线 | 已推 GitHub：ff42bc6(M2终态)→…→13709df(P2)→e2da6b9(docs重建) |
| 测试基线 | 278通过/16跳过（全绿） |
| 验收基准 | LB26拉臂装置/LB26.00000拉臂总成.DWG（老板确认；SLDDRW 是空白模板仅作格式参考） |
| P2 三 Spike | ✅ 全 VALIDATED（spikes/001-sw-native/VERDICT.md）：尺寸导入删除/真图快照/企业模板 |

**进行中的子代理任务（重启后用 subagents list 查收）**：
1. `bm1_step37_rewrite`（dev）：P3/B-M1 后端 Step3/7 重写（真图纸骨架）
2. `bm1_frontend_timeline`（dev）：✅ 已完成——前端步骤回放+快照路由（10 个失败属后端阵地，后端收尾后应全绿）
3. `asset_handbook`（doc-sync）：docs/assets/ 资产手册分册编写中（若残留单文件 10-现状资产手册.md 需删除）

**重启后动作**：①收 dev 的 B-M1 交付简报→转 tester 补测试→reviewer 审查→**请老板在 /generate 页面逐步快照验收（验收门禁：通过才动 B-M2）**；②收 doc-sync 手册→提交 git；③B-M1 验收过则派 B-M2（Step5 原生BOM+球标、Step6 InsertNote）

**本期铁规**：每里程碑交付即停等老板验收；前后端共同推进（派活时两线一起下）；主代理不自己动手实现，只做简报/验收/中转；SW 使用走"申请-归还"协议（见下行铁律）

### 历史状态
- **Control UI Status**: Control UI override has been successfully cleared.
- **Active Persona**: Active. Complete rollback to the native dual-identity routing defined in `IDENTITY.md` (Internal: Cai Shen / External: Tyler).

---

## 子代理体系（2026-07-30 落地）

- **四子代理就位**: dev（开发）/ tester（测试，只报不修）/ reviewer（只读审查）/ doc-sync（文档同步）。配置在 `openclaw.json agents.list`，各自独立工作区 `workspace/<id>/`，宪法三件套 = SOUL.md（角色契约）+ TOOLS.md（工具约束）+ USER.md（极简偏好）。
- **协作纪律**: 单向流水线 dev → tester → reviewer → doc-sync，子代理间禁止互调（配置层 deny sessions_send/sessions_spawn 双保险），一切经主代理中转。主代理 `subagents.allowAgents` 白名单已含四者。
- **工具配置教训**: `profile: minimal` 只含 session_status，子代理必须用 `profile: coding` + `deny` 做减法；`compaction` 只能在 agents.defaults 层配置，单代理级非法；`allowAgents`/`tools.profile`/`tools.deny` 均为保护路径，热更新被拦截，必须改文件重启。
- **项目切换约定**: 一句话指令（"切到 X"）→ 主代理读目标项目 `CONTEXT.md`（五段式舱单：定位/技术栈/拓扑/里程碑/禁区）+ 最新进度快照即开工。drawing-review-system 已建 CONTEXT.md；螺乐好房、DEMAS 目录未找到（待老板提供路径）。
- **角色归位**: 产品经理/架构师角色保留在主代理（对话密集型），不做成子代理（2026-07-30 与老板确认）。

## 执行宪法铁律（2026-06-12 新增）

**【绝对铁律】完全遵循设计，不擅自删减**

- 所有技术选型、架构设计、模块划分必须严格遵循文档
- 即使有更简单的方案，也必须按设计实现
- 疑问必须先提出确认，严禁猜测和擅自做主
- 每次执行前默念此铁律

**【2026-07-30 增补】**
- 设计文档中明确写出的技术选型，任何变更必须请示，无论大小（STEP→STL 事件）
- 未核实的假设禁止写入正式文档（SW 许可误报事件）；事实存疑必须先问老板
- 大任务不要求一次性完成，遇到问题随时沟通反馈，分步推进

**【2026-08-02 增补】**
- **方案审查基线铁律**: 方案/代码审查的基线必须是用户可验收的真实样例（如 LB26 案例图纸），禁止用内部设计文档当基线（自证无效）；每里程碑验收第一项 = 目视对比真实样例（M2 盲审事件）
- **验收基准确认**: LB26.00000拉臂总成.SLDDRW 经 spike 证实是空白模板图，真实完成图纸是同目录 .DWG 文件——引用"案例图纸"前必须先核实内容
- **SW 使用协调协议**: 需用 SW 前向老板申请"SW 归我用 N 分钟"，期间老板不碰 SW；用完归还；严禁启动/强杀 SW 进程（老板显式授权启动除外），弹窗卡死一律喊人，禁止自动关窗 hack
- **主代理动手纪律**: 多轮迭代型调试/实现工作一律派 dev 子代理，主代理只做简报设计、验收、中转（2026-08-02 老板批评事件）
- **需求背景（老板亲定）**: 图纸生成系统的目标是"给 3D 模型 → 输出生产工程图，减少工作量"。AI 辅助生成**可以实现的部分**，做不到的**留给人补**（人机协同是设计目标，不是缺陷）。禁止追求 100% 全自动完美生成而过度工程。
- **SW API 原生优先铁律**: 凡 SolidWorks 原生 API/导出能力能做的事（视图、隐藏线、DXF/DWG 导出、BOM、模板标题栏），**一律走原生，严禁重复造轮子**（逐边提取几何、自写投影/HLR、自绘 SW 能画的东西，均属违例）。老板从未要求"不依赖 SW 也能生成"，此类表述在一切文档/代码/记忆中均属错误，发现即清。
- **子代理重试纪律**: 同一失败重试 ≤2 次，第 3 次必须停止并上报主代理；禁止私自写"自动关弹窗"之类的续命 hack 代替上报（dialog_watch 事件）。
- **【2026-08-02 增补】重试按环节计数，非按假设计数**: "换了新假设所以重新计数"属违例——同一环节（如标题栏属性写入）连续试探 ≤2 次未果即停手上报；严禁无止境试错。SW API 存疑优先走"老板查官方文档"通道，禁止盲试参数组合。
- **SW API 文档通道**: SolidWorks API 行为存疑时，子代理把问题列成精确清单（成员名+疑问+现象）报主代理转老板查官方文档，拿到答案再动手。
- **强杀 SW 进程是高危操作**: 会损坏 SW 用户配置（默认模板失效→后续 COM 全挂），非老板指令不得执行（2026-08-01 半天事故）。

**【2026-08-04 增补】**
- **小任务跳过流水线（老板批准，例外于“一律派 dev”铁律）**: 预估变更 ≤2 文件且 ≤100 行的任务，主代理直接实现，不派子代理；超出此标准才走 dev→tester→reviewer 流水线。
- **简报精确化纪律**: 派活简报优先给“文档 X 的第 N 节”或直接摘录关键段落，禁止甩整本设计文档路径；优先给项目舱单 CONTEXT.md（≤3k 字快照）；大设计文档仅在设计有变更时才给对应章节。子代理无跨会话记忆，重复读文档是纯浪费。
- **模型调整**: dev 主模型 = moonshot/kimi-k2.7-code（256K，思考常开，fallback k3）；主代理 k3 contextWindow 降为 262144（API 模型不变，仅压缩管理窗口），compaction reserveTokens 同步降为 32768。
- **子代理写入路径铁律（2026-08-04 stranded B-M2 事件）**: 派活简报必须写明项目代码的**绝对路径**（如 `E:\147\workspaces\drawing-review-system`），严禁子代理在项目副本/自己工作区写代码；交付验收第一项 = git status 核实变更落在真项目。子代理工作区只允许写临时分析稿，不允许建项目目录结构。

## 纠错防线（2026-07-30，防新会话遗忘）

三道持久化防线，按加载优先级排序：
1. **TOOLS.md「环境事实」表**：本机环境类事实（Shell类型/编码/SW版本），每次会话必加载，消灭"环境假设"类错误
2. **MEMORY.md 铁律增补**：决策类教训（请示边界/假设禁入文档/分步推进）
3. **子代理 SOUL.md**：角色级教训沉淀到对应代理宪法（如 reviewer 八维度）

新事实登记顺序：先 TOOLS.md 环境事实表 → 再 MEMORY.md → 需要时进子代理宪法。

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

## Promoted From Short-Term Memory (2026-06-13)

<!-- openclaw-memory-promotion:memory:memory/2026-06-05-0843.md:115:117 -->
- | `SOUL.md` | ✅ 良好 | 执行宪法，铁律明确 | | `TOOLS.md` | ⚠️ 轻量 | 物理环境标准，但缺"当前活跃项目技术栈速查" | | `USER.md` | ✅ 良好 | 所有者画像 + 防线清晰 | [score=0.846 recalls=0 avg=0.620 source=memory/2026-06-05-0843.md:115-117]
<!-- openclaw-memory-promotion:memory:memory/2026-06-05-0843.md:144:147 -->
- | 项目 | 前端 | 后端 | 数据库 | 部署 | |------|------|------|--------|------| | DEMAS | Vue3 | Node.js/Express | PostgreSQL | Docker | | 螺乐好房 | 微信小程序 | Node.js | MySQL | 腾讯云 | [score=0.846 recalls=0 avg=0.620 source=memory/2026-06-05-0843.md:144-147]

## Promoted From Short-Term Memory (2026-06-15)

<!-- openclaw-memory-promotion:memory:memory/2026-06-10-1231.md:9:9 -->
- user: [Wed 2026-06-10 03:11 GMT+8] Write a dream diary entry from these memory fragments: [score=0.844 recalls=0 avg=0.620 source=memory/2026-06-10-1231.md:9-9]
