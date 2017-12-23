---
permalink: /sf/
title: "SF"
toc: true
---

## 書いた記事

<ul>
  {% for post in site.categories.SF %}
    <li><a href="{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

## 読んだ本

{% assign books_by_year = site.data.sf.books | group_by_exp: "book", "book.date | date: '%Y'" %}
{% for year in books_by_year %}

### {{ year.name }}

<ul>
  {% for book in year.items %}
    <li>
      <a href="https://www.amazon.co.jp/dp/{{ book.asin }}?tag=sankichi92-22" target="_blank">
        {{ book.author }}『{{ book.title }}』
      </a>
    </li>
  {% endfor %}
</ul>

{% endfor %}
