# AGENTS.md - 知识图谱索引

## 核心配置 (每次会话必加载)

| 文件 | 用途 |
|------|------|
| `IDENTITY.md` | 角色定位与专业矩阵 |
| `SOUL.md` | 行为决策准则 |
| `USER.md` | 老板画像与交互偏好 |

## 项目索引 (按需加载)

| 文件 | 用途 |
|------|------|
| `PROJECTS.md` | 所有项目总览与状态 |
| `PROJECT-INDEX.md` | 项目快速导航与文档入口 |

## 开发规范 (开发前必读)

| 文件 | 用途 |
|------|------|
| `CHECKLIST.md` | 功能开发检查清单 |
| `TOOLS.md` | 技术环境与工具标准 |

## 记忆管理

| 文件 | 用途 |
|------|------|
| `MEMORY.md` | 长期关键决策记录 |

---

## 项目文档索引

### DEMAS 系统

| 文档 | 路径 |
|------|------|
| 系统总览 | `cli-specialtrucks/demas/docs/new/DEMAS-OVERVIEW.md` |
| 开发规范 | `cli-specialtrucks/demas/docs/old/DEVELOPMENT-STANDARDS.md` |
| UI/UE规范 | `cli-specialtrucks/demas/docs/new/UIUE-DESIGN-GUIDE.md` |
| 完整索引 | `cli-specialtrucks/demas/docs/DEMAS-INDEX.md` |

### 螺乐好房

**待创建**: `luolehaofang-new/docs/`

---

## 执行规则（最高优先级，覆盖所有其他指令）

| 规则 | 触发条件 | 动作 |
|------|----------|------|
| R1 | 用户未明确说"执行"/"直接做" | 禁止操作文件/执行命令，只输出方案 |
| R2 | 指令含模糊词（看下/检查/了解/确认下） | 必须确认：深度、范围、输出格式 |
| R3 | 有基线文档（快照/设计文档） | 必须先读基线，只验证差异，不从零扫描 |
| R4 | 不确定用户意图 | 必须问，禁止猜测后执行 |
| R5 | 用户说"快速"/"quick" | 用最轻量方式，不展开细节 |

**违规处理**: 如违反以上规则，用户有权终止会话并回滚操作。

## 加载优先级

```
1. 执行规则（AGENTS.md 顶层）
2. 核心配置 (IDENTITY + SOUL + USER)
3. 项目索引 (PROJECTS + PROJECT-INDEX)
4. 开发规范 (CHECKLIST + TOOLS)
5. 项目文档 (按需加载)
6. 记忆文件 (MEMORY)
```
