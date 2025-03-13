---
layout: page
title: 搜索
permalink: /search/
---

<div class="search-page">
  <div class="search-container">
    <input type="text" id="search-input" placeholder="输入关键词搜索...">
    <button id="search-button"><i class="fas fa-search"></i></button>
  </div>
  
  <div id="search-results" class="search-results">
    <!-- 搜索结果将在这里显示 -->
  </div>
</div>

<script>
document.addEventListener('DOMContentLoaded', function() {
  // 获取所有文章数据
  fetch('{{ "/search.json" | relative_url }}')
    .then(response => response.json())
    .then(data => {
      const searchInput = document.getElementById('search-input');
      const searchButton = document.getElementById('search-button');
      const searchResults = document.getElementById('search-results');
      
      // 搜索函数
      function performSearch() {
        const query = searchInput.value.toLowerCase();
        if (query.length < 2) {
          searchResults.innerHTML = '<p>请输入至少2个字符...</p>';
          return;
        }
        
        const results = data.filter(item => {
          const titleMatch = item.title.toLowerCase().includes(query);
          const contentMatch = item.content.toLowerCase().includes(query);
          return titleMatch || contentMatch;
        });
        
        displayResults(results);
      }
      
      // 显示结果
      function displayResults(results) {
        if (results.length === 0) {
          searchResults.innerHTML = '<p>未找到匹配的结果</p>';
          return;
        }
        
        let html = '<ul class="search-results-list">';
        results.forEach(item => {
          html += `
            <li>
              <a href="${item.url}">
                <h3>${item.title}</h3>
                <p class="search-excerpt">${item.content.slice(0, 150)}...</p>
                <span class="search-date">${item.date}</span>
              </a>
            </li>
          `;
        });
        html += '</ul>';
        
        searchResults.innerHTML = html;
      }
      
      // 事件监听
      searchButton.addEventListener('click', performSearch);
      searchInput.addEventListener('keyup', function(e) {
        if (e.key === 'Enter') {
          performSearch();
        }
      });
    });
});
</script>

<style>
  .search-page {
    background: white;
    padding: 30px;
    border-radius: 10px;
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.05);
  }
  
  .search-container {
    display: flex;
    margin-bottom: 30px;
  }
  
  #search-input {
    flex: 1;
    padding: 12px 15px;
    border: 1px solid #e0e0e0;
    border-radius: 5px 0 0 5px;
    font-size: 16px;
  }
  
  #search-button {
    padding: 0 20px;
    background: #ff8c8c;
    color: white;
    border: none;
    border-radius: 0 5px 5px 0;
    cursor: pointer;
    transition: background 0.3s;
  }
  
  #search-button:hover {
    background: #ff6b6b;
  }
  
  .search-results-list {
    list-style: none;
    padding: 0;
  }
  
  .search-results-list li {
    margin-bottom: 20px;
    padding-bottom: 20px;
    border-bottom: 1px solid #e0e0e0;
  }
  
  .search-results-list a {
    text-decoration: none;
    color: inherit;
    display: block;
  }
  
  .search-results-list h3 {
    margin: 0 0 10px;
    color: #333;
    transition: color 0.3s;
  }
  
  .search-results-list a:hover h3 {
    color: #ff8c8c;
  }
  
  .search-excerpt {
    color: #666;
    margin: 0 0 5px;
  }
  
  .search-date {
    font-size: 12px;
    color: #828282;
  }
</style> 