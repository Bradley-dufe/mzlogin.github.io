---
layout: page
title: About
description: 算法
keywords: Lei Yang,Bradley 
comments: true
menu: 关于
permalink: /about/
---

忧郁的工程师

坚信算法改变人生

逐梦者，筑梦人

## 联系

{% for website in site.data.social %}
* {{ website.sitename }}：[@{{ website.name }}]({{ website.url }})
{% endfor %}

## Skill Keywords

{% for category in site.data.skills %}
### {{ category.name }}
<div class="btn-inline">
{% for keyword in category.keywords %}
<button class="btn btn-outline" type="button">{{ keyword }}</button>
{% endfor %}
</div>
{% endfor %}
