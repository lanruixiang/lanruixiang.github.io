---
layout: page
title: 题解
description: 题解
keywords: 题解
comments: false
menu: 题解
permalink: /solution/
---

<section class="container solution-content">
{% assign count = 1 %}
{% for solution in site.solution reversed %}
    {% assign year = solution.date | date: '%Y' %}
    {% assign nyear = solution.next.date | date: '%Y' %}
    {% if year != nyear %}
        {% assign count = count | append: ', ' %}
        {% assign counts = counts | append: count %}
        {% assign count = 1 %}
    {% else %}
        {% assign count = count | plus: 1 %}
    {% endif %}
{% endfor %}

{% assign counts = counts | split: ', ' | reverse %}
{% assign i = 0 %}

{% assign thisyear = 1 %}

{% for solution in site.solution %}
    {% assign year = solution.date | date: '%Y' %}
    {% assign nyear = solution.next.date | date: '%Y' %}
    {% if year != nyear %}
        {% if thisyear != 1 %}
            </ol>
        {% endif %}
<h3>{{ solution.date | date: '%Y' }} ({{ counts[i] }})</h3>
        {% if thisyear != 0 %}
            {% assign thisyear = 0 %}
        {% endif %}
        <ol class="solution-list">
        {% assign i = i | plus: 1 %}
    {% endif %}
<li class="solution-list-item">
<span class="solution-list-meta">{{ solution.date | date:"%m-%d" }}</span>
<a class="solution-list-name" href="{{ site.url }}{{ solution.url }}">{{ solution.title }}</a>
</li>
{% endfor %}
</ol>
</section>
