---
name: prompt-templates
description: Prompt template wrappers for structured AI interactions. Use when the user prefixes their message with /dev or /test to trigger specific workflow modes. /dev = development mode (check standards, assess current state, propose plan, phased execution). /test = testing mode (summarize every 10 reasoning steps, report issues before fixing, avoid cross-module changes without confirmation).
---

# Prompt Templates

This skill provides structured prompt wrappers that modify how I process your requests based on the prefix command.

## Available Templates

### /dev - Development Mode

**Trigger**: Message starts with `/dev`

**Workflow**:
1. Read `demas/docs/DEVELOPMENT-STANDARDS.md` to understand current coding standards
2. Check the current state of the feature/module being discussed
3. Propose a development plan that adheres to standards
4. Break into phases with clear milestones
5. Execute phase by phase, confirming before moving to next

**Key Behaviors**:
- Always check standards first
- Assess existing code before proposing changes
- Present plan before implementation
- Get confirmation for each phase
- Flag cross-module impacts early

### /test - Testing Mode

**Trigger**: Message starts with `/test`

**Workflow**:
1. Acknowledge testing mode constraints
2. Every 10 reasoning steps, pause and summarize current findings
3. Report issues discovered without immediately fixing them
4. For cross-module or high-risk changes, ask for confirmation first
5. Document test results clearly

**Key Behaviors**:
- No silent code changes
- Regular progress summaries (every 10 steps)
- Issue reporting before fixing
- Conservative approach to modifications
- Clear communication of findings

## Usage Examples

```
/dev 帮我实现客户画像的RFM评分功能
→ 我会先查规范，检查现有代码，给方案，分阶段执行

/test 检查一下订单模块的批量操作是否有bug
→ 我会每10步总结，发现问题先汇报，不擅自修改
```

## Reference

See [references/templates.md](references/templates.md) for detailed template specifications and examples.