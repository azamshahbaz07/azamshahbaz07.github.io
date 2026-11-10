---
title: Home
---

<section class="hero">
  <img src="{{ site.headshot | relative_url }}" alt="Headshot of Azam Shahbaz">
  <div>
    <p class="eyebrow">Computer Engineering · Georgia Tech</p>
    <h1>Hi, I'm Azam.</h1>
    <p>I build software and hardware where timing matters. My work sits where code meets the machine: C++ systems that have to be fast and correct, and the digital hardware they run on.</p>
    <p>I'm a Computer Engineering student at Georgia Tech on the BS/MS track, focused on systems software and computer architecture. I'm looking for a summer 2027 internship in systems, infrastructure, or low-latency engineering.</p>
    <div class="actions">
      <a class="btn" href="{{ '/projects/' | relative_url }}">See my projects</a>
      <a class="btn ghost" href="{{ '/resume/' | relative_url }}">Resume</a>
    </div>
  </div>
</section>

<div class="highlights">
  <div><strong>Systems software</strong><span>A crash-safe key-value store at 150K+ reads/sec, a work-stealing thread pool, and a 2M+ packet/sec analyzer, all in modern C++.</span></div>
  <div><strong>Hardware</strong><span>A pipelined RV32I core, analog IC porting to SKY130, and 4-layer PCB design.</span></div>
  <div><strong>Industry</strong><span>Linux kernel drivers and a C++ control daemon for Qualcomm platforms as a Device Software Engineer Intern at Flock Safety.</span></div>
</div>

## Featured work

<div class="grid">
{% assign featured = site.projects | where: "featured", true | sort: "order" %}
{% for p in featured %}{% include project-card.html p=p %}{% endfor %}
</div>

<p style="margin-top:1.4rem"><a href="{{ '/projects/' | relative_url }}">All projects →</a></p>
