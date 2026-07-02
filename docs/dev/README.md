# 需求、任务与模块变更索引

> 记录 L1+ 需要沉淀的功能开发、bug 修复、调研、计划、总结、评审和模块文档变更。新需求/问题优先读取本索引，再按相关性展开模块文档和少量独立文档，避免加载完整历史上下文。

## 独立文档编号规则

- 功能开发和 bug 修复默认更新模块文档，不分配编号。
- 只有新增独立任务、问题修复、调研、计划、总结、评审或需求变更文档时，才分配编号。
- 独立文档编号使用从 `1` 开始递增的正整数，不要求固定位数。
- 编号全局只在 `docs/dev/` 下递增，不按类型分别编号。
- 新增独立文档前，先检查本索引和 `docs/dev/` 现有编号文件名，取最大编号 + 1。
- 同一需求的多份独立文档使用同一编号，例如 `2-research-xxx.md`、`2-plan-xxx.md`、`2-summary-xxx.md`。
- 编号一旦分配不得复用；取消、废弃、拆分、合并也要在索引中保留记录并标注状态。
- 文件命名格式：`N-[type]-[slug].md`，其中 `type` 可取 `summary`、`task`、`fix`、`research`、`plan`、`review`。
- 模块文档命名格式：`modules/[module].md`。

## 索引

| 日期 | 级别 | 模块 | 类型 | 关联文档 | 状态 | 摘要 |
|------|------|------|------|----------|------|------|
| 2026-06-23 | L2 | project-overlay | task | [1-task-project-overlay-template.md](1-task-project-overlay-template.md) | 已完成 | 将项目特有配置和安全边界抽成持久覆盖模板，存在时自动加载且默认只读，只有用户明确指明时才允许修改。 |
| 2026-07-02 | L2 | workflow-documentation | module | [modules/workflow-documentation.md](modules/workflow-documentation.md) | 已完成 | 将 L1/L2 默认文档落点从每次新建独立任务文档改为模块文档 + 索引，独立文档只用于复杂场景。 |
