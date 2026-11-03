---
wide: true
image: /assets/og-content-design.png
image_alt: "Showing the right help to the right user. Audience-based content display for more than 200 in-product help pieces, shown to the right role at the right time."
last_updated: 2026-11-03
description: "How I organized in-product help so the right content reached the right user: audience-based display for more than 200 Whatfix help pieces, plus the use-case documentation that kept teams consistent."
---

# Showing the right help to the right user: audience-based content display

<div class="case-summary">
  <dl>
    <div><dt>The challenge</dt><dd>One shared Whatfix deployment at a large insurance company served many different end users. Claims adjusters on calls with customers needed policy information matched to the call, but nothing could be targeted until the customer exposed the user-identifying information the display logic needed.</dd></div>
    <div><dt>My contribution</dt><dd>Designed the audience-based display approach: content shown conditionally based on the end user's role, so claims adjusters saw the policy information for the call they were on. I documented this use case, its requirements, and the implemented solution, and shared it with the customer pre- and post-sales. It was one of 30+ customer use cases I documented across enterprise implementations.</dd></div>
    <div><dt>The result</dt><dd>More than 200 pieces of in-product help, including flows and beacons, delivered to the audiences they were built for, with analytics to track their use. Onboarding for customer representatives got shorter, and support tickets went down.</dd></div>
    <div><dt>Audience</dt><dd>Claims adjusters on customer calls at a large insurance company, and the customer representatives and support teams who use the same deployment.</dd></div>
  </dl>
</div>

## The design question: who sees what

Content design is often described as words on a page. In this work, the design question came first: which users should see which content, and what should stay out of their way.

The content itself was already planned: system updates, new features, warnings about actions to avoid, and guidance for completing a workflow. The missing piece was organization by audience, so each piece reached the adjuster handling the call it was written for.

That decision shaped everything after it. Instead of one undifferentiated library of help, the deployment treated audience as the organizing principle. A flow written for claims adjusters appeared for claims adjusters, and stayed hidden from everyone else.

## The blocker: no identity, no targeting

Audience-based display depends on knowing who the end user is. That information did not exist in the deployment when the work started, and nothing could be built until the customer exposed user-identifying information.

This was stakeholder work before it was build work. I worked with the customer to establish what identifying information could be shared, and in what form, so the display logic had something reliable to decide on. The implementation waited on that agreement. It is the part of the project most easily skipped in a retelling, and the part the whole design depended on.

## What I built

<div class="compare" markdown="1">
<div class="compare-col before" markdown="1">
<p class="compare-label">Before</p>
Help content with no audience logic. Every piece was equally visible, whether or not it matched the user's job, so users had to sort relevant guidance from noise themselves.
</div>
<div class="compare-col after" markdown="1">
<p class="compare-label">After</p>
Content shown conditionally, based on the end user's role. More than 200 pieces, including flows and beacons, reached the audiences they were built for.
</div>
</div>

<div class="callout callout-key">
<p class="callout-title">Why it matters</p>
<p>In-product help that ignores audience teaches users to ignore the help. Targeting is what makes the content feel written for the person reading it.</p>
</div>

<div class="compare" markdown="1">
<div class="compare-col before" markdown="1">
<p class="compare-label">Before</p>
Use cases, requirements, and implemented solutions lived across conversations and individual memory, so different teams could describe the same solution differently.
</div>
<div class="compare-col after" markdown="1">
<p class="compare-label">After</p>
This use case, its requirements, and the implemented solution documented in one place and shared with the customer pre- and post-sales, so every team worked from the same account.
</div>
</div>

<div class="callout callout-key">
<p class="callout-title">Why it matters</p>
<p>Documentation shared before and after a sale keeps the story straight. Customers hear the same account of what was built and why, and internal teams reuse it instead of reinventing it.</p>
</div>

I owned the work end to end: requirements, building and testing, then sharing the result and iterating with the customer.

## What changed

Onboarding for customer representatives got shorter, and support tickets went down. The content did not get louder. It got more precise about who it was for, and the documentation around it gave every team the same account of what existed and why.

## Content decisions worth naming

- **Audience before volume.** More than 200 pieces only help if each one reaches its audience. Organization by user came before adding more content.
- **Decisions documented where teams can reuse them.** This use case was documented and shared pre- and post-sales, so it served selling, onboarding, and support from one source.
- **Build on verified identity.** The display logic was only as good as the user information behind it, so that agreement came first, before any building.
