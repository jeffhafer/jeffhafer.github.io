---
layout: default
title: AWS Search
permalink: /aws/
published: true
---
<div id='category_page_title'>AWS</div>
<div id="home">
    <ul class="posts">
        {% assign sorted_posts = site.posts | sort: "title" %}
        {% for post in sorted_posts %}
            {% for category in post.categories %}
                {% if category == "aws" %}
                    <li>&laquo; <span>{{ post.date | date_to_string }}</span>&nbsp;&nbsp;<a href="{{ post.url }}">{{ post.title }}</a></li>
                {%endif%}
            {% endfor %}
        {% endfor %}
    </ul>
</div>
