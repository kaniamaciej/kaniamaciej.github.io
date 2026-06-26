---
layout: page
title: Scientific output
permalink: /output/
weight: 3
---

{% assign d = site.data.scientific-output %}

# **Scientific Output**

{% if d.papers and d.papers.size > 0 %}
## Peer-reviewed papers
{% for item in d.papers %}
**{{ item.title }}**<br>
<span class="text-muted">{{ item.authors }}{% if item.venue %} · {{ item.venue }}{% endif %}{% if item.year %} · {{ item.year }}{% endif %}</span>{% if item.link %} · [{{ item.link_text | default: "link" }}]({{ item.link }}){% endif %}{% if item.note %}<br>{{ item.note }}{% endif %}

{% endfor %}
{% endif %}

{% if d.preprints and d.preprints.size > 0 %}
## Preprints & under review
{% for item in d.preprints %}
**{{ item.title }}**<br>
<span class="text-muted">{{ item.authors }}{% if item.venue %} · {{ item.venue }}{% endif %}{% if item.year %} · {{ item.year }}{% endif %}</span>{% if item.link %} · [{{ item.link_text | default: "link" }}]({{ item.link }}){% endif %}{% if item.note %}<br>{{ item.note }}{% endif %}

{% endfor %}
{% endif %}

{% if d.studentjournal and d.studentjournal.size > 0 %}
## Student journals
{% for item in d.studentjournal %}
**{{ item.title }}**<br>
<span class="text-muted">{{ item.authors }}{% if item.venue %} · {{ item.venue }}{% endif %}{% if item.year %} · {{ item.year }}{% endif %}</span>{% if item.link %} · [{{ item.link_text | default: "link" }}]({{ item.link }}){% endif %}{% if item.note %}<br>{{ item.note }}{% endif %}

{% endfor %}
{% endif %}

{% if d.oral_presentations and d.oral_presentations.size > 0 %}
## Oral presentations
{% for item in d.oral_presentations %}
**{{ item.title }}**<br>
<span class="text-muted">{{ item.authors }}{% if item.venue %} · {{ item.venue }}{% endif %}{% if item.year %} · {{ item.year }}{% endif %}</span>{% if item.note %}<br>{{ item.note }}{% endif %}

{% endfor %}
{% endif %}

{% if d.posters and d.posters.size > 0 %}
## Posters
{% for item in d.posters %}
**{{ item.title }}**<br>
<span class="text-muted">{{ item.authors }}{% if item.venue %} · {{ item.venue }}{% endif %}{% if item.year %} · {{ item.year }}{% endif %}</span>{% if item.note %}<br>{{ item.note }}{% endif %}

{% endfor %}
{% endif %}

{% if d.workshops and d.workshops.size > 0 %}
## Workshops
{% for item in d.workshops %}
**{{ item.title }}**<br>
<span class="text-muted">{% if item.venue %}{{ item.venue }}{% endif %}{% if item.year %} · {{ item.year }}{% endif %}</span>{% if item.note %}<br>{{ item.note }}{% endif %}

{% endfor %}
{% endif %}
