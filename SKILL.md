---
name: embedded-c-doxygen-comments
description: Add accurate Chinese Doxygen-style comments for embedded C firmware code. Use when creating, modifying, or reviewing C source/header files that need function comments, MCU driver notes, alarm/reporting state-machine explanations, FIFO logic documentation, interrupt handling notes, or Chinese embedded-development code comments.
---

# Embedded C Doxygen Comments

## Overview

Use this skill to document embedded C code with concise, accurate Chinese Doxygen comments. Apply it whenever adding or changing meaningful firmware logic, even if the user does not explicitly ask for comments.

## Comment Scope

Comment only code that benefits from explanation:

- Add Doxygen blocks for major functions, state-machine handlers, interrupt handlers, reporting/packing functions, FIFO operations, low-power transitions, debounce logic, and hardware abstraction entry points.
- Add short end-of-line comments only for single important statements whose intent is not obvious.
- Do not mechanically comment every function, every branch, or every assignment.
- Do not add misleading comments to code whose behavior has not been checked.

## Function Comment Format

For each major C function, use this exact Doxygen block style:

```c
/**
 * @brief 用一句话简洁说明函数功能。
 *
 * 1. 清晰描述第一步执行流程。
 * 2. 清晰描述第二步执行流程。
 * 3. 清晰描述第三步执行流程。
 *
 * 设计意图：说明该函数的抽象目的、可靠性目的或嵌入式设计取舍。
 *
 * @param param_name 参数用途说明。
 * @return 返回值含义说明。
 */
```

Rules:

- Write all comments in Chinese.
- Keep `@brief` to one concise sentence.
- Use numbered steps `1. 2. 3.` to describe the actual execution flow.
- Include a design-intent paragraph beginning with `设计意图：`.
- Include one `@param` line per parameter.
- Use `@param 无` when the function has no parameters.
- Include `@return` for every function.
- Use `@return 无` for `void` functions.
- Keep wording in an embedded-firmware style: concrete, operational, and tied to hardware, timing, state machines, queues, interrupts, or reporting behavior.
- Ensure the comment matches the implementation exactly before writing it.

## End-Of-Line Comments

Use short Chinese end-of-line comments only for important single statements:

```c
di_alarm.step = DI_ALARM_STEP_WAIT_INT; // 连续稳定后重新允许低功耗中断唤醒。
```

Rules:

- Comment the intent, not the syntax.
- Do not explain obvious assignments such as `i++`.
- Avoid long end-of-line comments that wrap awkwardly.
- If a comment is long, put it on the previous line instead.

## Workflow

When editing embedded C code:

1. Read the surrounding code first and identify the real behavior.
2. Decide which functions are major enough to need Doxygen blocks.
3. Write comments after understanding the state transitions, timing, hardware polarity, error paths, and data ownership.
4. Add concise end-of-line comments only to important non-obvious statements.
5. Compile or at least run a syntax check when possible, especially after adding Chinese comments in legacy-encoded files.

## Quality Bar

Before finishing, verify:

- The comment does not claim behavior that the code does not implement.
- The numbered steps match the order and conditions in the function.
- The design intent explains why the function exists, not just what it does.
- Parameter names exactly match the function signature.
- Return descriptions cover all meaningful return values.
- The comments do not create encoding or line-continuation problems in the C compiler.
