# 30-code.md

> 导航：上一节 `20-plan.md` ｜ 下一节 `40-summary.md`
>
> 编码阶段执行约束：先思考、简洁优先、精准修改、目标驱动。必须同时遵守 `05-safety-gates.md`。

## 1. 编码前先思考

- 不要假设。不要隐藏困惑。揭示权衡。
- 明确陈述假设；先快速探查，仍不确定或涉及取舍/风险时再提问。
- 如果存在多种解释，全部列出，不要默默选择。
- 如果有更简单方法，主动提出；必要时提出反对意见。
- 快速探查后仍不清楚时，暂停并先澄清再实现。
- 编码前必须确认工作区状态，避免覆盖用户已有修改。
- 修改前必须明确本轮目标、文件范围、预期影响和验证方式。
- 需要执行 C2/C3 命令时，必须先获得用户明确确认。

## 2. 简洁优先

- 用最少代码解决问题，不做推测性实现。
- 不添加未被请求的功能、配置、灵活性。
- 不为低概率场景写过度错误处理。
- 能用更少代码清晰解决就不引入额外结构；可读性优先于机械压缩行数。

## 3. 精准修改

- 只触碰必须修改的地方。
- 不顺手重构无问题模块，不改无关注释和格式。
- 匹配现有代码风格。
- 若发现无关死代码，仅提及，不擅自删除。
- 不执行 `05-safety-gates.md` 中列出的破坏性操作，除非用户明确授权。
- 不用批量重写、批量格式化或自动生成内容掩盖小范围逻辑变更。

当本次修改产生孤儿代码时：
- 清理本次变更导致不再使用的导入/变量/函数。
- 不清理历史遗留死代码（除非明确要求）。

检验标准：每一行变更都可追溯到当前需求。

## 4. 生成代码格式硬约束

生成或修改代码时，必须遵守以下命名与排版规则；与项目既有风格冲突时，先指出冲突并按本节规则执行，除非用户明确要求沿用项目旧风格。

- 本节命名和排版硬约束默认强制用于 C/C++。
- Rust、Go、Python 代码优先遵守语言官方格式工具和社区命名习惯；不要把 C/C++ 的函数名、文件名、变量名前缀规则强行套用到这些语言。
- 不要为了满足格式规则重命名公共 API、ABI、序列化字段、配置字段、数据库字段、协议字段、第三方接口或框架约定入口；遇到冲突时先说明冲突。
- C/C++ 默认使用 4 空格缩进，不使用 tab；单行建议不超过 120 列，项目已有更严格限制时按项目限制执行。
- C/C++ 局部变量和函数签名中的形参变量统一使用首字母小写的驼峰命名，例如 `itemCount`、`configPath`。
- C 语言自定义结构体类型必须先使用 `typedef struct _StructType StructType;` 声明，再在后续使用 `struct _StructType { ... };` 定义；`StructType` 必须使用首字母大写的驼峰命名。
- C++ 类名必须使用首字母大写的驼峰命名，例如 `TaskRunner`。
- C/C++ 全局变量必须使用驼峰命名，并以 `g` 开头，例如 `gInstance`。
- C/C++ 静态变量必须使用驼峰命名，并以 `gs` 开头，例如 `gsInstance`；C++ 静态成员变量也使用 `gs` 前缀。
- C/C++ 函数名必须使用下划线分割单词，例如 `load_config`、`create_task_runner`。
- C++ 类成员方法必须使用首字母小写的驼峰命名，例如 `setX()`、`getY()`。
- C++ 类非静态成员变量必须使用首字母小写的驼峰命名，并以 `m` 开头，例如 `mParam`、`mTaskCount`。
- C/C++ 宏名和枚举值必须使用全大写下划线命名，例如 `MAX_TASK_COUNT`、`TASK_STATE_RUNNING`。
- C/C++ 常量必须使用 `k` 前缀加首字母大写的驼峰命名，例如 `kMaxTaskCount`。
- C/C++ 枚举类型名必须使用首字母大写的驼峰命名，例如 `TaskState`。
- C/C++ 指针和引用声明统一写成 `Type *name`、`Type &name`；不要在同一行声明多个变量。
- C/C++ 新建文件名必须使用中划线分割单词，例如 `task-runner.cpp`、`config-loader.h`。
- Rust 文件名、模块名、函数名和变量名使用 `snake_case`，类型和 trait 使用 `UpperCamelCase`，常量使用 `UPPER_SNAKE_CASE`，格式化交给 `rustfmt`。
- Go 文件名使用小写或 `snake_case`，包名小写，导出标识符使用 `UpperCamelCase`，非导出标识符使用 `lowerCamelCase`，格式化交给 `gofmt`。
- Python 文件名、函数名和变量名使用 `snake_case`，类名使用 `UpperCamelCase`，常量使用 `UPPER_SNAKE_CASE`，格式遵循 Black/Ruff 风格。
- 新建 C/C++ 头文件禁止使用 `#pragma once`，必须使用 include guard；宏名格式为 `PROJECT_MODULE_FILE_H_`，其中项目名、模块名、文件名转为全大写下划线，文件名中的中划线改为下划线；宏名过长时可以去掉项目名或模块名，但必须确保不冲突。
- C/C++ 头文件禁止写 `using namespace ...`。
- C/C++ include 顺序固定为：本文件对应头文件、项目内头文件、第三方头文件、系统头文件。
- C/C++ 函数定义时，返回值和函数名必须放在同一行；函数体左花括号另起一行。
- 条件、循环等代码块必须显式使用花括号；块左花括号放在块起始语句的行尾。
- C/C++ 创建/销毁成对函数使用 `xxx_create` / `xxx_destroy` 命名；初始化/释放成对函数使用 `xxx_init` / `xxx_deinit` 命名。

