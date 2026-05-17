---
title: 最佳实践-为什么不应该使用Openclaw/Hermes进行开发
date: 2026-05-17 13:12:34
tags:
---
做开发时（尤其是结合 Hermes Agent 和 OpenClaw 这类自主代理/自动化工具）觉得 Token 像流水一样烧得飞快，这其实是 Auto-Agent（自主智能体）架构的底层逻辑决定的。这并不是你的错觉，也不是代码写写错了，而是这类工具在开发和运行阶段有几个天然的“Token 碎纸机”机制。

以下是核心原因的深度剖析：
1. 恐怖的“上下文滚雪球”效应 (Context Accumulation)Auto-Agent 核心的运作方式是：思考 $\rightarrow$ 行动 $\rightarrow$ 观察 $\rightarrow$ 再思考 的循环（ReAct 框架）。
第 1 轮： Prompt + 任务目标 $\rightarrow$ 消耗 2k Token。
第 2 轮： Prompt + 任务目标 + 第 1 轮的思考和执行结果（比如读文件、查数据库） $\rightarrow$ 消耗 4k Token。
第 3 轮： Prompt + 任务目标 + 前两轮的所有历史和报错信息 $\rightarrow$ 消耗 8k Token。每一次它尝试修复一个 Bug 或者多走一步，都会把前面所有的对话历史、代码上下文、控制台报错原封不动地叠加塞回给大模型。这种指数级或线性的上下文堆叠，是烧 Token 的头号杀手。

2. System Prompt（系统提示词）过于臃肿像 OpenClaw 和 Hermes 这种为了保证高成功率、能进行复杂工具调用（Function Calling）的 Agent，其背后的 System Prompt 极其庞大。里面包含了：严密的逻辑框架、角色设定、各种异常处理守则、输出格式规范（比如强制要求 JSON 且不能出错）。外加它能调用的每一个工具（API、读写文件、执行 Shell 命令行）的定义说明。结果： 哪怕你只是让它改一行代码，只要它和模型交互一次，哪怕模型只回答一个词，这几千甚至上万 Token 的 System Prompt 都要作为输入重新计费一次（如果没有开启 Context Caching 的话）。

3. “反思”与“自我纠错”机制的代价Hermes 等 Agent 之所以显得聪明，是因为它有一套“自我反思（Self-Reflection）”和“纠错”机制：代码写完了？它会自己调编译器运行一下。报错了？它会把报错信息吞进去，自己跟自己讨论：“哦，看来这里类型不对，我得换个方法”。在这个感知-纠错的闭环里，用户可能只看到了最终改好的那一行代码，但期间它可能已经和背后的 Claude 或 GPT 悄悄对视了 5-10 个回合，每一回合都是全量上下文的输入。4. 代码文件全量读取 (Full File Injection)在做开发任务时，Agent 为了理解依赖关系，往往需要读取你整个文件甚至多个关联文件的内容。如果你没有做精细的路径裁剪，Agent 可能会把整段文件的代码都塞进 Prompt 里。一旦它决定“我要重写这个函数”，它在 Output（输出端）又会把整段代码重新吐出来。要知道，Output Token 的价格通常是 Input Token 的 3 倍左右，反复吐出大段代码会瞬间让账单飙升。