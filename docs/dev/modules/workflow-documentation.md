# 工作流文档模块

> 文档元数据
> - 文档类型：module
> - 文件路径：docs/dev/modules/workflow-documentation.md
> - 文档版本：v1.0.0
> - 最后更新：2026-07-02
> - 维护范围：Agent 工作流中的本地上下文文档、模块文档、任务索引和独立任务文档策略。

## 1. 模块边界

- 职责：定义 `docs/dev` 的文档落点、索引方式、模块文档维护方式、独立编号文档触发条件，以及提交时文档与代码的关系。
- 非职责：不记录单次任务的完整流水账，不替代产品总文档 `docs/overview-product.md` 或开发总文档 `docs/overview-product-dev.md`。
- 相关规则路径：`AGENTS.md`、`.dj-agent/README.md`、`.dj-agent/guide/00-routing.md`、`.dj-agent/guide/10-research.md`、`.dj-agent/guide/20-plan.md`、`.dj-agent/guide/40-summary.md`、`.dj-agent/guide/99-appendix.md`。
- 相关模板路径：`.dj-agent/dev-index-template.md`、`.dj-agent/module-doc-template.md`、`.dj-agent/task-lite-template.md`、`.dj-agent/fix-lite-template.md`。

## 2. 当前行为

- `docs/dev/README.md` 是任务与模块变更索引，记录 L1+ 中需要沉淀的变更。
- `docs/dev/modules/[module].md` 是功能开发和 bug 修复的默认文档落点，按模块维护当前行为、关键约束、验证方式、故障模式和变更记录。
- L1/L2 默认不新建独立 `docs/dev/[N]-*.md`；普通功能开发和 bug 修复只更新索引与相关模块文档。
- 独立编号文档只用于 L3/L4、复杂 bug、跨模块方案取舍、专项评审/审计、用户明确要求，或不适合写入模块文档的过程性复盘。
- 提交时，本次相关代码、长期文档、`docs/dev` 索引、模块文档和独立任务文档同次提交；无关历史文档和敏感信息不纳入提交范围。

## 3. 关键约束

- 模块文档记录长期可复用事实，不堆叠临时排查过程。
- 索引只保留检索所需摘要，不复制完整方案。
- 单个模块文档超过 500 行时，按子模块拆分为 `docs/dev/modules/[module]-[topic].md`。
- 新增独立文档时才分配全局编号，编号不可复用。
- 文档修改必须与当前需求直接相关，不顺手整理无关历史内容。

## 4. 验证方式

| 场景 | 验证命令/步骤 | 备注 |
|------|---------------|------|
| 规则引用一致性 | `rg -n "默认.*新建|docs/dev|modules|task-lite|fix-lite" AGENTS.md .dj-agent README.md docs/dev` | 检查是否仍存在 L2 默认新建独立文档的冲突规则 |
| Markdown 基础检查 | `git diff --check` | 检查尾随空白等格式问题 |
| 提交范围检查 | `git status --short` | 确认只包含本次相关规则、模板和文档 |

## 5. 故障模式与修复记录

| 日期 | 类型 | 现象/需求 | 处理结果 | 验证 |
|------|------|-----------|----------|------|
| 2026-07-02 | task | L1/L2 每次默认新建任务文档，导致 `docs/dev` 文件数量随开发频率爆炸增长。 | 改为模块文档 + 索引默认模式，独立任务文档改为复杂场景例外。 | `rg` 一致性检查、`git diff --check` |

## 6. 变更记录

| 日期 | 关联提交/文档 | 变更 | 影响 |
|------|---------------|------|------|
| 2026-07-02 | 本次提交 | 新增模块文档策略，调整 L1/L2 默认文档落点，新增模块文档模板，并取消 `docs/` 忽略。 | 降低任务文档数量，保留模块级长期上下文和索引追溯能力。 |
