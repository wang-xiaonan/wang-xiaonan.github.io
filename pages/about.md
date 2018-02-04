---
layout: page
title: About
description: 打码改变世界
keywords: about, 关于
comments: true
menu: 关于
permalink: /about/
---

> 我天性不宜交际。在多数场合，我不是觉得对方乏味，就是害怕对方觉得我乏味。
> 可是我既不愿忍受对方的乏味，也不愿费劲使自己显得有趣，那都太累了。我独处时
> 最轻松，因为我不觉得自己乏味，即使乏味，也自己承受，不累及他人，无需感到不安。

## 联系

{% for website in site.data.social %}
* {{ website.sitename }}：[@{{ website.name }}]({{ website.url }})
  {% endfor %}

## 技能

{% for category in site.data.skills %}
### {{ category.name }}
<div class="btn-inline">
{% for keyword in category.keywords %}
<button class="btn btn-outline" type="button">{{ keyword }}</button>
{% endfor %}
</div>
{% endfor %}
