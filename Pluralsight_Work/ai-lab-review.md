---
wide: true
image: /assets/og-ai-lab-review.png
image_alt: "Reviewing AI-generated labs: what I catch and why. A rubric checklist with validation items checked off."
last_updated: 2026-10-25
description: "How I review AI-generated hands-on labs: a triage-first rubric covering validation, solution hygiene, alignment, and style, with feedback written to improve the prompting, not just the draft."
---

# Reviewing AI-Generated Labs: What I Catch and Why

<div class="case-summary">
  <dl>
    <div><dt>The challenge</dt><dd>AI-generated labs read fluently but hide accuracy gaps: solutions that do more than the task asks, validation that doesn't actually pass, instructions that drift from the lab outline, or describe tools the lab environment doesn't have.</dd></div>
    <div><dt>My contribution</dt><dd>Review AI-generated software-development labs against a structured rubric: validation and solution hygiene first, then alignment, relevance, and style, with feedback written to be constructive and clear enough to improve the AI prompting itself.</dd></div>
    <div><dt>The result</dt><dd>On one C# debugging lab: 7 issues flagged across 5 steps in the first round (4 required fixes, 3 suggested improvements), caught in review before learners ever saw them. After a second round of review and code testing, all of the suggested and required changes were implemented, and the lab is now published.</dd></div>
    <div><dt>Audience</dt><dd>Pluralsight learners, who get labs that work, and lab authors, who get feedback they can act on in one pass.</dd></div>
  </dl>
</div>

**How to read this page, in 2 minutes:** process below, then 3 worked examples, then the published outcome. Expand any section for the full before and after.

<div class="process">
<div><div class="process-top"><svg class="icon-svg" width="28" height="28" viewBox="0 0 24 24" aria-hidden="true"><circle cx="11" cy="11" r="7"/><path d="M21 21l-4.3-4.3"/></svg><span class="step-num">01</span></div><h3>Triage</h3><p>Does the lab work at all?</p></div>
<div><div class="process-top"><svg class="icon-svg" width="28" height="28" viewBox="0 0 24 24" aria-hidden="true"><path d="M4 22V4"/><path d="M4 4h13l-2.5 4L17 12H4"/></svg><span class="step-num">02</span></div><h3>First round</h3><p>7 flags, 4 required and 3 suggested</p></div>
<div><div class="process-top"><svg class="icon-svg" width="28" height="28" viewBox="0 0 24 24" aria-hidden="true"><path d="M10 2h4"/><path d="M10 2v6l-5 12a2 2 0 0 0 2 2h10a2 2 0 0 0 2-2L14 8V2"/><path d="M8 15h8"/></svg><span class="step-num">03</span></div><h3>Second round</h3><p>Code testing, standards, wording</p></div>
<div><div class="process-top"><svg class="icon-svg" width="28" height="28" viewBox="0 0 24 24" aria-hidden="true"><circle cx="12" cy="12" r="9"/><path d="M8 12l3 3 5-6"/></svg><span class="step-num">04</span></div><h3>Published</h3><p>All changes implemented, lab published</p></div>
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


<details class="template" markdown="1">
<summary><svg class="summary-icon-svg" width="20" height="20" viewBox="0 0 24 24" aria-hidden="true"><path d="M12 3L22 20H2L12 3z"/><path d="M12 10v4"/><path d="M12 17h.01"/></svg>Error taxonomy: how I grade what I find</summary>

Not every flag is equal. Required means the lab does not work, teaches the wrong thing, or misleads a learner. Suggested means the lab works, but a change would help learners focus or trust the steps.

| Category | Severity | Example from this lab |
|---|---|---|
| Validation failure | Required | A debugging task where the starter code does not throw an exception, so there is nothing to debug. |
| Environment mismatch | Required | Steps that use DataTips, Watch windows, and tracepoints that are not available in the lab editor. |
| Instruction drift from the objective | Required | A task that asks learners to correct a tax calculation instead of investigating an external assembly. |
| Solution hygiene | Required | Starter methods that return placeholder values such as 0 or false, instead of mostly working code with an intentional bug. |
| Workflow gap | Required | No workflow for reproducing a race condition and verifying the fix with Hot Reload. |
| Style and standards | Required | Code font, spacing, and wording that do not follow the Google Developer Documentation Style Guide, or language that guarantees behavior the code cannot guarantee. |
| Learner focus | Suggested | Learners see all 10 tasks at once, or start without running the application first, so they cannot observe an issue, change it, and compare results. |

</details>

## How I work with AI

- I use AI output as a first draft to review, not as a finished lab to publish.
- I never let AI output go unchecked on validation, code, or safety steps. If I did not test it, I do not publish it.
- I write feedback so the next draft improves, not just this draft. That means naming the exact step, the exact wording or code to change, and why it matters for the learner.
- I do not claim prompt engineering expertise beyond that structured feedback. My skill is evaluation: testing, judging accuracy, and writing feedback an author, or a prompting loop, can act on in one pass.

## What happened next: second round, code testing, and publication

After the first round, I reviewed the lab again and tested the code. The second round was mostly standards, wording, and learner setup, not new blockers. All of these changes were implemented, and the lab is now published. Expand a section for the before and after.

<details class="template" markdown="1">
<summary><svg class="summary-icon-svg" width="20" height="20" viewBox="0 0 24 24" aria-hidden="true"><path d="M3 7a2 2 0 0 1 2-2h4l2 2h8a2 2 0 0 1 2 2v9a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V7z"/></svg>Learner setup</summary>

