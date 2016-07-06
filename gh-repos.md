---
title: Git Hub Projects
date: 2016-07-06T16:30:09+00:00
author: Matt Erickson (ME)
layout: default
---

<div class="page-content">
  <div class="mdl-grid">
    {% for repository in site.github.public_repositories %}

    <div class="mdl-card mdl-shadow--2dp mdl-cell mdl-cell--4-col mdl-cell--4-col-desktop mdl-cell--4-col-tablet  mdl-cell--12-col-phone">
      <div class="mdl-card__title" {% if repository.image %} style="background: url('{{ repository.image }}') center/cover;" {% endif %}>
        <h2 class="mdl-card__title-text">{{ repository.name }}</h2>
      </div>
      <div class="mdl-card__supporting-text">
        <span>{{ repository.date | date: "%b %-d, %Y" }}</span>
        <p>{{ repository.dscription }}</p>
      </div>
      <div class="mdl-card__actions mdl-card--border">
        <a class="mdl-button mdl-button--colored mdl-js-button mdl-js-ripple-effect" href="{{ repository.url | prepend: site.baseurl }}">
          View on GitHub
        </a>
      </div>
      <div class="mdl-card__menu">
        <button class="mdl-button mdl-button--icon mdl-js-button mdl-js-ripple-effect" id="post-{{ post.id }}">
          <i class="material-icons">share</i>
        </button>
        <ul class="mdl-menu mdl-js-menu mdl-menu--bottom-right" for="post-{{ post.id }}">
          <li><a href="https://www.facebook.com/dialog/share?app_id={{site.facebook_app_id}}&display=page&href={{ post.url | prepend: site.baseurl }}&redirect_uri={{ site.baseurl }}" class="mdl-menu__item">Facebook</a></li>
          <li><a href="https://twitter.com/share?url={{ post.url | prepend: site.baseurl }}&text={{ post.title }}&via={{ site.twitter_username }}" class="mdl-menu__item">Twitter</a></li>
          <li><a href="https://plus.google.com/share?url={{ post.url | prepend: site.baseurl }}" class="mdl-menu__item">Google+</a></li>
        </ul>
      </div>
    </div>

    {% endfor %}
  </div>
</div>