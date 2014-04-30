---
layout: page
title: java, ruby, node, PHP ….
tagline: ちょっとしたTips
---

{% include JB/setup %}


My HP [johann canu HP](http://canujohann.com)



## 記事一覧


<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>