- Kept these files open for learners on startup: `src/OrderLineParser.cs`, `src/DefectClassifier.cs`, and `src/Probe.cs`, so learners start in the code they will debug instead of searching for it.
- Kept **Checkpoint** as a step, but bolded it and capitalized the first letter of the sentence. Example: "4. Checkpoint: Move the `Probe.Watch` line to just after your reset and rerun. It reads 0 for every order, and all five orders match their expected totals. Then remove the `Probe.Watch` line."

</details>

<details class="template" markdown="1">
<summary><svg class="summary-icon-svg" width="20" height="20" viewBox="0 0 24 24" aria-hidden="true"><path d="M4 20h4L19 9l-4-4L4 16v4z"/><path d="M14 6l4 4"/></svg>Readability and standards</summary>

- Added spacing where needed to break up large blocks of text.
- Updated and added code font where needed to align with Google style conventions.

</details>

<details class="template" markdown="1">
<summary><svg class="summary-icon-svg" width="20" height="20" viewBox="0 0 24 24" aria-hidden="true"><circle cx="12" cy="12" r="9"/><circle cx="12" cy="12" r="5"/><circle cx="12" cy="12" r="1"/></svg>Objective and wording</summary>

<div class="compare" markdown="1">
<div class="compare-col before" markdown="1">
<p class="compare-label">Before: objective title</p>
Debug into an external assembly via its symbols and IL
</div>
<div class="compare-col after" markdown="1">
<p class="compare-label">After: objective title</p>
Investigate an external .NET assembly using IL and stack traces
</div>
</div>

<div class="compare" markdown="1">
<div class="compare-col before" markdown="1">
<p class="compare-label">Before: Hot Reload fallback</p>
If `dotnet watch` ever says it can't apply a change in place and asks to restart, answer `y`. The soak starts again with your change.
</div>
<div class="compare-col after" markdown="1">
<p class="compare-label">After: Hot Reload fallback</p>
If `dotnet watch` can't apply a change without restarting, follow the prompt to restart the application. However, the goal of this exercise is to apply and verify the fix in the same running process using Hot Reload.
</div>
</div>

<div class="compare" markdown="1">
<div class="compare-col before" markdown="1">
<p class="compare-label">Before: external assembly explanation</p>
In an IDE you'd load symbols for the assembly and step into its decompiled source. The `inspect` command shows you the same information from the terminal:
</div>
<div class="compare-col after" markdown="1">
<p class="compare-label">After: external assembly explanation</p>
In an IDE, you could use matching symbols to debug the assembly's original source or decompilation to investigate code without the source. In this lab, the `inspect` command provides assembly information, IL, and runtime evidence from the terminal:
</div>
</div>

</details>

<details class="template" markdown="1">
<summary><svg class="summary-icon-svg" width="20" height="20" viewBox="0 0 24 24" aria-hidden="true"><path d="M12 3v18"/><path d="M5 21h14"/><path d="M8 21l-3-9M16 21l3-9"/><path d="M5 12h6M13 12h6"/></svg>Accuracy language: removing guarantees the code cannot make</summary>

<div class="compare" markdown="1">
<div class="compare-col before" markdown="1">
<p class="compare-label">Before: performance claim</p>
Summing tens of thousands of decimals takes **well under a millisecond**, so the parallel loop isn't buying anything.
</div>
<div class="compare-col after" markdown="1">
<p class="compare-label">After: performance claim</p>
A sequential loop is **sufficient** for this workload, so the parallel loop isn't necessary.
</div>
</div>

<div class="compare" markdown="1">
<div class="compare-col before" markdown="1">
<p class="compare-label">Before: state leaking</p>
That **shape** (correct at first, wrong later) **means** state is leaking between calls.
</div>
<div class="compare-col after" markdown="1">
<p class="compare-label">After: state leaking</p>
That **pattern** (correct at first, wrong later) **suggests** state **may be** leaking between calls.
</div>
</div>

<div class="compare" markdown="1">
<div class="compare-col before" markdown="1">
<p class="compare-label">Before: below expected</p>
It's **below the expected figure** and **different every round**...
</div>
<div class="compare-col after" markdown="1">
<p class="compare-label">After: below expected</p>
It **can fall below** the expected figure and **vary between rounds**...
</div>
</div>

<div class="compare" markdown="1">
<div class="compare-col before" markdown="1">
<p class="compare-label">Before: race conditions</p>
**Races reproduce under load**, not by inspection, and they're **different on every run**
</div>
<div class="compare-col after" markdown="1">
<p class="compare-label">After: race conditions</p>
Race conditions **can be difficult to reproduce** because their behavior depends on execution timing. Running the application under load **can help reveal** them.
</div>
</div>

</details>

That second round is why the feedback loop matters. The first round caught whether the lab worked at all. The second round caught whether the language was accurate, consistent, and easy to follow, and whether learners started in the right place.

## The rest of the review

| What I flagged | Severity |
|---|---|
| Task 5.1 asked learners to correct a tax calculation instead of investigating an external assembly; the activity had drifted from its learning objective. | Required |
| Tasks 5.2–5.3 had no workflow for reproducing a race condition and verifying the fix with Hot Reload, which tested successfully in the lab environment. | Required |
| The lab never asked learners to run the application first; suggested introducing a run at the beginning and checkpoints throughout, so learners observe an issue, make changes, and compare results before validating. | Suggested |
| <code>dotnet run</code> displayed all 10 tasks at once; suggested letting learners run individual scenarios so they can focus on the issue they're investigating. | Suggested |
