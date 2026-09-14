---
layout: default
title: Research
description: Research themes and consortium projects of the Ishaque Lab, Charité and BIH.
---
# Research

Our focus is bioinformatics in cancer research, at the intersection of spatial biology, single-cell genomics and cancer genomics. Cancer is not merely an intrinsic genetic disease of the cell but an ecosystem at the tissue level. The spatial arrangement of tumour, immune and stromal cells relative to one another carries information that conventional approaches cannot capture. We therefore try to understand the causal mechanisms that determine cell and tissue structure in the tumour microenvironment, with the goal of identifying robust routes to new therapies. While most of our work is in oncology, we have active interests in immunology, neurodegeneration and metabolic disease. Alongside this we develop software for the wider field of spatial analysis, including tools that identify data-quality problems in spatial transcriptomics.

<nav class="toc" aria-label="On this page">
  <span>On this page:</span>
  {% for t in site.data.projects %}<a href="#{{ t.id }}">{{ t.name }}</a>{% endfor %}
  <a href="#projects">Consortia and projects</a>
</nav>

## Themes

{% for t in site.data.projects %}
<section class="theme" id="{{ t.id }}">
  <h3>{{ t.name }}</h3>
  <p>{{ t.summary }}</p>
</section>
{% endfor %}

## Consortia and major projects {#projects}

{% for c in site.data.consortia %}
<section class="consortium" id="{{ c.id }}">
  <div class="consortium-head">
    {% if c.logo %}<a href="{{ c.url }}"><img src="{{ c.logo | relative_url }}" alt="" loading="lazy"></a>{% endif %}
    <h3><a href="{{ c.url }}">{{ c.name }}</a></h3>
  </div>
  <p>{{ c.about }}</p>
  <h4>Our role</h4>
  <p>{{ c.role }}</p>
  {% if c.roles_line %}<p class="roles">{{ c.roles_line }}</p>{% endif %}
  {% if c.related.size > 0 %}
  <p class="related">Related:
    {% for r in c.related %}<a href="{{ r.url | relative_url }}">{{ r.text }}</a>{% unless forloop.last %}, {% endunless %}{% endfor %}
  </p>
  {% endif %}
</section>
{% endfor %}

