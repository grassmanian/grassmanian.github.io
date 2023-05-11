---
layout: default
title: A Little into Math
---

# {{ page.title }}

A semi-anonymous blog about math, CS, and various other interests. I believe that writing is an incredibly important skill, and one that takes lots of practice to truly develop, and this is a semi-public means to grow those skills. Check out the [About](/about.html) page for more general information, else peruse the links below. 

<table>
    {% for post in site.posts %}
    <tr>
        <td>{{ post.date | date: "%e %B %Y" }}</td>
        <td><a href="{{ post.url }}">{{ post.title }}</a></td>
    </tr>
    {% endfor %}
</table>
