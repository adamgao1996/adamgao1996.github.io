---
layout: page
title: news
permalink: /news/
published: false
---

<div class="news">
  {% if site.news != blank %}
    {% assign news_size = site.news | size %}
    <div class="table-responsive">
      <table class="table table-sm table-borderless">
        {% assign news = site.news | reverse %}
        
        <!-- Show first 5 news items -->
        <tbody id="news-initial">
          {% for item in news limit: 5 %}
            <tr>
              <th scope="row" style="width: 20%">{{ item.date | date: '%b %d, %Y' }}</th>
              <td>
                {% if item.inline %}
                  {{ item.content | remove: '<p>' | remove: '</p>' | emojify }}
                {% else %}
                  <a class="news-title" href="{{ item.url | relative_url }}">{{ item.title }}</a>
                {% endif %}
              </td>
            </tr>
          {% endfor %}
        </tbody>
        
        <!-- Show remaining news items (hidden by default) -->
        {% if news_size > 5 %}
          <tbody id="news-additional" style="display: none;">
            {% for item in news offset: 5 %}
              <tr>
                <th scope="row" style="width: 20%">{{ item.date | date: '%b %d, %Y' }}</th>
                <td>
                  {% if item.inline %}
                    {{ item.content | remove: '<p>' | remove: '</p>' | emojify }}
                  {% else %}
                    <a class="news-title" href="{{ item.url | relative_url }}">{{ item.title }}</a>
                  {% endif %}
                </td>
              </tr>
            {% endfor %}
          </tbody>
        {% endif %}
      </table>
      
      <!-- Show More / Show Less button -->
      {% if news_size > 5 %}
        <div class="text-center mt-3">
          <button 
            id="news-toggle-btn" 
            class="btn btn-outline-primary btn-sm"
            onclick="toggleNews()"
          >
            Show More ({{ news_size | minus: 5 }} more)
          </button>
        </div>
      {% endif %}
    </div>
  {% else %}
    <p>No news so far...</p>
  {% endif %}
</div>

<script>
function toggleNews() {
  const additionalNews = document.getElementById('news-additional');
  const toggleBtn = document.getElementById('news-toggle-btn');
  
  if (additionalNews.style.display === 'none') {
    additionalNews.style.display = 'table-row-group';
    toggleBtn.textContent = 'Show Less';
    toggleBtn.scrollIntoView({ behavior: 'smooth', block: 'center' });
  } else {
    additionalNews.style.display = 'none';
    toggleBtn.textContent = 'Show More ({{ news_size | minus: 5 }} more)';
    document.getElementById('news-initial').scrollIntoView({ behavior: 'smooth', block: 'start' });
  }
}
</script>

<style>
.btn-outline-primary {
  border-color: var(--global-theme-color);
  color: var(--global-theme-color);
}

.btn-outline-primary:hover {
  background-color: var(--global-theme-color);
  border-color: var(--global-theme-color);
  color: white;
}
</style>
