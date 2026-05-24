---
title: 通过CC-Switch配置Claude Code使用GPT模型
date: 2026-05-24 23:49:02
tags:
---
    在日常使用中，虽然Claude Code直接使用OPUS模型是解决问题的最佳选择，但无奈模型太贵，本文指引如何介绍CC-Switch的进阶用法，配置Claude Code使用GPT模型。

一、什么是 CC Switch
    CC Switch 是一款跨平台桌面应用，专为使用 AI 编程工具的开发者设计。它帮助你统一管理 Claude Code、Claude Desktop、Codex、Gemini CLI、OpenCode、OpenClaw 和 Hermes 等受管应用的配置。

二、官方网站及下载地址：
    https://ccswitch.io/zh/ 下载并安装。



三、导入本站Claude分组配置
   
1、请登录网站后，在API密钥页面，在“Claude Max号池组” 对应行，点击导入到CCS
   ![n3PEcZ9WwwPI106h2527dZLiLmQ5Hemn.webp](https://cdn.nodeimage.com/i/n3PEcZ9WwwPI106h2527dZLiLmQ5Hemn.webp)

2、先按默认设置导入
![DN3143CEmu5mzOqTDyLjFy6Odi4d7VSt.webp](https://cdn.nodeimage.com/i/DN3143CEmu5mzOqTDyLjFy6Odi4d7VSt.webp)

3、CCS软件中选择刚导入的配置并进行编辑
![kyjtpXMaP2VGVpirjdOI3dLHy9GQbdn2.webp](https://cdn.nodeimage.com/i/kyjtpXMaP2VGVpirjdOI3dLHy9GQbdn2.webp)

4、**非常重要！复制本站的codex Pro号池组的key，替换Claude号池的key
![D9Ko5AzlAuhOfT1GblScRdeNjMagUh1p.webp](https://cdn.nodeimage.com/i/D9Ko5AzlAuhOfT1GblScRdeNjMagUh1p.webp)

5、点击获取模型列表，根据你的需求，选择gpt5.5或者5.4后保存！
![D9Ko5AzlAuhOfT1GblScRdeNjMagUh1p.webp](https://cdn.nodeimage.com/i/D9Ko5AzlAuhOfT1GblScRdeNjMagUh1p.webp)

6、重新打开vscode 即可在claude code 插件中使用gpt模型！

7、后台验证模型调用,确认！
![OIbTrhPG5TtZwefoMWX7g9znW3XYgmZ5.webp](https://cdn.nodeimage.com/i/OIbTrhPG5TtZwefoMWX7g9znW3XYgmZ5.webp)