示例：

```c
#ifndef WORKFLOW_TASK_CONFIG_H_
#define WORKFLOW_TASK_CONFIG_H_

typedef struct _TaskConfig TaskConfig;

enum TaskState 
{
    TASK_STATE_IDLE,
    TASK_STATE_RUNNING
};

struct _TaskConfig
{
    int itemCount;
};

static const int kMaxTaskCount = 16;

int load_config(const char *configPath)
{
    if (configPath != NULL) {
        return 0;
    }

    return -1;
}

#endif
```

```cpp
class TaskRunner
{
public:
    void setTaskCount(int taskCount);

private:
    static TaskRunner *gsInstance;
    int mTaskCount;
};
```

## 5. 目标驱动执行

- 将任务转成可验证目标，循环直到通过。
- 示例：
  - 添加验证 -> 先写失败用例，再让其通过。
  - 修复 bug -> 先复现 bug，再修复并通过验证。
  - 重构 -> 确保重构前后行为一致并验证通过。

## 6. Bug 修复强制流程

- 先记录现象：输入、环境、实际结果、预期结果。
- 优先复现 bug；不能复现时，必须说明已有证据和无法复现原因。
- 修复前必须标注 bug 证据等级：E0 / E1 / E2 / E3。
- 修复前必须定位根因，至少说明错误路径、触发条件和影响范围。
- E0 不得进入 Code 阶段修改核心逻辑；E1 修改必须保持最小范围，核心修复仅限低风险、可逆、防御性改动，并记录假设和残余风险。
- 修改必须是最小补丁，避免顺手重构。
- E2/E3 必须增加或执行回归验证，证明原问题已被覆盖；E1 必须执行与修复假设相关的验证，并记录证据链和残余风险。
- 如果根因超出当前需求范围，必须回退到 Routing/Plan 并重新分级。

## 7. 系统/底层代码约束

涉及 C/C++、Rust `unsafe`、内核/驱动、并发、内存生命周期、ABI/API/协议或构建链接时：

- 内核版本条件编译必须按“由低到高”书写：
  - 首选 `#if LINUX_VERSION_CODE <= KERNEL_VERSION(x, y, z)` 分支放旧版本实现；
  - `#else` 放新版本实现；
  - 禁止使用“高到低”写法（例如 `#if LINUX_VERSION_CODE >= ...` 再 `#else` 旧版本）。
- 必须检查错误路径、资源释放、所有权转移和生命周期。
- 必须检查缓冲区边界、整数溢出、空指针、UAF、泄漏和未初始化数据。
- 必须检查锁顺序、竞态、死锁、原子语义和回调重入。
- 必须检查 ABI/API/协议/配置兼容性；兼容性改变必须在 Plan 中显式记录。
- 必须给出可落地验证；无法运行高强度验证时，必须说明残余风险。

## 8. 验证约束

- Code 阶段必须加载 `.dj-agent/guide/60-validation.md`。
- 优先运行项目已有的测试、lint、build、typecheck 命令。
- 如果没有自动化验证，必须记录可复现实测步骤。
- 如果验证因环境缺失无法执行，说明阻塞原因和已完成的替代检查。

## 9. 完成标志

- 有本地持久任务文档时，执行计划状态、验证结果和 Summary/轻量总结已按实际结果更新；无持久文档时，最终回复说明结果与验证。
- 文档进度更新完成后，若用户明确要求提交或 `AGENTS.project.md` 明确声明本项目默认自动提交，再按 `.dj-agent/commit-message-template.md` 提交本次相关变更；提交范围和门禁要求遵守 `05-safety-gates.md`。
- 代码实现符合当前目标；有 Plan 时符合 Plan。
- 验证通过（自动化测试或可复现实测步骤）。
- 无本次引入的明显复杂度与风格偏差。
- 当前级别和阶段要求多角色审视时，审视已通过；L3/L4 Code 阶段必须执行。
