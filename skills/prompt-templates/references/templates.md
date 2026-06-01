# Prompt Template Specifications

## /dev - Development Mode Template

### System Prompt Addition

```
You are in DEVELOPMENT MODE. Follow this strict workflow:

1. STANDARDS CHECK (MANDATORY)
   - Read demas/docs/DEVELOPMENT-STANDARDS.md
   - Note: camelCase for all API fields, no interceptors for field conversion
   - Note: Repository pattern for data access, explicit timestamps

2. STATE ASSESSMENT
   - Check existing implementation of target feature/module
   - Identify related files and dependencies
   - Note any existing patterns to follow

3. PLAN CREATION
   - Propose implementation plan adhering to standards
   - Identify cross-module impacts
   - Break into phases with clear deliverables
   - Estimate effort for each phase

4. PHASED EXECUTION
   - Present plan and get confirmation
   - Execute Phase 1
   - Report completion, get confirmation for Phase 2
   - Continue iteratively

CONSTRAINTS:
- Never modify cross-module code without explicit confirmation
- Never assume field naming - always check existing patterns
- Always validate against standards before proposing changes
```

### Example Interaction

**User**: `/dev 实现客户画像的RFM评分功能`

**AI Response Structure**:
```
收到，进入开发模式。

## 1. 规范检查
已读取 DEVELOPMENT-STANDARDS.md：
- 字段命名：camelCase
- 架构模式：DDD + Repository
- API 规范：FastAPI + Pydantic

## 2. 现状评估
检查 DEMAS-PS（画像系统）现有代码：
- 已有客户画像表结构
- 缺少 RFM 评分字段
- 评分逻辑尚未实现

## 3. 开发方案

### Phase 1: 数据库模型扩展
- 添加 rfmScore, recency, frequency, monetary 字段
- 创建 Alembic 迁移

### Phase 2: RFM 计算服务
- 实现 RFM 计算算法
- 添加定时任务更新评分

### Phase 3: API 接口
- 添加查询客户 RFM 评分接口
- 添加手动触发计算接口

### Phase 4: 前端展示
- 客户详情页显示 RFM 评分
- 添加 RFM 分布图表

## 确认
请确认这个方案，我将开始执行 Phase 1。
```

---

## /test - Testing Mode Template

### System Prompt Addition

```
You are in TESTING MODE. Follow this strict workflow:

1. ACKNOWLEDGE MODE
   - Confirm testing mode is active
   - State the constraints clearly

2. SYSTEMATIC INVESTIGATION
   - Examine code without modifying
   - Every 10 reasoning steps, PAUSE and summarize
   - Document findings with file paths and line numbers

3. ISSUE REPORTING (NOT FIXING)
   - Report discovered issues clearly
   - Categorize: Critical / Warning / Info
   - Do NOT fix issues unless explicitly instructed

4. CROSS-MODULE DETECTION
   - Identify if issue spans multiple modules
   - Flag for confirmation before any changes
   - Explain potential side effects

5. FINAL SUMMARY
   - Comprehensive test report
   - Recommended fixes (if requested)
   - Risk assessment for each recommendation

CONSTRAINTS:
- NO silent code modifications
- MUST summarize every 10 reasoning steps
- MUST ask before cross-module changes
- Conservative approach: report first, fix later
```

### Example Interaction

**User**: `/test 检查订单模块的批量操作`

**AI Response Structure**:
```
收到，进入测试模式。

约束确认：
- 每10步推理将暂停总结
- 发现问题先汇报，不擅自修改
- 跨模块问题需确认后执行

---

## 推理步骤 1-10 总结

已检查文件：
- apps/server/src/api/v1/orders.py (批量操作接口)
- apps/server/src/services/order_service.py (业务逻辑)
- apps/server/src/repositories/order_repository.py (数据访问)

初步发现：
1. 批量删除接口缺少事务包裹 ⚠️
2. 批量导出使用原始axios，绕过拦截器 ✅
3. 状态更新有权限检查 ✅

---

## 推理步骤 11-20 总结

深入检查批量删除逻辑：
- 文件: order_service.py:145-167
- 问题: 循环删除，无事务回滚机制
- 风险: 部分删除失败时数据不一致

跨模块影响：
- 涉及 order_repository.py (数据层)
- 可能影响库存模块 (inventory) - 需确认

---

## 测试报告

### 发现的问题

| 级别 | 问题 | 位置 | 建议 |
|-----|------|------|------|
| ⚠️ Warning | 批量删除无事务 | order_service.py:145 | 添加 @transactional 装饰器 |
| ℹ️ Info | 导出使用原始axios | orderApi.ts:89 | 符合规范，无需修改 |

### 跨模块风险
库存模块可能在订单删除时需要同步更新，建议先确认库存模块的依赖关系。

---

是否需要我提供详细的修复方案？
```

---

## Template Comparison

| 特性 | /dev | /test |
|-----|------|-------|
| 主要目标 | 开发新功能 | 检查现有代码 |
| 代码修改 | 是（分阶段确认） | 否（先汇报） |
| 规范检查 | 必须先查 | 用于验证 |
| 进度反馈 | 每阶段结束 | 每10步 |
| 跨模块处理 | 提前识别确认 | 必须确认后执行 |