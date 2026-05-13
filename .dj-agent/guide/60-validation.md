# 60-validation.md

> 导航：上一节 `50-review-checklist.md` ｜ 返回 `00-routing.md`
>
> 验证命令约定：把“验证通过”变成可执行标准。

## 1. 默认策略

- 优先使用项目已有脚本：`Makefile`、`package.json`、`go.mod`、`pyproject.toml`、`Cargo.toml`、`pom.xml` 等。
- 优先级：单元测试 > lint/typecheck > build > 可复现实测步骤。
- 改动越小，验证越窄；影响公共接口、架构或数据时，验证必须扩大。
- 验证命令失败时，先判断是否由本次修改导致；非本次问题要明确记录。

## 2. 常见项目命令

| 项目类型 | 优先验证命令 |
|---------|-------------|
| Go | `go test ./...` |
| Node.js | `npm test`、`npm run lint`、`npm run build`、`npm run typecheck` |
| Python | `pytest`、`ruff check .`、`mypy .` |
| Rust | `cargo test`、`cargo clippy`、`cargo build` |
| Java/Maven | `mvn test` |
| Java/Gradle | `./gradlew test` |
| 文档仓库 | 链接检查、`git diff --check`、人工阅读一致性检查 |

## 3. 分级验证要求

| 级别 | 最小验证 |
|------|---------|
| L0 | 代码阅读或单个针对性命令 |
| L1 | 复现/验证目标问题，必要时跑相关测试 |
| L2 | 执行计划中的验证项，至少跑相关自动化或说明无自动化原因 |
| L3 | 相关模块完整测试 + 构建/类型/静态检查 |
| L4 | 全量验证 + 部署/回滚/监控检查 |

## 4. 无自动化验证时

记录以下内容：
- 验证环境：本地/容器/测试环境。
- 操作步骤：可由他人复现。
- 预期结果：明确成功标准。
- 实际结果：说明是否通过。
- 风险：无法覆盖的场景。
