# AGENTS.md

> Agent 行为指南（入口索引版）：默认只加载本文件，再按阶段增量加载对应分片，减少上下文占用。

## 0. 使用方式（先看这里）

- 启动时仅加载：`AGENTS.md` + `.dj-agent/guide/00-routing.md`
- 进入 Research 阶段：追加加载 `.dj-agent/guide/10-research.md`
- 进入 Plan 阶段：追加加载 `.dj-agent/guide/20-plan.md`
- 进入 Code 阶段：追加加载 `.dj-agent/guide/30-code.md`
- 进入 Summary 阶段：追加加载 `.dj-agent/guide/40-summary.md` + `.dj-agent/guide/50-review-checklist.md`
- 出现争议、回退、需求变更：按需追加 `.dj-agent/guide/99-appendix.md`

按级别加载 `50-review-checklist.md`：
- L1：默认仅在 Summary 阶段加载并执行 L1 裁剪项。
- L2：在 Plan、Summary 阶段加载并执行 L2 裁剪项。
- L3/L4：在 Research、Plan、Code、Summary 每阶段加载并执行全量项。

## 1. 快速路由

- 需求分级与阶段触发：`.dj-agent/guide/00-routing.md`
- Research 规则：`.dj-agent/guide/10-research.md`
- Plan 规则：`.dj-agent/guide/20-plan.md`
- Code 规则：`.dj-agent/guide/30-code.md`
- Summary 规则：`.dj-agent/guide/40-summary.md`
- 三角色审视清单：`.dj-agent/guide/50-review-checklist.md`
- 回退/变更处理与附录：`.dj-agent/guide/99-appendix.md`

## 2. 全局约束（始终生效）

- 不要假设。不要隐藏困惑。揭示权衡；不确定时先提问。
- 简洁优先：用最少代码解决问题，不做推测性设计。
- 精准修改：只改与需求直接相关的内容，不顺手重构无关代码。
- 目标驱动：将任务写成可验证目标，循环直到验证通过。
- 与现有风格保持一致；仅清理由本次修改引入的孤儿代码。

## 3. 文档入口

- 产品设计文档：`docs/overview-product.md`
- 开发设计文档：`docs/overview-product-dev.md`
- 需求文档索引：`docs/dev/README.md`
- 模板目录：`.dj-agent/`

## 4. 维护规则

- 新增规则时，优先写入对应分片，不在本文件堆叠细节。
- 本文件只保留：加载策略、路由索引、全局约束。
- 当分片超过 500 行时继续拆分，并在对应分片顶部加导航链接。
