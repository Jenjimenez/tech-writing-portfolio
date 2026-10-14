---
layout: default
title: Jennifer Botia - Technical writing portfolio
home: true
---
<section class="hero container" aria-labelledby="intro-title">
  <h1 id="intro-title">Jennifer Botia</h1>
  <p class="hero-role">{{ site.role | escape }}</p>
  <p class="hero-intro">I turn complex technical concepts into clear, practical documentation that helps people learn, solve problems, and use technology effectively.</p>
  <div class="hero-bottom">
    <p class="current-role">Currently a Technical Content Producer at Pluralsight.</p>
    <a class="button button-primary" href="#writing-samples">Explore writing samples <span aria-hidden="true">&darr;</span></a>
  </div>
</section>

<section id="writing-samples" class="writing-section container" aria-labelledby="writing-title">
  <div class="section-heading">
    <div><p class="eyebrow">Selected work</p><h2 id="writing-title">Featured writing samples</h2></div>
    <p>Process documentation, user guidance,<br class="desktop-only"> and developer reference.</p>
  </div>
  <div class="sample-grid sample-grid--featured">
{% for sample in site.data.samples %}
{% if sample.featured %}
{% include sample-card.html sample=sample %}
{% endif %}
{% endfor %}
  </div>
  <div class="additional-heading"><h2 id="more-writing">More writing samples</h2><p>Additional examples of operational and customer-facing documentation.</p></div>
  <div class="sample-grid sample-grid--secondary" aria-labelledby="more-writing">
{% for sample in site.data.samples %}
{% unless sample.featured %}
{% include sample-card.html sample=sample %}
{% endunless %}
{% endfor %}
  </div>
</section>

<section id="about" class="about-section" aria-labelledby="about-title">
  <div class="container about-grid">
    <div><p class="eyebrow">About my work</p><h2 id="about-title">Writing, testing,<br>and improving content.</h2></div>
    <div class="about-copy">
      <p>I work as a Technical Content Producer at Pluralsight, contributing to courses and hands-on learning experiences across software development, IT, AI, and cloud technologies.</p>
      <p>My work includes technical content reviews, lab validation and troubleshooting, documentation maintenance, and collaboration with authors and cross-functional teams.</p>
      <p>With a background in technical content production, software implementations, and customer enablement, I bring both a technical perspective and a user-focused approach to documentation.</p>
      <p class="focus-line"><strong>Areas of focus</strong><br>Technical documentation &middot; Lab validation &middot; Content quality assurance &middot; Documentation standards</p>
    </div>
  </div>
</section>

<section id="contact" class="container contact-section" aria-labelledby="contact-title">
  <div><p class="eyebrow">Get in touch</p><h2 id="contact-title">Let&rsquo;s talk documentation.</h2><p>Connect with me about technical writing and content opportunities.</p></div>
  <div class="contact-links"><a class="button button-primary" href="mailto:{{ site.email | escape }}">Email Jennifer <span aria-hidden="true">&rarr;</span></a><a class="text-link" href="{{ site.linkedin_url | escape }}">LinkedIn <span aria-hidden="true">&nearr;</span></a>{% if site.resume_path != '' %}<a class="text-link" href="{{ site.resume_path | relative_url }}">View r&eacute;sum&eacute; <span aria-hidden="true">&rarr;</span></a>{% endif %}</div>
</section>
