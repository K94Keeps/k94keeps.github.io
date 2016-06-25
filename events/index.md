---
layout: default
title: Upcoming Events
---
<div class="container">
  <h1>{{ page.title }}</h1>
  <div class="row">
    {% for p in site.pages %}
      {% if p.type == "event" %}
        <div class="col-md-4 text-center">
          <a href="{{ p.url }}"><img class="img-circle hover-zoom" src="{{ p.img }}" alt="{{ p.event-name }}" width="140" height="140"></a>
          <h2>{{ p.event-name }}</h2>
          <p>
            {{ p.location }}<br />
            {{ p.date | date: '%B %d, %Y' }}
          </p>
          <p><a class="btn btn-default" href="{{ p.url }}" role="button">More details &raquo;</a></p>
        </div><!-- /.col-md-4 -->
      {% endif %}
    {% endfor %}
  </div><!-- /.row -->
</div><!-- /.container -->
