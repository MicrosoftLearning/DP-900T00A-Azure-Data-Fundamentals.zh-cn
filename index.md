---
title: 联机托管说明
permalink: index.html
layout: home
---

# Azure 数据基础知识练习

这些动手练习旨在支持 [Microsoft Learn](https://docs.microsoft.com/training/) 上的培训内容。

若要完成这些练习，你需要一个有管理权限的 Microsoft Azure 订阅。 可在 [https://azure.microsoft.com](https://azure.microsoft.com) 注册免费试用版。

{% assign labs = site.pages | where_exp:"page", "page.url contains '/Instructions/Labs'" %}
| 练习 |
| --- |
{% for activity in labs  %}| [{{ activity.lab.title }}{% if activity.lab.type %} - {{ activity.lab.type }}{% endif %}]({{ site.github.url }}{{ activity.url }}) |
{% endfor %}
