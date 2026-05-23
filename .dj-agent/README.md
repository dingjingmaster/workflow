# AGENTS.md

> Agent 行为指南（入口索引版）：默认加载共享入口、项目覆盖层与安全门禁，再按阶段增量加载对应分片，减少上下文占用。

## 0. 使用方式（先看这里）

- 框架启动时仅加载：`AGENTS.md` + `AGENTS.project.md`（如存在）+ `.dj-agent/guide/00-routing.md` + `.dj-agent/guide/05-safety-gates.md`
- 进入具体新需求后：按 `.dj-agent/guide/00-routing.md` 的加载策略追加索引和相关 Summary。
- 进入 Research 阶段：追加加载 `.dj-agent/guide/10-research.md`
- 进入 Plan 阶段：追加加载 `.dj-agent/guide/20-plan.md`
- 进入 Code 阶段：追加加载 `.dj-agent/guide/30-code.md` + `.dj-agent/guide/60-validation.md`
- 进入 Summary 阶段：追加加载 `.dj-agent/guide/40-summary.md`；审视清单按 `.dj-agent/guide/00-routing.md` 的加载时机加载 `.dj-agent/guide/50-review-checklist.md`
- 出现争议、回退、需求变更：按需追加 `.dj-agent/guide/99-appendix.md`
- 用户在工作中给出“本项目长期有效”的配置、安全边界或操作要求时，先写入或更新 `AGENTS.project.md`，后续任务必须自动加载并遵守。

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

- 不要假设。不要隐藏困惑。揭示权衡；先快速探查，仍不确定或涉及取舍/风险时再提问。
- 简洁优先：用最少代码解决问题，不做推测性设计。
- 精准修改：只改与需求直接相关的内容，不顺手重构无关代码。
- 目标驱动：将任务写成可验证目标，循环直到验证通过。
- 与现有风格保持一致；仅清理由本次修改引入的孤儿代码。
- 小任务优先走轻流程；只有影响范围、接口、数据、安全、性能、稳定性、依赖、部署或架构发生变化时才升级流程。
- 闭环交付：每次完成修改后同步更新当前任务文档进度；验证通过后按提交模板提交本次相关变更。
- 安全门禁始终优先：任何分级裁剪都不能绕过破坏性操作禁令、工作区保护和高风险开发门禁。
- 项目覆盖层始终生效：`AGENTS.project.md` 中的项目特有配置、安全边界、验证要求和禁止触碰范围必须在每次修改前读取；与共享规则冲突时执行更严格、更具体的规则，仍无法判断时暂停询问。
- 项目特有规则必须保留：不得在更新共享工作流或同步模板时覆盖、删除、降级 `AGENTS.project.md` 中已有规则；只有用户明确要求变更时才可修改，并保留变更记录。

## 3. 文档入口

- 产品设计文档：`docs/overview-product.md`
- 开发设计文档：`docs/overview-product-dev.md`
- 需求文档索引：`docs/dev/README.md`（不存在时，首次创建 L1+ 文档前用 `.dj-agent/dev-index-template.md` 初始化）
- 项目特有配置：`AGENTS.project.md`（不存在且用户给出长期配置时，用 `.dj-agent/AGENTS.project-template.md` 初始化）
- 模板目录：`.dj-agent/`
- 详细设计片段：`.dj-agent/fragments/`

## 4. 模板选择

| 场景 | 模板 | 输出位置 |
|------|------|----------|
| L0 小改 | 不建文档 | 最终回复说明修改与验证 |
| L1 轻量总结 | `.dj-agent/summary-lite-template.md` | `docs/dev/[N]-summary-[slug].md` |
| 普通任务/功能（L2） | `.dj-agent/task-lite-template.md` | `docs/dev/[N]-task-[slug].md` |
| Bug/问题修复（L2） | `.dj-agent/fix-lite-template.md` | `docs/dev/[N]-fix-[slug].md` |
| L3/L4 完整流程（含复杂 bug 修复） | `.dj-agent/001-research-template.md` + `.dj-agent/002-plan-template.md` + `.dj-agent/003-summary-template.md` | 同一 `N` 编号的多份文档 |
| L4 专项评审 | 无固定模板，按评审结论记录 | `docs/dev/[N]-review-[slug].md` |
| 总产品事实 | `.dj-agent/overview-product-template.md` | `docs/overview-product.md` |
| 总开发事实 | `.dj-agent/overview-product-dev-template.md` | `docs/overview-product-dev.md` |
| 项目特有配置 | `.dj-agent/AGENTS.project-template.md` | `AGENTS.project.md` |
| 详细设计片段 | `.dj-agent/fragments/` | 按需复制到任务文档或总文档 |
| 代码提交说明 | `.dj-agent/commit-message-template.md` | commit message / 提交注释 |
| 任务索引初始化 | `.dj-agent/dev-index-template.md` | `docs/dev/README.md` |

总文档模板只记录长期稳定事实；单次任务细节写入 `docs/dev/[N]-*.md`，API/数据/部署/性能/并发/内核等详细设计按需使用 `.dj-agent/fragments/`。

`AGENTS.project.md` 是每个项目的持久覆盖文件，只记录本项目长期有效的规则、配置和安全边界；共享工作流升级时不得覆盖该文件。

Todo list 规则：不新增独立 todo list 模板；执行清单边界见 `.dj-agent/guide/20-plan.md`。

## 5. 总文档更新规则

- 影响长期产品行为、用户流程或功能边界时，更新 `docs/overview-product.md`。
- 影响架构、公共接口、数据模型、依赖、部署、长期通用验证方式、项目级验证入口或发布验证标准时，更新 `docs/overview-product-dev.md`。
- 总文档只沉淀长期稳定事实，不记录单次实现过程、临时排查、阶段性计划或可从任务文档追溯的细节。
- 仅实现细节变化时，不强制更新总文档；在任务 Summary 中记录即可。
- L1+ 只要新增任务、问题、调研、计划、总结或评审文档，就必须分配从 `1` 开始递增的文件编号并更新 `docs/dev/README.md` 索引。

## 6. 项目特有配置保留规则

- `AGENTS.project.md` 是共享工作流之外的项目覆盖层，必须与 `AGENTS.md` 一起加载。
- 用户明确给出的“本项目以后都要遵守”“安全边界”“禁止触碰”“固定验证命令”“提交/部署约束”等长期规则，必须写入 `AGENTS.project.md` 后再继续修改项目。
- 如果用户说明某条规则仅对当前任务有效，不写入 `AGENTS.project.md`；如果意图不清且会影响后续行为，先询问。
- 更新 `AGENTS.project.md` 时只追加或精确修改相关条目，不删除历史规则；规则废弃时标记为“已废弃/被替代”，并保留原因与日期。
- `AGENTS.project.md` 不记录密钥、令牌、密码、私有证书正文或其它敏感值；只记录密钥所在的安全读取方式和禁止暴露规则。
- 共享模板更新、批量同步、格式化或重构不得覆盖 `AGENTS.project.md`；提交前必须检查它是否只包含本次用户明确要求的项目规则变更。

## 7. 维护规则

- 新增规则时，优先写入对应分片，不在本文件堆叠细节。
- 本文件只保留：加载策略、路由索引、全局约束、模板选择与总文档更新规则。
- 当分片超过 500 行时继续拆分，并在对应分片顶部加导航链接。
