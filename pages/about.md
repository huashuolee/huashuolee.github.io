---
layout: page
title: About
description: huashuolee Blog
keywords: huashuolee 
comments: true
menu: 关于
permalink: /about/
---

huashuolee, 测试工程师，希望成为一个懂代码的测试工程师。


坚信只有想不到，没有做不到。

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
