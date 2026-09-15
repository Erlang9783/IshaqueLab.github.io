---
layout: default
title: Publications
---
# Publications

## Selected {#selected}

<ul class="pubs selected">
{% for p in site.data.selected_publications %}
  <li>
    <span class="pub-title">{% if p.doi contains "verify" %}{{ p.title }}{% else %}<a href="https://doi.org/{{ p.doi }}">{{ p.title }}</a>{% endif %}</span>
    <span class="pub-meta">{{ p.citation }}</span>
    <span class="pub-why">{{ p.why }}</span>
  </li>
{% endfor %}
</ul>

## All publications

Listed from <a href="https://openalex.org">OpenAlex</a> using ORCID <a href="https://orcid.org/{{ site.orcid }}">{{ site.orcid }}</a>, newest first. For citation counts see <a href="{{ site.scholar }}">Google Scholar</a>.

<div data-pubs data-controls="true" data-orcid="{{ site.orcid }}" data-limit="200" data-mailto="{{ site.openalex_mailto }}" data-scholar="{{ site.scholar }}">
  <p class="pubs-status">Loading publications…</p>
</div>

<script src="{{ '/assets/js/publications.js' | relative_url }}" defer></script>
