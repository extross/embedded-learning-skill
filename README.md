# Embedded Learning Skills for AI Agents

> **拒绝黑盒许愿机，面向深度学习与工程实践的嵌入式系统 AI 架构导师技能包。**
> 
> *A collection of pedagogical, first-principles skills for Codex, Claude Code, Antigravity, and other AI coding agents—designed for engineers who want to master embedded systems rather than treat AI as a code dispenser.*

---

## 🎯 设计初衷 (Design Philosophy)

在嵌入式开发、机器人竞赛（如 RoboCup、RM）和实时操作系统（FreeRTOS/RT-Thread）工程中，**将 AI 当成黑盒“许愿机”是非常危险的**：
- 硬件跑飞、DMA 缓存不一致、中断优先级反转、竞态数据撕裂等深层硬件隐患，纯靠黑盒生成的代码完全无法定位“案发现场”。
- 工程师的核心竞争力不在于“写出能跑的代码”，而在于**洞悉底层原理、权衡硬件资源、以及科学严谨的系统级设计与排错能力**。

本仓库提供四个深度适配嵌入式软硬件协同开发的专有 Skill，约束 AI 智能体化身**资深嵌入式架构师与实战导师**，辅导开发者完成高质量工程进阶。

---

## 📦 技能概览 (Skills Included)

| Skill 目录 | 核心定位 | 解决痛点 | 典型触发词 / 前缀 |
| :--- | :--- | :--- | :--- |
| **[`socratic-mentor`](./socratic-mentor/SKILL.md)** | **苏格拉底式架构导师** | 严禁一上来堆砌大段完整代码；先理清物理约束、抽象分层，提问引导自主决策。 | `/mentor`、`怎么设计`、`先别写代码`、`给个思路` |
| **[`design-tradeoff-analyst`](./design-tradeoff-analyst/SKILL.md)** | **方案权衡与第一性原理推演** | 拒绝盲目选型；输出 RAM/ROM/时延/竞态多维对比矩阵与 Mermaid 状态机/时序图。 | `/tradeoff`、`方案对比`、`用A还是用B`、`优缺点` |
| **[`embedded-code-walkthrough`](./embedded-code-walkthrough/SKILL.md)** | **底层微架构与机制伴读** | 拒绝浮于表面的语法复述；透视芯片寄存器映射、总线时延、`volatile` 与汇编展开。 | `/walkthrough`、`为什么这么写`、`底层原理`、`逐行讲解` |
| **[`embedded-debug-coach`](./embedded-debug-coach/SKILL.md)** | **故障溯源与排错教练** | 遇到崩溃拒绝盲猜；教你读取 Cortex-M SCB 寄存器、反推压栈 PC 指针、单一变量实验定位根因。 | `/debug`、`HardFault`、`卡死`、`跑飞`、`调试思路` |

---

## 🚀 快速安装 (Installation)

### 1. Codex (OpenAI Coding Agent)
将本仓库中的技能文件夹克隆或复制到你的全局技能目录中：

**Windows:**
```powershell
git clone https://github.com/extross/embedded-learning-skill.git "$env:USERPROFILE\.agents\skills\embedded-learning-skill"
```
或者拷贝到 `.agents/skills` / `.codex/skills`：
```powershell
Copy-Item -Path "embedded-learning-skill\*" -Destination "$env:USERPROFILE\.agents\skills" -Recurse -Force
```

**Linux / macOS:**
```bash
git clone https://github.com/extross/embedded-learning-skill.git ~/.agents/skills/embedded-learning-skill
```

### 2. 项目级安装 (Project-Level)
如果你只想在特定的嵌入式工程中生效（如当前机器人竞赛工程），可直接放入工程根目录：
```text
your-project/
├── .agents/
│   └── skills/
│       ├── socratic-mentor/SKILL.md
│       ├── design-tradeoff-analyst/SKILL.md
│       ├── embedded-code-walkthrough/SKILL.md
│       └── embedded-debug-coach/SKILL.md
```

---

## 💡 使用范例 (Usage Examples)

### 示例 1：架构启发式提问 (`/mentor`)
> **User**: `/mentor 我打算在 FreeRTOS 中为双电机实现编码器速度解算与增量式 PID 控制，先别给完整代码，带我梳理一下时钟分频、采样周期与任务划分。`
> 
> **AI (Socratic Mentor)**:
> 1. 先帮你建立硬件分层模型（定时器编码器模式 -> 周期性采样任务 -> 算法解算）；
> 2. 抛出关键问题：“如果在定时器溢出中断更新多圈计数，电机高转速反转时如何避免临界区读取毛刺？”
> 3. 给出接口头文件原型，引导你自主完成驱动与算法实现。

### 示例 2：方案权衡对比 (`/tradeoff`)
> **User**: `/tradeoff STM32 接收高频激光雷达点云，用 DMA 循环模式+空闲中断，还是 DMA 双缓冲机制？帮我做个对比并画时序图。`
> 
> **AI (Tradeoff Analyst)**:
> 1. 输出包含 RAM 占用、中断延迟、总线竞态的对比矩阵；
> 2. 生成 Mermaid 时序图，直观展示数据所有权如何在硬件与任务间流转。

### 示例 3：底层寄存器与时序伴读 (`/walkthrough`)
> **User**: `/walkthrough 为什么在 STM32 的中断服务函数中清除标志位后，通常要紧跟一次寄存器读取或者 __DSB() 屏障？`
> 
> **AI (Code Walkthrough)**:
> - 从 ARM Cortex-M 写入缓冲（Write Buffer）和 APB 总线桥的传播时延讲起，解析为什么不追加读取会导致从 ISR 退出时标志位尚未清零而引发虚假二次中断。

### 示例 4：系统化排错教学 (`/debug`)
> **User**: `/debug 烧录运行后系统直接跳入 HardFault_Handler，指导我读取寄存器排查原因。`
> 
> **AI (Debug Coach)**:
> 1. 指导查看 `EXC_RETURN` 判断当前使用的是 MSP 还是 PSP；
> 2. 定位堆栈中保存的 `PC` 地址，并在反汇编（Disassembly）中找到罪魁祸首的汇编指令（如野指针解引用）；
> 3. 解读 `SCB->CFSR` 状态寄存器，定位总线错误或未对齐访问标志。

---

## 📄 License

MIT License. 欢迎参赛队员、嵌入式开发者 Fork 与补充优化！
