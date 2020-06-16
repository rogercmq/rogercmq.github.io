---
layout: page
title: About
description: TODO
keywords: Mengqi Cao
comments: true
menu: 关于
permalink: /about/
---

我是**曹梦奇**，2020年夏天毕业于上海交通大学计算机科学专业（IEEE试点班），已南京大学人工智能学院预录取。最喜欢的国内外 Rapper 是 AR 和 J.Cole，最喜欢的摇滚乐队是高旗&超载乐队。最近在看的书是小椴的《杯雪》，也正在刷伍迪艾伦的电影。

## 联系

<ul>
{% for website in site.data.social %}
<li>{{website.sitename }}：<a href="{{ website.url }}" target="_blank">@{{ website.name }}</a></li>
{% endfor %}
{% if site.url contains 'mazhuang.org' %}
<li>
微信公众号：<br />
<img style="height:192px;width:192px;border:1px solid lightgrey;" src="{{ assets_base_url }}/assets/images/qrcode.jpg" alt="闷骚的程序员" />
</li>
{% endif %}
</ul>


## 擅长调用各种API

{% for skill in site.data.skills %}
### {{ skill.name }}
<div class="btn-inline">
{% for keyword in skill.keywords %}
<button class="btn btn-outline" type="button">{{ keyword }}</button>
{% endfor %}
</div>
{% endfor %}
