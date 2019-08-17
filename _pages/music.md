---
permalink: /music/
title: "Music"
toc: true
---

## 作った曲

<iframe width="100%" height="450" scrolling="no" frameborder="no" src="https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/users/40540645&amp;color=%23368a56&amp;auto_play=false&amp;hide_related=false&amp;show_comments=true&amp;show_user=true&amp;show_reposts=false&amp;show_teaser=true"></iframe>

### 使用機材

<dl>
  {% for equipment in site.data.music.equipments %}
    <dt>{{ equipment.category }}</dt>
    {% for tool in equipment.tools %}
      <dd>
        {% if tool.asin %}
          <a href="https://www.amazon.co.jp/dp/{{ tool.asin }}?tag=sankichi92-22" target="_blank">{{ tool.maker }} {{ tool.name }}</a>
        {% else %}
          {{ tool.maker }} {{ tool.name }}
        {% endif %}
      </dd>
    {% endfor %}
  {% endfor %}
</dl>
