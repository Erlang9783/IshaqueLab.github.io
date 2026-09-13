---
layout: default
title: Research
---
# Research and software

We develop computational methods to understand biological heterogeneity in disease, using single-cell, spatial and multi-omics data. Most of our work is in oncology. We rely on close ties with experimental collaborators who profile large, high-dimensional datasets with state-of-the-art techniques, and we release our methods as open-source software.

## Research areas

<ul class="areas">
{% for p in site.data.projects %}
  <li><h3>{{ p.name }}</h3><p>{{ p.summary }}</p></li>
{% endfor %}
</ul>

## Community

We are actively involved in [ELIXIR](https://elixir-europe.org/), [ELIXIR-Germany](https://elixir-europe.org/about-us/who-we-are/nodes/germany)/[de.NBI](https://www.denbi.de/) and coordinate the [SpaceHack](https://spatialhackathon.github.io/) hackathon serie.
