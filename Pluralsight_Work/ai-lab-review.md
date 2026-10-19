---
wide: true
# TODO: add a social/OG image, e.g. /assets/og-ai-lab-review.png
last_updated: 2026-10-19
description: "How I review AI-generated hands-on labs: a triage-first rubric covering validation, solution hygiene, alignment, and style, with feedback written to improve the prompting, not just the draft."
---

# Reviewing AI-Generated Labs: What I Catch and Why

<div class="case-summary">
  <dl>
    <div><dt>The challenge</dt><dd>AI-generated labs read fluently but hide accuracy gaps: solutions that do more than the task asks, validation that doesn't actually pass, instructions that drift from the lab outline, or describe tools the lab environment doesn't have.</dd></div>
    <div><dt>My contribution</dt><dd>Review AI-generated software-development labs against a structured rubric: validation and solution hygiene first, then alignment, relevance, and style, with feedback written to be constructive and clear enough to improve the AI prompting itself.</dd></div>
    <div><dt>The result</dt><dd>On one C# debugging lab: 7 issues flagged across 5 steps (4 required fixes, 3 suggested improvements), caught in review before learners ever saw them.</dd></div>
    <div><dt>Audience</dt><dd>Pluralsight learners, who get labs that work, and lab authors, who get feedback they can act on in one pass.</dd></div>
  </dl>
</div>

## How I review: blockers first, content second

AI output gets a triage pass before anything else. If the lab doesn't work, style notes can wait.

1. **Run validation.** Do all tasks and validations pass? Does the solution code contain *only* what the task requests? Immediate issues are raised right away so they get a quick turnaround.
2. **Review content** once major blockers are resolved, against the rubric below.

## The rubric

**Outline and instruction alignment**

- Lab instructions cover all key objectives from the lab outline.
- Content follows internal standards and the Google Developer Documentation Style Guide.

**Relevance and redundancy**

- No repetition or filler.
- Content is meaningful, with examples that build a clear learning progression.

**Feedback, solution, and validation**

- Feedback to the author is constructive and clear, written so it improves AI prompting, not just this draft.
- Solution code contains only the changes the task requests.
- Validation passes with properly marked solutions.
- AI-generated content is marked as such for learners.

## In practice: a C# debugging lab

The lab: **Fixing a C# Application with C# Failure Stack Traces**. Learners reproduce crashes, read stack traces, and fix bugs across five steps.

### The crash that couldn't crash <span class="flag flag-required">Required fix</span>

<div class="compare" markdown="1">
<div class="compare-col before" markdown="1">
<p class="compare-label">What the AI generated</p>
Task 2.1 asks learners to reproduce a crash, but the starter parser doesn't throw an exception. There is nothing to investigate.
</div>
<div class="compare-col after" markdown="1">
<p class="compare-label">What I flagged</p>
A debugging lab where the bug doesn't exist. The task is uncompletable as written: a blocker, not a style nit.

**My feedback:** "Provide a mostly working parser with an intentional bug so learners can investigate the exception and stack trace before fixing it."
</div>
</div>

> **Why it matters:** Learners can't practice debugging if there's nothing to debug.

### Instructions for an editor the learners don't have <span class="flag flag-required">Required fix</span>

<div class="compare" markdown="1">
<div class="compare-col before" markdown="1">
<p class="compare-label">What the AI generated</p>
Steps 3–4 introduce DataTips, Watch windows, and tracepoints, none of which are available in the lab's editor.
</div>
<div class="compare-col after" markdown="1">
<p class="compare-label">What I flagged</p>
The AI described the platonic ideal of Visual Studio debugging, not the environment learners were actually in.

**My feedback:** "Add terminal-based debugging steps so learners can investigate changing values and isolate issues while connecting the activities to the course concepts."
</div>
</div>

> **Why it matters:** Instructions that reference unavailable tools do more than confuse. They erode trust in every step that follows.

### Placeholder code in a debugging lab <span class="flag flag-suggested">Suggested fix</span>

<div class="compare" markdown="1">
<div class="compare-col before" markdown="1">
<p class="compare-label">What the AI generated</p>
Across steps 2–5, several starter methods return placeholder values such as <code>0</code> or <code>false</code>.
</div>
<div class="compare-col after" markdown="1">
<p class="compare-label">What I flagged</p>
Learners would spend the lab implementing functionality from scratch instead of debugging, which is the opposite of the learning objective.

**My feedback:** "Provide more working code with intentional bugs so learners can focus on debugging rather than implementing functionality from scratch."
</div>
</div>

> **Why it matters:** Every minute spent writing boilerplate is a minute not spent on the skill the lab promises to teach. This became a principle I now apply everywhere: in a debugging lab, starter code should be mostly working with intentional bugs, never empty placeholders.

## The rest of the review

| What I flagged | Severity |
|---|---|
| Task 5.1 asked learners to correct a tax calculation instead of investigating an external assembly; the activity had drifted from its learning objective. | Required |
| Tasks 5.2–5.3 had no workflow for reproducing a race condition and verifying the fix with Hot Reload, which tested successfully in the lab environment. | Required |
| The lab never asked learners to run the application first; suggested introducing a run at the beginning and checkpoints throughout, so learners observe an issue, make changes, and compare results before validating. | Suggested |
| <code>dotnet run</code> displayed all 10 tasks at once; suggested letting learners run individual scenarios so they can focus on the issue they're investigating. | Suggested |
