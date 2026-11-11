---
title: Career Goals
permalink: /career/
---

# Career Goals

## Where I want to go

My long-term goal is to be a **systems engineer working on low-latency, performance-critical infrastructure**: the kind of software where a few microseconds or one rare edge case decides whether a system works. I'd like to help build infrastructure that a lot of people depend on without noticing. I'm especially interested in the boundary between software and hardware, where my background in mechanical, electrical, and computer engineering has been most useful so far.

## Where I am now

So far I've had the chance to work at both ends of the stack: I've written kernel drivers during an internship, ported analog circuits to a new process in a research lab, and built software projects on my own. I also have clear gaps. My computer architecture knowledge is mostly coursework and one pipelined RV32I core, my FPGA experience is still early, and I need more practice solving algorithm problems under time pressure. Most of my roadmap is aimed at those gaps.

## How I get from here to there

<figure>
  <img src="{{ '/assets/img/roadmap.svg' | relative_url }}" alt="Roadmap from Fall 2026 to an M.S. in ECE in December 2029">
  <figcaption>My roadmap from now through the M.S. (diagram I made)</figcaption>
</figure>

<ul class="timeline">
{% for s in site.data.roadmap %}
  <li{% if s.now %} class="now"{% endif %}>
    <h3>{{ s.title }}</h3>
    <p class="meta">{{ s.stage }}{% if s.now %} · current{% endif %}</p>
    <ul>{% for step in s.steps %}<li>{{ step }}</li>{% endfor %}</ul>
  </li>
{% endfor %}
</ul>

## Why the BS/MS

The BS/MS program lets me double-count courses, so I can finish a master's in about one extra year. For the roles I want, graduate coursework in computer systems would help a lot, and the program gives me time for research with faculty while I'm still at Georgia Tech. Keeping summers free for internships is part of the plan, so I graduate with both depth and industry experience.
