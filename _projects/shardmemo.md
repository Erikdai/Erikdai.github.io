---
layout: page
title: ShardMemo
description: Official code for our EMNLP 2026 Findings paper — a three-tier memory service for LLM agents where metadata predicates first decide which memory shards a request may access, then a learned masked router probes only a few of them, so out-of-scope shards never spend probe budget (LoCoMo, HotpotQA, ToolBench).
description_zh: EMNLP 2026 Findings 论文的官方代码——面向大模型智能体的三层记忆服务：先由元数据谓词确定请求可以访问哪些记忆分片，再由学习到的掩码路由器只探测其中少数几个，不可访问的分片不占用探测预算（LoCoMo、HotpotQA、ToolBench）。
img: assets/img/proj_shardmemo.png # cover drawn in the repo's logo palette (1280x640, 2:1)
importance: 2
category: work
github: https://github.com/Erikdai/shardmemo
report: https://arxiv.org/abs/2601.21545
report_label: Paper (arXiv)
redirect: https://github.com/Erikdai/shardmemo
---
