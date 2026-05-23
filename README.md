# workflow

> AI Agent 工作流规范仓库。

## 快速入口

- Agent 入口：`AGENTS.md`
- 项目覆盖层：`AGENTS.project.md`（由 `.dj-agent/AGENTS.project-template.md` 初始化）
- 阶段规则：`.dj-agent/guide/`
- 轻量模板：`.dj-agent/task-lite-template.md`、`.dj-agent/summary-lite-template.md`
- 完整模板：`.dj-agent/001-research-template.md`、`.dj-agent/002-plan-template.md`、`.dj-agent/003-summary-template.md`
- 产品文档：`docs/overview-product.md`
- 开发文档：`docs/overview-product-dev.md`
- 任务索引：`docs/dev/README.md`

## 核心策略

- L0/L1：小任务走轻流程，避免文档成本大于改动本身。
- L2：默认单文件轻量任务记录。
- L3/L4：完整 Research -> Plan -> Code -> Summary。
- Code 阶段必须明确验证命令或可复现实测步骤。
- 每个项目的长期配置、安全边界和固定验证要求写入 `AGENTS.project.md`，共享工作流升级时必须保留并持续遵守。
