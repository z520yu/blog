---
layout: page
title: 分类
permalink: /categories/
---

<div class="categories-page">
  {% for category in site.categories %}
    <div class="category-section">
      <h2 id="{{ category[0] }}">{{ category[0] }}</h2>
      <ul class="post-list">
        {% for post in category[1] %}
          <li>
            <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
            <span class="post-date">{{ post.date | date: "%Y-%m-%d" }}</span>
          </li>
        {% endfor %}
      </ul>
    </div>
  {% endfor %}
</div>

<style>
  .categories-page {
    background: white;
    padding: 30px;
    border-radius: 10px;
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.05);
  }
  
  .category-section {
    margin-bottom: 30px;
  }
  
  .category-section h2 {
    padding-bottom: 10px;
    border-bottom: 1px solid #e0e0e0;
    color: #ff8c8c;
  }
  
  .post-list {
    list-style: none;
    padding-left: 20px;
  }
  
  .post-list li {
    margin: 10px 0;
    display: flex;
    justify-content: space-between;
  }
  
  .post-date {
    color: #828282;
    font-size: 14px;
  }
</style> 