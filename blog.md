---
title: Blog
permalink: /blog/
layout: page
excerpt: Arsip tulisan
comments: false
---

<div class="search-article">
  <label for="search-input" aria-hidden="true">
    <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="rgba(128,128,128,0.8)" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="feather feather-search"><circle cx="11" cy="11" r="8"></circle><line x1="21" y1="21" x2="16.65" y2="16.65"></line></svg>
  </label>
  <input type="search" id="search-input" placeholder="Find some articles" aria-label="Search">
</div>

<ul id="search-results"></ul>

{%- for post in site.posts -%}
  {%- capture current_year -%}{{ post.date | date: "%Y" }}{%- endcapture -%}
  {%- unless current_year == previous_year -%}
    <h2>{{ current_year }}</h2>
    {%- assign previous_year = current_year -%}
  {%- endunless -%}
  <article class="post-item">
    <span class="post-item-date">{{ post.date | date: "%b %d" }}</span>
    <h3 class="post-item-title">
      <a href="{{ post.url }}">{{ post.title | escape }}</a>&nbsp;
      [{% for tag in post.tags %}
      {% if forloop.last %}
      <a href="/tags#{{ tag }}">{{ tag }}</a>
      {% else %}
      <a href="/tags#{{ tag }}">{{ tag }}</a>, 
      {% endif %}
      {% endfor %}]
    </h3> 
    <!-- <h3 class="post-item-title">
      <table id="utama">
        <tbody>
            <th>{{ post.date | date: "%b" }}</th>
            <td><a href="{{ post.url }}">{{ post.title | escape }}</a></td>
            <td>
                [{% for tag in post.tags %}
                {% if forloop.last %}
                <a href="/tags#{{ tag }}">{{ tag }}</a>
                {% else %}
                <a href="/tags#{{ tag }}">{{ tag }}</a>, 
                {% endif %}
                {% endfor %}]
            </td>
        </tbody>
      </table>
    </h3> --> 
  </article>
{%- endfor -%}