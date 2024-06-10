---
layout: archive
title: "Team"
permalink: /Team/
author_profile: true
---

{% include base_path %}

{% for post in site.team reversed %}
  {% include archive-single.html %}
{% endfor %}
