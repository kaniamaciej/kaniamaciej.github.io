---
layout: page
title: About
permalink: /about/
weight: 1
---

# **About Me**

Hi, I'm **{{ site.author.name }}** :wave:

I'm a PhD student in theoretical and computational neuroscience at the **Institute of Science and Technology Austria (ISTA)**, in the **Vogels lab**. My research sits at the intersection of spiking neural network simulation, biologically constrained synaptic plasticity, reservoir computing, and simulation-based inference — I study what makes plasticity rules functionally effective under goal-directed behaviour.

I work with Auryn (C++), Brian2, and Python, run large-scale simulations on HPC clusters, and care about reproducible, publication-quality science. Outside the lab I'm active in neuroscience outreach across Austria.

<div class="row">
{% include about/timeline.html %}
</div>

# **Scholarships & Funding**

{% for item in site.data.funding %}
**{{ item.title }}**{% if item.year %} · <span class="text-muted">{{ item.year }}</span>{% endif %}<br>
<span class="text-muted">{{ item.org }}</span>{% if item.note %}<br>{{ item.note }}{% endif %}

{% endfor %}
