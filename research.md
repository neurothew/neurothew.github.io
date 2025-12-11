---
layout: default
title: Research
---
# Research Highlights

<div class="research-grid">
  {% for post in site.categories.research %}
    <div class="research-card">
      <div>
        <h3 class="card-title">{{ post.title }}</h3>
        {% if post.image %}
          <img src="{{ post.image | relative_url }}" alt="{{ post.title }}" class="card-image">
        {% endif %}
        <p class="card-text">{{ post.excerpt }}</p>
      </div>
      <a href="{{ post.url | relative_url }}" class="read-more-btn">Read More</a>
    </div>
  {% endfor %}
</div>
