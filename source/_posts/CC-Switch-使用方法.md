---
title: CC-Switch 使用方法
date: 2026-05-11 23:08:37
tags:
---
CC-Switch 使用方法
CC-Switch 适合用来统一管理 Claude Code、Codex CLI、Gemini CLI、OpenCode、OpenClaw 等工具的 API Provider。添加一次智惠 API Provider 后，就可以在 CC-Switch 里一键切换到本站接口。

CC-Switch 配置项	填写内容
Provider Name	zhihui 或 Api2CN
API Type / Format	OpenAI Compatible
Base URL	https://api.api2cn.com/v1
API Key	放置你创建的api kye即可
Model	gpt-5.5 或 gpt-5.4
打开 CC-Switch，点击新增 Provider。
按上表填写 Provider 信息并保存。
在 CC-Switch 中选择刚创建的 Provider，并应用到需要使用的工具，例如 Claude Code、Codex CLI、OpenCode 或 OpenClaw。
回到对应终端工具，新开一个会话测试是否已经切换成功。
如果你的 CC-Switch 版本支持统一供应商（Universal Provider），建议优先创建统一供应商，这样 Claude Code、Codex CLI、Gemini CLI 等工具可以共用同一套智惠 API 配置。