---
title: 联机托管说明
permalink: index.html
layout: home
ms.openlocfilehash: 928f59a9cdc6a3f70d5ad651fb1b5a45b405cee8
ms.sourcegitcommit: 1117342052bce0bbd5a703bd1f763862b9129807
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/16/2022
ms.locfileid: "140682422"
---
# <a name="azure-data-fundamentals-exercises"></a>Azure 数据基础知识练习

使用以下链接完成针对 Microsoft 课程 [DP-900 Microsoft Azure 数据基础知识](https://docs.microsoft.com/learn/certifications/courses/dp-900t00)的动手实验室练习。

要完成这些练习，需要有一个 Microsoft Azure 订阅。 如果讲师未提供，可以在 [https://azure.microsoft.com](https://azure.microsoft.com) 注册免费试用版。

{% assign labs = site.pages | where_exp:"page", "page.url contains '/Instructions/Labs'" %}
| 模块 | 实验室 |
| --- | --- | 
{% 表示实验室 % 中的活动}| {{ activity.lab.module }} | [{{ activity.lab.title }}{% if activity.lab.type %} - {{ activity.lab.type }}{% endif %}]({{ site.github.url }}{{ activity.url }}) |
{% endfor %}
