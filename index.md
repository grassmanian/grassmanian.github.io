---
layout: default
title: Placeholder
---

# {{ page.title }}

Contents of the rest of the site end up here at the end of the day. 

<table>
    {% for post in site.posts %}
    <tr>
        <td>{{ post.date | date: "%e %B %Y" }}</td>
        <td><a href="{{ post.url }}">{{ post.title }}</a></td>
    </tr>
    {% endfor %}
</table>
