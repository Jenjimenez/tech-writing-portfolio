---
last_updated: 2026-10-15
description: "How I planned, wrote, and tested this portfolio, with the decisions I made for clarity and accessibility."
---
# How I Built This Site

<div class="case-summary">
  <dl>
    <div><dt>The challenge</dt><dd>My old portfolio used a default theme, looked like a code project, and didn’t show my work at Pluralsight. A hiring manager had to dig to find my strongest samples.</dd></div>
    <div><dt>My contribution</dt><dd>Planned the site, chose the design direction, edited every sample, and reviewed each change before publishing it. I used Claude, an AI assistant, as a pair partner to help write the layout code and run accessibility checks.</dd></div>
    <div><dt>The result</dt><dd>A docs-as-code portfolio that leads with my editing work, explains my role on every sample, and passes automated accessibility checks in light and dark mode.</dd></div>
    <div><dt>Tools</dt><dd>Markdown, Git, GitHub, Jekyll, GitHub Pages, HTML, CSS, and JavaScript.</dd></div>
    <div><dt>The source</dt><dd><a href="https://github.com/Jenjimenez/tech-writing-portfolio">View the code and commit history on GitHub</a>.</dd></div>
  </dl>
</div>

I treated this site the way I treat a lab before publication: decide who it’s for, test every part of it, and revise until a reader can use it without guessing.

## Start with the reader

The people reading this site are hiring managers and recruiters, and most of them skim. Every decision started with one question: can someone find my strongest work in under a minute?

That led to a few rules:

- **Lead with the best evidence.** My before-and-after lab edit is the first sample, and a preview of it sits next to the headline.
- **Say what I did.** Every sample lists my role, such as *wrote*, *edited*, or *tested*, so no one has to guess what was mine.
- **Let readers narrow the list.** Filters group the samples by skill, like *Technical editing* or *Developer documentation*, while keeping my Pluralsight work separate from earlier roles.
- **Keep the focus on writing.** Extras like my career timeline and photo sit lower on the page, after the samples.

## Give the site one clear idea

I wanted the design to show what I do before anyone reads a paragraph, so the site borrows the language of editing:

- The headline is written as a tracked change: “Technical content that ~~is hard to follow~~ works the first time.”
- Comment bubbles explain the reasoning behind real edits, the way I’d leave feedback for an author.
- **Review mode** on the homepage adds my notes on how I wrote the page itself.
- Even the page-not-found page uses the same idea: “This page ~~exists~~ doesn’t exist.”

I kept everything else restrained, with one accent color and no decorative animation, so the samples stay the focus.

## Build it like documentation

The site is docs-as-code, the same workflow many documentation teams use:

- **Markdown** for every writing sample, so the content stays separate from the design.
- **Git** for version history. Every change is a commit, so the history of each sample is visible.
- **Jekyll and GitHub Pages** to build and publish the site automatically after each push.
- **A single data file** that sets the order of the samples, so the previous and next links on each sample stay in sync with the homepage.

## Hold my samples to my own standard

A portfolio is a writing sample too, so I edited it the way I’d edit an author’s lab:

- **Style:** I revised my older samples to follow the Google Developer Documentation Style Guide. For example, I replaced “navigate to” with “go to,” removed abbreviations like “e.g.,” and cut promotional phrases.
- **Accuracy:** I expanded my API reference with example requests, responses, and errors. After a peer review pointed out that one PowerShell example in my VM assertions guide didn’t return the exit code the guide requires, I fixed it and checked the others.
- **Privacy:** I removed internal links, identifiers, and credentials from employer work, replaced client product names with a fictional product, and blurred a colleague’s name in a screenshot.

## Make it accessible

I wanted the site to work for every reader, not just the ones using a mouse on a large screen.

- **Contrast:** I check every page with an automated accessibility tool, in both light and dark mode, including color contrast.
- **Keyboard access:** Every link, button, and filter works with a keyboard and shows a visible focus outline. Wide code blocks and tables can also be scrolled with the keyboard.
- **Screen readers:** Images have descriptions. Switches and filters announce their state, such as “Showing 2 samples.” The tracked changes in my edit examples include hidden “Deleted” and “Inserted” labels, so they make sense when read aloud.
- **Light and dark mode:** The site follows each visitor’s device setting, and a switch in the menu lets them choose the other mode if it’s easier to read.
- **Reduced motion:** Smooth scrolling and small animations turn off for visitors who have reduced motion turned on in their device settings.
- **Phones and print:** Every page adapts to small screens, and printed samples drop the menus and buttons and show the full web address of each link.

## Make it easy to get around

Long technical samples are hard to read on any screen, so each one includes:

- An **On this page** menu that highlights the section you’re reading. On phones, it collapses into a menu at the top.
- **Previous and next** links at the end, so readers can keep going without returning to the homepage.
- A **Back to top** button on long pages, and screenshots that open larger when you select them.

## Ask for feedback, then decide

Before calling the site done, I asked for a peer review, the same way I’d ask for a second reviewer on a lab. I acted on most of the feedback: I added case-study summaries to my Pluralsight samples, made my role on each sample explicit, and trimmed my skills list to tools I can discuss in depth.

I pushed back on a few suggestions, too. For example, I kept my homepage introduction to one paragraph instead of two, because a longer introduction would compete with the samples. Deciding what *not* to change is part of editing.

## What’s next

- Add a sample for the tools that don’t have one yet, starting with AWS CloudFormation.
- Translate one sample into Spanish, to show my bilingual work rather than just list it.
- Keep each sample current, and update the date at the top of the page when I do.
