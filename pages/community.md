---
layout: page
title: Community
permalink: /community/
weight: 3
---

# **Community Activities**

Science outreach and service in the neuroscience community.

{% for item in site.data.community.activities %}
### {{ item.role }}
<span class="text-muted">{{ item.org }} · {{ item.from }}{% if item.to %} — {{ item.to }}{% endif %}</span>

{{ item.description }}

{% endfor %}
