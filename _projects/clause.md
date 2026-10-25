---
layout: page
title: CLAUSE
description: Official code for our ICLR 2026 paper. CLAUSE builds the context for multi-hop questions over a knowledge graph with three agents. One edits the question subgraph, one follows or backtracks reasoning paths and one picks the evidence for the reader LLM. They are trained jointly with LC-MAPPO under budgets on edge edits, steps and tokens (HotpotQA, Wikidata5M).
description_zh: ICLR 2026 论文的官方代码。CLAUSE 用三个智能体在知识图谱上为多跳问答构建上下文，分别负责编辑问题子图、沿推理路径前进或回溯，以及为阅读器大模型挑选证据。三者在边编辑数、交互步数和 token 预算的约束下用 LC-MAPPO 联合训练（HotpotQA、Wikidata5M）。
img: assets/img/proj_clause.png # cover drawn in the repo's logo palette, same layout as the ShardMemo card (1280x640, 2:1)
importance: 3
category: work
github: https://github.com/Erikdai/CLAUSE-reproduction
report: https://arxiv.org/abs/2509.21035
report_label: Paper (arXiv)
redirect: https://github.com/Erikdai/CLAUSE-reproduction
---
