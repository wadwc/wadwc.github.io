# Welcome to WeAreDevelopers WorldCongress 2024 Demos

<img width="300" alt="image" src="https://cdn.prod.website-files.com/5e9996a6531fea7d1003b18e/6414b1e3b9640fcca069b10b_Humans-General.png">

> > > ### Demos

<style>
  
@keyframes colorChange {
  0% { background-color: #f9f9f9; }
  50% { background-color: #e0e0e0; }
  100% { background-color: #f9f9f9; }
}

.odd {
  animation: colorChange 15s infinite;
}

@keyframes colorChangeEven {
  0% { background-color: #e0e0e0; }
  50% { background-color: #f9f9f9; }
  100% { background-color: #e0e0e0; }
}

.even {
  animation: colorChangeEven 15s infinite;
}
</style>

{% assign counter = 0 %}

<ul>
{% assign sorted_repositories = site.github.public_repositories | sort: "name" %}
{% for repo in sorted_repositories %}
  {% if repo.owner.login == 'wadwc' and repo.name contains 'demo' %}
    {% unless repo.name contains 'github.io' or repo.fork %}
      {% assign row_class = counter | modulo: 2 | times: 1 | plus: 1 %}
      <li>
        <a class="{% if row_class == 1 %}odd{% else %}even{% endif %}" href="https://wadwc.github.io/{{ repo.name }}">{{ repo.name  | replace: '-', ' ' }}</a>
          <p class="repo-description">{{ repo.description | default: "" }}</p>
        <p class="repo-updated">Last updated: {{ repo.updated_at | date: "%B %d, %Y" }}</p>
      </li>
      {% assign counter = counter | plus: 1 %}
    {% endunless %}
  {% endif %}
{% endfor %}
</ul>
{% if counter == 0 %}
  <p>No demos found.</p>
{% endif %}
