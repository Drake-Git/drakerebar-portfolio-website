---
layout: page
title: Projects
permalink: /projects/
---

### Recent Technical Projects

{% for project in site.projects %}
* **[{{ project.title }}]({{ project.url }})** - {{ project.description }}
{% endfor %}