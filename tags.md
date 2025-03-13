---
layout: page
title: 标签
permalink: /tags/
---

<div class="tags-page">
  <div class="tag-cloud">
    {% assign tags = site.tags | sort %}
    {% for tag in tags %}
      <a href="#{{ tag[0] }}" class="tag" 
         style="font-size: {{ tag[1].size | times: 4 | plus: 14 }}px">
        {{ tag[0] }}
      </a>
    {% endfor %}
  </div>

  <div class="tag-sections">
    {% for tag in tags %}
      <div class="tag-section">
        <h2 id="{{ tag[0] }}">{{ tag[0] }}</h2>
        <ul class="post-list">
          {% for post in tag[1] %}
            <li>
              <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
              <span class="post-date">{{ post.date | date: "%Y-%m-%d" }}</span>
            </li>
          {% endfor %}
        </ul>
      </div>
    {% endfor %}
  </div>
</div>

<style>
  .tags-page {
    background: white;
    padding: 30px;
    border-radius: 10px;
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.05);
  }
  
  .tag-cloud {
    margin-bottom: 40px;
    padding: 20px;
    background: #f9f9f9;
    border-radius: 5px;
    text-align: center;
  }
  
  .tag {
    display: inline-block;
    margin: 5px;
    padding: 3px 10px;
    background: #ff8c8c;
    color: white;
    border-radius: 15px;
    transition: all 0.3s;
  }
  
  .tag:hover {
    background: #ff6b6b;
    transform: translateY(-2px);
  }
  
  .tag-section {
    margin-bottom: 30px;
  }
  
  .tag-section h2 {
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