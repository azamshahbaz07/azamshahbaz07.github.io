---
title: Career Goals
permalink: /career/
---

# Career Goals

## Where I want to go

My long-term goal is to be a **systems engineer working on low-latency, performance-critical infrastructure**: the kind of software where a few microseconds or one rare edge case decides whether a system works. I see myself at a large technology company building infrastructure that millions of people depend on without noticing, or at a trading firm, where latency is the product. Either way, I want to work at the boundary between software and hardware, because that's where my background in mechanical, electrical, and computer engineering gives me an advantage.

## Where I am now

I have real experience at both ends of the stack. I've written kernel drivers in industry, ported analog circuits to a new process, and built C++ systems projects from scratch. I want to be honest about my gaps too. My computer architecture knowledge is mostly coursework and one pipelined RV32I core, my FPGA experience is still early, and I need more practice solving algorithm problems in C++ under time pressure. Most of my roadmap is aimed at those gaps.

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

The BS/MS program lets me double-count courses, so I can finish a master's in about one extra year. For the roles I want, graduate coursework in computer systems and architecture is a real advantage, and it gives me time for research with faculty while I'm still at Georgia Tech. Keeping summers free for internships is part of the plan, so I graduate with both depth and industry experience.
