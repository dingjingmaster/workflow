# 工作流轻量化优化任务记录

> 文档版本：v1.0.0
> 最后更新：2026-05-13
> 需求级别：L2
> 关联需求：分析并优化当前 AI Agent 工作流，一次性完成并提交

## 1. 目标

- 要解决的问题：当前工作流对中大型任务有效，但 L1/L2 小任务文档成本偏高，且 `docs/` 入口缺失。
- 成功标准：小任务有轻流程；L2 有单文件记录；验证命令有明确约定；总文档入口存在；变更可提交。

## 2. 背景与边界

- 背景：原流程已有分阶段加载和三角色审视，但 L2 仍强制 Research/Plan/Summary 分离，容易产生模板填充成本。
- 包含：路由规则、阶段规则、验证规则、轻量模板、docs 骨架、索引。
- 不包含：自动化文档生成器、CI 集成、具体业务项目规范。
- 关键假设：该仓库主要维护工作流规范和 Markdown 文档，不包含运行时代码。

## 3. 方案

- 推荐方案：增加 L0/Fast Path；L2 默认使用单文件轻量任务记录；L3/L4 保留完整模板；总文档按影响条件更新；新增验证命令约定。
- 取舍理由：保留严谨性给复杂任务，把日常小任务从重模板中释放出来。
- 风险与应对：轻流程可能记录不足，因此规定 L2+ 必须进入索引，升级条件明确覆盖接口、数据、安全、架构等高风险变化。

## 4. 执行计划

1. 调整 `AGENTS.md` 和 `00-routing.md` -> 验证：L0-L4 分级、模板选择、总文档更新规则一致。
2. 调整 Research/Plan/Code/Summary 分片 -> 验证：不再无条件强制更新总文档。
3. 新增验证规则和轻量模板 -> 验证：Code 阶段有可执行验证命令矩阵。
4. 补齐 `docs/` 骨架和任务索引 -> 验证：入口文件存在且索引可追溯。
5. 提交变更 -> 验证：`git diff --check` 通过，工作树只包含本次相关变更。

## 5. 实现记录

- 修改文件：`AGENTS.md`、`.dj-agent/guide/00-routing.md`、`.dj-agent/guide/10-research.md`、`.dj-agent/guide/20-plan.md`、`.dj-agent/guide/30-code.md`、`.dj-agent/guide/40-summary.md`。
- 新增文件：`.dj-agent/guide/60-validation.md`、`.dj-agent/task-lite-template.md`、`.dj-agent/summary-lite-template.md`、`docs/overview-product.md`、`docs/overview-product-dev.md`、`docs/dev/README.md`、`docs/dev/001-task-workflow-optimization.md`。
- 关键决策：L2 使用单文件任务记录，L3/L4 保留完整 Research/Plan/Summary。
- 计划偏差：无。

## 6. 验证记录

| 验证项 | 命令/步骤 | 结果 | 备注 |
|--------|-----------|------|------|
| 空白检查 | `git diff --check` | 通过 | 无空白错误 |
| 文件存在性 | `find AGENTS.md README.md .dj-agent docs -maxdepth 4 -type f | sort` | 通过 | 新增入口文件存在 |
| 规则一致性 | 人工阅读关键分片 | 通过 | L0/L2/总文档规则一致 |

## 7. 总结

- 最终结果：已完成 L0/L1/L2 轻量化、验证约定、docs 骨架和索引更新，随本次提交落库。
- 遗留风险：无自动化链接检查器，链接正确性通过人工阅读和文件存在性检查确认。
- 后续建议：如果使用频率提高，可增加脚本自动检查分片导航和 docs/dev 索引。
