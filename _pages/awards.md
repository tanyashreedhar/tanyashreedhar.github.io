---
layout: page
permalink: /awards/
title: Awards
nav: true
nav_order: 6
category_order: ["Fellowships", "Academic", "Extra Curricular", "Travel Grants"]
---

{% if site.enable_award_categories == true %}

<div class="awards">
  {% assign categories = site.awards | map: 'categories' | join: ',' | split: ',' | uniq %}
  {% assign order = page.category_order %}
  {% for category in order %}
    {% if categories contains category %}
      <h3 class="category">{{ category }}</h3>
      {% assign awards = site.awards | where: "categories", category | where: "display", true %}
      {% assign sorted_awards = awards | sort: "date" | reverse %}
      {% for award in sorted_awards %}
        <div class="col-md-12 mb-4 item">
          <div class="card shadow-sm border-0">
            <div class="card-body">
              <div class="row">
                <div class="col-md-1">
                  <i class="fas fa-award fa-2x"></i>
                </div>
                <div class="col-md-11">
                  {% if award.link %}
                    <h5 class="card-title"><a href="{{ award.link }}">{{ award.title }}</a></h5>
                  {% else %}
                    <h5 class="card-title">{{ award.title }}</h5>
                  {% endif %}
                  {% capture award_date %}{{ award.date | date: "%B %Y" }}{% endcapture %}
                  {% if award.show_month == false %}
                    {% assign parts = award_date | split: " " %}
                    {% assign year = parts[1] %}
                    <p class="card-text"><small class="text-muted award-date">{{ year }}</small></p>
                  {% else %}
                    <p class="card-text"><small class="text-muted award-date">{{ award_date }}</small></p>
                  {% endif %}
                  {% if award.content %}
                    <div class="award-content">
                      {{ award.content }}
                    </div>
                  {% endif %}
                </div>
              </div>
            </div>
          </div>
        </div>
      {% endfor %}
    {% endif %}
  {% endfor %}
  {% if site.awards.size == 0 %}
    <p>No awards found.</p>
  {% endif %}
</div>
{% else %}
<div class="awards">
  {% assign awards = site.awards | where: "display", true %}
  {% assign sorted_awards = awards | sort: "date" | reverse %}
  {% for award in sorted_awards %}
    <div class="col-md-12 mb-4 item">
      <div class="card shadow-sm border-0">
        <div class="card-body">
          <div class="row">
            <div class="col-md-1">
              <i class="fas fa-award fa-2x"></i>
            </div>
            <div class="col-md-11">
              {% if award.link %}
                <h5 class="card-title"><a href="{{ award.link }}">{{ award.title }}</a></h5>
              {% else %}
                <h5 class="card-title">{{ award.title }}</h5>
              {% endif %}
              {% capture award_date %}{{ award.date | date: "%B %Y" }}{% endcapture %}
              {% if award.show_month == false %}
                {% assign parts = award_date | split: " " %}
                {% assign year = parts[1] %}
                <p class="card-text"><small class="text-muted award-date">{{ year }}</small></p>
              {% else %}
                <p class="card-text"><small class="text-muted award-date">{{ award_date }}</small></p>
              {% endif %}
              {% if award.content %}
                <div class="award-content">
                  {{ award.content }}
                </div>
              {% endif %}
            </div>
          </div>
        </div>
      </div>
    </div>
  {% endfor %}
  {% if site.awards.size == 0 %}
    <p>No awards found.</p>
  {% endif %}
</div>
{% endif %}
