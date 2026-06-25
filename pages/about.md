---
layout: page
title: About
permalink: /about/
weight: 1
---

# **About Me**

Hi, I'm **{{ site.author.name }}** :wave:

I'm a PhD student in theoretical and computational neuroscience at the **Institute of Science and Technology Austria (ISTA)**.

<div class="row">
{% include about/timeline.html %}
</div>

# **Scholarships & Funding**

# {% for item in site.data.funding %}
# **{{ item.title }}**{% if item.year %} · <span class="text-muted">{{ item.year }}</span>{% endif %}<br>
# <span class="text-muted">{{ item.org }}</span>{% if item.note %}<br>{{ item.note }}{% endif %}

{% endfor %}
