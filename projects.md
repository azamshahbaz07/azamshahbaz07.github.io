---
title: Projects
permalink: /projects/
---

# Projects

These are things I've designed and built myself. Each page explains the problem, how I approached it, and what came out of it. I add to this page as I finish new work at Georgia Tech.

## ECE Discovery Project

{% assign disc = site.projects | where: "category", "discovery" %}
{% if disc.size > 0 %}
<div class="grid">
{% for p in disc %}{% include project-card.html p=p %}{% endfor %}
</div>
{% else %}
<p class="note">My ECE 1100 Discovery Project is in progress. A full write-up with photos will be posted here before the Discovery Project Showcase.</p>
{% endif %}

## Systems software

<div class="grid">
{% assign sw = site.projects | where: "category", "software" | sort: "order" %}
{% for p in sw %}{% include project-card.html p=p %}{% endfor %}
</div>

## Hardware

<div class="grid">
{% assign hw = site.projects | where: "category", "hardware" | sort: "order" %}
{% for p in hw %}{% include project-card.html p=p %}{% endfor %}
</div>
