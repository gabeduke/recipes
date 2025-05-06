---
layout: default
title: Recipe Book
---

<h1>Welcome to the Recipe Book</h1>
<p>Browse, discover, and cook up something new! Filter by tag to find your next adventure.</p>

<div class="tag-filters">
  <button class="tag-filter active" data-tag="all">All</button>
  {% assign all_tags = site.tags | sort %}
  {% for tag in all_tags %}
    <button class="tag-filter" data-tag="{{ tag[0] | slugify }}">{{ tag[0] }}</button>
  {% endfor %}
</div>

<div class="recipe-grid">
  {% for post in site.posts %}
    <div class="recipe-card" data-tags="{{ post.tags | join: ' ' | slugify }}">
      <a href="{{ post.url | relative_url }}">
        <div class="recipe-card-content">
          <h2 class="recipe-title">{{ post.title }}</h2>
          <p class="recipe-desc">{{ post.excerpt | strip_html | truncate: 120 }}</p>
          {% if post.tags %}
            <div class="recipe-tags">
              {% for tag in post.tags %}
                <span class="tag">{{ tag }}</span>
              {% endfor %}
            </div>
          {% endif %}
        </div>
      </a>
    </div>
  {% endfor %}
</div>

<script>
document.addEventListener('DOMContentLoaded', function() {
  const filterButtons = document.querySelectorAll('.tag-filter');
  const cards = document.querySelectorAll('.recipe-card');
  filterButtons.forEach(btn => {
    btn.addEventListener('click', function() {
      filterButtons.forEach(b => b.classList.remove('active'));
      this.classList.add('active');
      const tag = this.getAttribute('data-tag');
      cards.forEach(card => {
        if (tag === 'all' || card.getAttribute('data-tags').includes(tag)) {
          card.style.display = '';
        } else {
          card.style.display = 'none';
        }
      });
    });
  });
});
</script>

<style>
.recipe-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(270px, 1fr));
  gap: 2em;
  margin: 2em 0;
}
.recipe-card {
  background: #fffbe9;
  border: 1px solid #e0cfa9;
  border-radius: 1em;
  box-shadow: 0 2px 8px rgba(0,0,0,0.07);
  transition: transform 0.12s;
  overflow: hidden;
}
.recipe-card:hover {
  transform: translateY(-4px) scale(1.02);
  box-shadow: 0 4px 16px rgba(0,0,0,0.12);
}
.recipe-card a {
  color: inherit;
  text-decoration: none;
  display: block;
  height: 100%;
}
.recipe-card-content {
  padding: 1.5em;
}
.recipe-title {
  margin: 0 0 0.5em 0;
  font-size: 1.3em;
  font-weight: bold;
}
.recipe-desc {
  color: #4b3f2a;
  font-size: 1em;
  margin-bottom: 1em;
}
.recipe-tags {
  margin-top: 0.5em;
}
.tag {
  display: inline-block;
  background: #e0cfa9;
  color: #4b3f2a;
  border-radius: 0.5em;
  padding: 0.2em 0.7em;
  font-size: 0.9em;
  margin-right: 0.4em;
  margin-bottom: 0.2em;
}
.tag-filters {
  margin: 2em 0 1em 0;
  display: flex;
  flex-wrap: wrap;
  gap: 0.7em;
}
.tag-filter {
  background: #e0cfa9;
  color: #4b3f2a;
  border: none;
  border-radius: 0.5em;
  padding: 0.4em 1.2em;
  font-size: 1em;
  cursor: pointer;
  transition: background 0.15s, color 0.15s;
}
.tag-filter.active, .tag-filter:hover {
  background: #4b3f2a;
  color: #fffbe9;
}
</style>
