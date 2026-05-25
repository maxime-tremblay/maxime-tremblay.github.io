---
layout: page
title: Search
---

<div id="search-container">
  <input type="text" id="search-input" placeholder="Search posts..." autofocus>
  <p id="search-no-results" style="display:none;">No results found.</p>
  <ul id="results-container"></ul>
</div>

<script src="{{ '/assets/js/simple-jekyll-search.min.js' | relative_url }}" type="text/javascript"></script>
<script>
SimpleJekyllSearch({
  searchInput: document.getElementById('search-input'),
  resultsContainer: document.getElementById('results-container'),
  json: '{{ '/search.json' | relative_url }}',
  searchResultTemplate: '<li class="search-result-item"><a href="{url}" class="search-result-title">{title}</a><span class="search-result-meta">{date}</span><p class="search-result-excerpt">{excerpt}</p><div class="blog-tags search-result-tags">{tags}</div></li>',
  noResultsText: '<li class="search-no-results">No results found.</li>'
});
</script>
