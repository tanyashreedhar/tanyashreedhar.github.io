---
layout: page
permalink: /services/
title: Services
description: 
nav: true
nav_order: 5
layout: page
---

<div class="services">
  {% for category in site.data.services %}
    {% assign committee_type = category[0] %}
    {% assign committees = category[1] %}
    <h3 class="category">{{ committee_type }}</h3>
    <table class="table">
      <tbody>
        {% for committee in committees %}
          {% assign years = committee.years | map: "year" %}
          {% assign urls = committee.years | map: "url" %}
          <tr>
            <td class="conference-name">{{ committee.conference }}</td>
            <td class="years">
              {% for year in years %}
                {% assign year_url = committee.years | where: "year", year %}
                {% if year_url[0].url %}
                  <a href="{{ year_url[0].url }}">{{ year }}</a><span class="year-padding"></span>{% unless forloop.last %}&nbsp;&bull;&nbsp;{% endunless %}
                {% else %}
                  {{ year }}<span class="year-padding"></span>{% unless forloop.last %}&nbsp;&bull;&nbsp;{% endunless %}
                {% endif %}
                {% if year_url[0].comment %}
                <br>
                <code class="comment"> {{ year_url[0].comment }} </code>
                {% endif %}
              {% endfor %}
            </td>
          </tr>
        {% endfor %}
      </tbody>
    </table>
  {% endfor %}
</div>

<!-- <div class="services">
  {% for category in site.data.services %}
    {% assign committee_type = category[0] %}
    {% assign committees = category[1] %}
    <h3 class="category">{{ committee_type }}</h3>
    <table class="table">
      <tbody>
        {% assign conferences = committees | group_by: 'conference' %}
        {% for conference in conferences %}
          {% assign conference_years = conference.items | map: 'year' %}
          {% assign conference_years_with_comments = conference.items | where: 'comment', true %}
          {% assign conference_years_without_comments = conference.items | where: 'comment', false %}
          {% if conference_years_with_comments.size > 0 %}
            {% for year_index in (0..conference_years_with_comments.size-1) %}
              {% assign year = conference_years_with_comments[year_index] %}
              <tr>
                {% if year_index == 0 %}
                  <td rowspan="{{ conference_years_with_comments.size }}" class="conference-name">{{ conference.name }}</td>
                {% endif %}
                <td class="years">{{ year.year }}</td>
                <td class="comment">{{ year.comment }}</td>
                <td class="year-url"><a href="{{ year.url }}">{{ year.year }}</a></td>
              </tr>
            {% endfor %}
          {% endif %}
          {% if conference_years_without_comments.size > 0 %}
            {% for year_index in (0..conference_years_without_comments.size-1) %}
              {% assign year = conference_years_without_comments[year_index] %}
              <tr>
                {% if year_index == 0 and conference_years_with_comments.size == 0 %}
                  <td class="conference-name">{{ conference.name }}</td>
                {% endif %}
                <td class="years">{{ year.year }}</td>
                <td></td>
                <td class="year-url"><a href="{{ year.url }}">{{ year.year }}</a></td>
              </tr>
            {% endfor %}
          {% endif %}
        {% endfor %}
      </tbody>
    </table>
  {% endfor %}
</div> -->



