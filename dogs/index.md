---
layout: default
title: Adoptable Dogs
---
<div class="container marketing">
  <h1>{{ page.title }}</h1>
  <div class="row">
    {% for p in site.pages %}
      {% if p.type == "dog" %}
        <div class="col-lg-4">
          <a href="{{ p.url }}"><img class="img-circle hover-zoom" src="{{ p.images[0] }}" alt="{{ p.dog-name }}" width="140" height="140"></a>
          <h2>{{ p.dog-name }}</h2>
          <p>
            {{ p.gender }}<br />
            {{ p.breed }}<br />
            {{ p.age }}
          </p>
          <p><a class="btn btn-default" href="{{ p.url }}" role="button">More details &raquo;</a></p>
        </div><!-- /.col-lg-4 -->
      {% endif %}
    {% endfor %}
  </div><!-- /.row -->
</div><!-- /.container -->