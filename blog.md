---
layout: default
title: Blog
---

<h1>Blog</h1>

<div class="post-list">
  {% for post in site.posts %}
    <article class="post-item">
      <h2>
        <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
      </h2>
      <p class="post-meta">{{ post.date | date: "%B %d, %Y" }}</p>
      
      <div class="post-excerpt">
        {{ post.excerpt }}
      </div>
      
      <a href="{{ post.url | relative_url }}" class="read-more">Read More &raquo;</a>
    </article>
  {% endfor %}
</div>