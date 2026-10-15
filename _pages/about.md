---
layout: about
title: about
title_zh: 关于
permalink: /
subtitle: '进退维谷之日，正是别有洞天之时。<br><span class="subtitle-en">When there seems to be no way forward or back, a whole new world may be just about to reveal itself.</span>'

# Intro splash shown before the homepage (see _includes/splash.liquid). Plays once per tab;
# add ?splash to the URL to force it. Set enabled: false to turn it off. The greetings float
# around the name; the page only opens when the visitor drags the slide-to-enter knob to the end.
splash:
  enabled: true
  subtitle: "AI Researcher · Agent Engineer · World Explorer"
  enter_label: "滑动进入 · Slide to enter"
  greetings:
    - 你好
    - Hello
    - こんにちは
    - 안녕하세요
    - Bonjour
    - Hola
    - Hallo
    - Ciao
    - Olá
    - Привет
    - مرحبا
    - नमस्ते
    - Xin chào
    - Sawubona

profile:
  align: right
  image: prof_pic_2026.jpg
  image_circular: false # crops the image to make it circular
  more_info: >
    <p>School of Computer Science</p>
    <p>University of Sydney</p>
    <p>NSW, Australia</p>
  more_info_zh: >
    <p>计算机学院</p>
    <p>悉尼大学</p>
    <p>澳大利亚 新南威尔士州</p>

selected_papers: false # all papers live on /publications/, grouped by year newest first (scholar.group_order in _config.yml)
social: true # includes social icons at the bottom of the page

announcements:
  enabled: false
  scrollable: true
  limit: 5

latest_posts:
  enabled: false
  scrollable: true
  limit: 3
---

<!-- Bilingual body: the language toggle in the navbar shows one of the two blocks (classes lang-en / lang-zh). -->
<div class="lang-en" markdown="1">

Hi! I am **Chengxiao Dai**, a Master of Computer Science student and tutor at the [University of Sydney](https://www.sydney.edu.au/). I have previously worked as a research intern at [A\*STAR's Singapore Institute of Manufacturing Technology](https://www.a-star.edu.sg/simtech) and the [China Academy of Information and Communications Technology (CAICT)](http://www.caict.ac.cn/english/), and as an algorithm engineer at [Imperial Vision](https://imperial-vision.com/en). I am also a co-founder of [ChuChiang Data](https://chuchiangdata.cc/), where we focus on building high-quality synthetic data solutions to address long-tail data challenges.

My research focuses on large language models and multi-agent systems, in particular LLM post-training, reinforcement learning for agentic systems, knowledge-graph reasoning, and domain-specific applications.

</div>
<div class="lang-zh" markdown="1">

你好！我是 **Chengxiao Dai**，[悉尼大学](https://www.sydney.edu.au/)计算机科学硕士在读，同时担任课程助教。此前曾在[新加坡科技研究局制造技术研究院（A\*STAR SIMTech）](https://www.a-star.edu.sg/simtech)和[中国信息通信研究院（CAICT）](http://www.caict.ac.cn/english/)担任研究实习生，并在 [Imperial Vision](https://imperial-vision.com/en) 担任算法工程师。我也是 [ChuChiang Data](https://chuchiangdata.cc/) 的联合创始人，我们专注于构建高质量的合成数据方案，以解决长尾数据难题。

我的研究方向是大语言模型与多智能体系统，重点关注 LLM 后训练、面向智能体系统的强化学习、知识图谱推理以及领域应用。

</div>

{% assign gs = site.data.scholar_stats %}
<p class="lang-en" style="font-size: 0.9rem; color: var(--global-text-color-light);" title="Google Scholar figures as of {{ gs.last_updated }}"><a href="https://scholar.google.com/citations?user={{ site.data.socials.scholar_userid }}" target="_blank">Google Scholar</a> · {{ gs.citations }} citations · h-index {{ gs.h_index }} · i10-index {{ gs.i10_index }}</p>
<p class="lang-zh" style="font-size: 0.9rem; color: var(--global-text-color-light);" title="Google Scholar 数据更新于 {{ gs.last_updated }}"><a href="https://scholar.google.com/citations?user={{ site.data.socials.scholar_userid }}" target="_blank">Google Scholar</a> · 引用 {{ gs.citations }} 次 · h 指数 {{ gs.h_index }} · i10 指数 {{ gs.i10_index }}</p>

<div class="lang-en" markdown="1">

I am currently seeking PhD opportunities and AI/ML engineering roles. Feel free to reach out at **chengxiao [dot] dai [at] sydney [dot] edu [dot] au**.

</div>
<div class="lang-zh" markdown="1">

我目前正在寻找博士（PhD）机会以及 AI/ML 工程师岗位，欢迎通过 **chengxiao [dot] dai [at] sydney [dot] edu [dot] au** 与我联系。

</div>
