---
layout: post
title: 标题写这里
date: 2026-08-01 10:00:00 +1000 # 发布时间，+1000 是悉尼时区
description: 一句话摘要，会显示在 /blog/ 列表里
tags: llm agents # 空格分隔；点进去是 /blog/tag/llm/
categories: paper-notes # 空格分隔；点进去是 /blog/category/paper-notes/
related_posts: false # 文末不显示「相关文章」
# featured: true      # 取消注释可置顶到 /blog/ 顶部的卡片区
# thumbnail: assets/img/xxx.png   # 列表右侧的小图
# giscus_comments: true           # 需要先在 _config.yml 里配好 giscus
---

正文从这里开始，直接写 Markdown。下面是这个主题常用的几种写法，用完可以删掉。

## 数学

行内公式 $$E = mc^2$$，独立成段就是展示公式：

$$
\sum_{k=1}^\infty |\langle x, e_k \rangle|^2 \leq \|x\|^2
$$

## 代码

```python
def hello(name: str) -> str:
    return f"hello, {name}"
```

## 图片

图片放在 `assets/img/` 下，然后：

{% raw %}

```liquid
{% include figure.liquid loading="eager" path="assets/img/xxx.png" class="img-fluid rounded z-depth-1" %}
```

{% endraw %}

## 引用文献

引 `_bibliography/papers.bib` 里的条目：{% raw %}`{% cite zhao2026clause %}`{% endraw %}，文末加 {% raw %}`{% bibliography --cited %}`{% endraw %} 生成参考文献列表。

## 侧边目录

在 front matter 里加 `toc: sidebar: left` 就会在左侧生成目录（正文用 `##` 分节即可）。
