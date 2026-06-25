---
title: 포트폴리오
icon: fas fa-briefcase
order: 5
---

> 직접 기획·개발한 프로젝트들입니다. 제목을 클릭하면 상세 페이지로 이동합니다.
{: .prompt-tip }

## 📱 모바일 앱

{% assign apps = site.posts | where_exp: "p", "p.categories contains '앱'" %}
{% for post in apps %}
### [{{ post.title }}]({{ post.url | relative_url }})

{{ post.description }}
{% if post.tags %}
`{{ post.tags | join: "` · `" }}`
{% endif %}
{% endfor %}

## 🌐 웹 프로젝트

{% assign webs = site.posts | where_exp: "p", "p.categories contains '웹'" %}
{% for post in webs %}
### [{{ post.title }}]({{ post.url | relative_url }})

{{ post.description }}
{% if post.tags %}
`{{ post.tags | join: "` · `" }}`
{% endif %}
{% endfor %}
