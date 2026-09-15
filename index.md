---
layout: default
title: null
---
<div class="hero">
  <div>
    <h1>Cancer is an ecosystem. We map it.</h1>
    <p class="lead">Bioinformatics for cancer research at the intersection of spatial biology, single-cell genomics and cancer genomics. We are the group of Naveed Ishaque, Professor of Cancer Bioinformatics at Charité - Universitätsmedizin Berlin and the BIH Center of Digital Health.</p>
    <p>The spatial arrangement of tumour, immune and stromal cells carries information that conventional approaches cannot capture. We work to understand the causal mechanisms that shape cell and tissue structure in development and disease. Our focus is oncology, with active interests in immunology, neurodegeneration and metabolic disease. We build open-source software for the wider field of spatial analysis, including tools that find data-quality problems in spatial transcriptomics.</p>
    <div class="actions">
      <a class="button" href="{{ '/research/' | relative_url }}">Research</a>
      <a class="button secondary" href="{{ '/software/' | relative_url }}">Software</a>
      <a class="button secondary" href="{{ '/join/' | relative_url }}">Join the lab</a>
    </div>
  </div>
  <aside class="hero-side">
    <p><strong>Part of</strong></p>
    <ul>
      {% for c in site.data.consortia %}
      <li><a href="{{ '/research/' | relative_url }}#{{ c.id }}">{{ c.name }}</a></li>
      {% endfor %}
    </ul>
  </aside>
</div>

<h2>What we work on</h2>
<ul class="areas">
{% for t in site.data.projects %}
  <li><h3><a href="{{ '/research/' | relative_url }}#{{ t.id }}">{{ t.name }}</a></h3><p>{{ t.short }}</p></li>
{% endfor %}
</ul>

<h2>Recent publications</h2>
<div data-pubs data-orcid="{{ site.orcid }}" data-limit="5" data-mailto="{{ site.openalex_mailto }}" data-scholar="{{ site.scholar }}">
  <p class="pubs-status">Loading publications…</p>
</div>
<p><a href="{{ '/publications/' | relative_url }}">All publications</a> or <a href="{{ site.scholar }}">view on Google Scholar</a>.</p>

<script src="{{ '/assets/js/publications.js' | relative_url }}" defer></script>
