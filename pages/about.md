---
layout: page
title: About
description: TODO
keywords: Mengqi Cao
comments: true
menu: 关于
permalink: /about/
---

我就是一傻逼孩子，2020年夏天毕业于上海交通大学计算机科学与技术专业（IEEE试点班），已被南京大学人工智能学院预录取，录取通知书还没有发因为档案还他妈的没有邮寄到南京。

# 联系方式

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


# 专业技能

{% for skill in site.data.skills %}
## {{ skill.name }}
<div class="btn-inline">
{% for keyword in skill.keywords %}
<button class="btn btn-outline" type="button">{{ keyword }}</button>
{% endfor %}
</div>
{% endfor %}



# 兴趣爱好

**最爱的音乐人 (排名不分先后)**: Howie Lee; J.Cole; AR刘夫阳; 野孩子; 野外合作社; Kevin Abstract; Kanye West; 高旗&超载乐队; 万能青年旅店; 惘闻; 魏如萱; 零壹乐队; Nirvana

**最爱的电影 (排名不分先后)**: 《教父》三部曲; 《爱在》三部曲; 《幻想曲2000》; 《宿醉》三部曲; 《热天午后》; 《疤面煞星》; 《无间道》前两部; 《枪火》; 《笑傲江湖之东方不败》; 《喜剧之王》; 《人在囧途》; 《天注定》

正在练习吉他。

longboard 板混, 有块燃烧冰Flamingo, 还在练习 pivot。

会游泳，教练给我的评价是“不习水性”，建议别自己去游泳。

深田老师，永远滴神。