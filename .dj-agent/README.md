# AGENTS.md

> Agent 行为指南（入口索引版）：默认只加载本文件，再按阶段增量加载对应分片，减少上下文占用。

## 0. 使用方式（先看这里）

- 启动时仅加载：`AGENTS.md` + `.dj-agent/guide/00-routing.md` + `.dj-agent/guide/05-safety-gates.md`
- 进入 Research 阶段：追加加载 `.dj-agent/guide/10-research.md`
- 进入 Plan 阶段：追加加载 `.dj-agent/guide/20-plan.md`
- 进入 Code 阶段：追加加载 `.dj-agent/guide/30-code.md` + `.dj-agent/guide/60-validation.md`
- 进入 Summary 阶段：追加加载 `.dj-agent/guide/40-summary.md` + `.dj-agent/guide/50-review-checklist.md`
- 出现争议、回退、需求变更：按需追加 `.dj-agent/guide/99-appendix.md`

按级别加载 `50-review-checklist.md`：
- L0：不加载清单，只做最小验证与一句话记录。
- L1：默认仅在 Summary 阶段加载并执行 L1 裁剪项。
- L2：在 Plan、Summary 阶段加载并执行 L2 裁剪项，可使用轻量任务文档合并记录。
- L3/L4：在 Research、Plan、Code、Summary 每阶段加载并执行全量项。

## 1. 快速路由

- 需求分级与阶段触发：`.dj-agent/guide/00-routing.md`
- 安全门禁与破坏性操作禁令：`.dj-agent/guide/05-safety-gates.md`
- Research 规则：`.dj-agent/guide/10-research.md`
- Plan 规则：`.dj-agent/guide/20-plan.md`
- Code 规则：`.dj-agent/guide/30-code.md`
- Summary 规则：`.dj-agent/guide/40-summary.md`
- 多角色审视清单：`.dj-agent/guide/50-review-checklist.md`
- 验证命令约定：`.dj-agent/guide/60-validation.md`
- 回退/变更处理与附录：`.dj-agent/guide/99-appendix.md`

## 2. 全局约束（始终生效）

- 不要假设。不要隐藏困惑。揭示权衡；不确定时先提问。
- 简洁优先：用最少代码解决问题，不做推测性设计。
- 精准修改：只改与需求直接相关的内容，不顺手重构无关代码。
- 目标驱动：将任务写成可验证目标，循环直到验证通过。
- 与现有风格保持一致；仅清理由本次修改引入的孤儿代码。
- 小任务优先走轻流程；只有影响范围、接口、数据、安全或架构发生变化时才升级流程。
- 安全门禁始终优先：任何分级裁剪都不能绕过破坏性操作禁令、工作区保护和高风险开发门禁。

## 3. 文档入口

- 产品设计文档：`docs/overview-product.md`
- 开发设计文档：`docs/overview-product-dev.md`
- 需求文档索引：`docs/dev/README.md`
- 模板目录：`.dj-agent/`

## 4. 模板选择

- L0：不建文档，在最终回复中说明修改与验证即可。
- L1：按需使用 `.dj-agent/summary-lite-template.md`。
- L2：默认使用 `.dj-agent/task-lite-template.md`，将 Research、Plan、Summary 合并成单文件。
- L3/L4：使用完整模板 `.dj-agent/001-research-template.md`、`.dj-agent/002-plan-template.md`、`.dj-agent/003-summary-template.md`。
- 代码提交说明：使用 `.dj-agent/commit-message-template.md`。

## 5. 总文档更新规则

- 影响长期产品行为、用户流程或功能边界时，更新 `docs/overview-product.md`。
- 影响架构、公共接口、数据模型、依赖、部署或验证方式时，更新 `docs/overview-product-dev.md`。
- 仅实现细节变化时，不强制更新总文档；在任务 Summary 中记录即可。
- 每个 L2+ 任务都应更新 `docs/dev/README.md` 索引。

## 6. 维护规则

- 新增规则时，优先写入对应分片，不在本文件堆叠细节。
- 本文件只保留：加载策略、路由索引、全局约束、模板选择与总文档更新规则。
- 当分片超过 500 行时继续拆分，并在对应分片顶部加导航链接。
