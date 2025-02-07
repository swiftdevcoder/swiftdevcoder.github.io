---
title: 검색
layout: page
permalink: /search/
---

<h1>검색</h1>

<input type="text" id="search-input" placeholder="검색어를 입력하세요">

<div id="search-results"></div>

<script>
  const searchInput = document.getElementById('search-input');
  const searchResults = document.getElementById('search-results');

  searchInput.addEventListener('input', function() {
    const query = this.value.toLowerCase();
    searchResults.innerHTML = ''; // 검색 결과 초기화

    if (query.length > 0) {
      // Jekyll 검색 API 호출
      fetch('/search.json')
        .then(response => response.json())
        .then(data => {
          const results = data.filter(item => {
            return item.title.toLowerCase().includes(query) ||
                   item.content.toLowerCase().includes(query);
          });

          // 검색 결과 표시
          results.forEach(result => {
            const resultItem = document.createElement('div');
            resultItem.innerHTML = `<h3><a href="${result.url}">${result.title}</a></h3><p>${result.excerpt}</p>`;
            searchResults.appendChild(resultItem);
          });
        });
    }
  });
</script>