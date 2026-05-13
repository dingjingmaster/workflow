# AI Agent 工作流开发文档

> 文档版本：v1.0.0
> 最后更新：2026-05-13
> 更新来源：001-task-workflow-optimization
> 关联产品文档：docs/overview-product.md

## 1. 项目概述

本仓库是 AI Agent 工作流规范仓库，核心交付物是 Markdown 规则、模板和文档索引，不包含运行时代码。

## 2. 目录结构

```text
AGENTS.md                         # Agent 入口规则
README.md                         # 仓库简介
.dj-agent/                        # 工作流规则与模板
  guide/                          # 阶段分片规则
  *template.md                    # 完整/轻量模板
docs/                             # 项目长期文档
  overview-product.md             # 产品视角总文档
  overview-product-dev.md         # 开发视角总文档
  dev/README.md                   # 需求/任务索引
```

## 3. 规则加载架构

- `AGENTS.md` 只保留入口索引、全局约束、模板选择和总文档更新规则。
- `.dj-agent/guide/00-routing.md` 负责分级、阶段裁剪和升级触发。
- `.dj-agent/guide/10-research.md` 到 `.dj-agent/guide/40-summary.md` 负责阶段行为。
- `.dj-agent/guide/50-review-checklist.md` 负责按级别裁剪审视项。
- `.dj-agent/guide/60-validation.md` 负责验证命令约定。
- `.dj-agent/guide/99-appendix.md` 负责回退和变更处理。

## 4. 模板策略

| 级别 | 模板 | 用途 |
|------|------|------|
| L0 | 无 | 回复中说明修改与验证 |
| L1 | `.dj-agent/summary-lite-template.md` | 轻量总结 |
| L2 | `.dj-agent/task-lite-template.md` | 合并 Research/Plan/Summary |
| L3/L4 | `001/002/003-*template.md` | 完整调研、计划、总结 |

## 5. 验证策略

文档仓库默认验证：
- `git diff --check` 检查空白错误。
- `find . -maxdepth 4 -type f | sort` 检查新增入口文件是否存在。
- 人工阅读关键规则之间的一致性。

代码仓库使用 `.dj-agent/guide/60-validation.md` 中的语言/框架命令矩阵。

## 6. 维护原则

- 新规则优先写入对应分片，不把细节堆到 `AGENTS.md`。
- L1/L2 优先轻流程，避免小任务被完整模板拖慢。
- 只有长期产品行为或架构/接口/数据/部署变化才更新总文档。
- 分片超过 500 行时继续拆分，并在顶部维护导航链接。
