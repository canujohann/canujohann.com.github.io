---
layout: page
title: Welcome on my blog
tagline: johann canu
---

{% include JB/setup %}


<div class="alert alert-success">
ウエブ開発に関する知識を共有したいという気持ちでこのブログをスタートしました。
メモ程度にまとめたブログですが、誰かのお役にたてれば幸いです ...
</div>




<h2><i class="fa fa-calendar-o"></i> 記事一覧</h2>


<dl class="dl-horizontal">
  {% for post in site.posts %}
    <dt>{{ post.date | date_to_string }}</dt>
    <dd><a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></dd>
  {% endfor %}
</dl>




