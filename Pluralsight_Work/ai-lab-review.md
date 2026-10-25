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


## Error taxonomy: how I grade what I find

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

## How I work with AI

- I use AI output as a first draft to review, not as a finished lab to publish.
- I never let AI output go unchecked on validation, code, or safety steps. If I did not test it, I do not publish it.
- I write feedback so the next draft improves, not just this draft. That means naming the exact step, the exact wording or code to change, and why it matters for the learner.
- I do not claim prompt engineering expertise beyond that structured feedback. My skill is evaluation: testing, judging accuracy, and writing feedback an author, or a prompting loop, can act on in one pass.

## What happened next: second round, code testing, and publication

After the first round, I reviewed the lab again and tested the code. The second round was mostly standards, wording, and learner setup, not new blockers. All of these changes were implemented, and the lab is now published.

**Learner setup**

- Kept these files open for learners on startup: src/OrderLineParser.cs, src/DefectClassifier.cs, and src/Probe.cs, so learners start in the code they will debug instead of searching for it.
- Kept Checkpoint as a step, but bolded it and capitalized the first letter of the sentence. Example: "4. Checkpoint: Move the Probe.Watch line to just after your reset and rerun. It reads 0 for every order, and all five orders match their expected totals. Then remove the Probe.Watch line."

**Readability and standards**

- Added spacing where needed to break up large blocks of text.
- Updated and added code font where needed to align with Google style conventions.

**Objective and wording, before and after**

Objective title, before: "Debug into an external assembly via its symbols and IL"
Objective title, after: "Investigate an external .NET assembly using IL and stack traces"

Hot Reload fallback, before: "If `dotnet watch` ever says it can't apply a change in place and asks to restart, answer `y`. The soak starts again with your change."
Hot Reload fallback, after: "If `dotnet watch` can't apply a change without restarting, follow the prompt to restart the application. However, the goal of this exercise is to apply and verify the fix in the same running process using Hot Reload."

External assembly explanation, before: "In an IDE you'd load symbols for the assembly and step into its decompiled source. The `inspect` command shows you the same information from the terminal:"
External assembly explanation, after: "In an IDE, you could use matching symbols to debug the assembly's original source or decompilation to investigate code without the source. In this lab, the `inspect` command provides assembly information, IL, and runtime evidence from the terminal:"

**Accuracy language: removing guarantees the code cannot make**

Performance claim, replaced: "Summing tens of thousands of decimals takes well under a millisecond, so the parallel loop isn't buying anything."
Performance claim, with: "A sequential loop is sufficient for this workload, so the parallel loop isn't necessary."

State leaking, replaced: "That shape (correct at first, wrong later) means state is leaking between calls."
State leaking, with: "That pattern (correct at first, wrong later) suggests state may be leaking between calls."

Below expected, replaced: "It's below the expected figure and different every round..."
Below expected, with: "It can fall below the expected figure and vary between rounds..."

Race conditions, before: "Races reproduce under load, not by inspection, and they're different on every run"
Race conditions, with: "Race conditions can be difficult to reproduce because their behavior depends on execution timing. Running the application under load can help reveal them."

That second round is why the feedback loop matters. The first round caught whether the lab worked at all. The second round caught whether the language was accurate, consistent, and easy to follow, and whether learners started in the right place.

## The rest of the review

| What I flagged | Severity |
|---|---|
| Task 5.1 asked learners to correct a tax calculation instead of investigating an external assembly; the activity had drifted from its learning objective. | Required |
| Tasks 5.2–5.3 had no workflow for reproducing a race condition and verifying the fix with Hot Reload, which tested successfully in the lab environment. | Required |
| The lab never asked learners to run the application first; suggested introducing a run at the beginning and checkpoints throughout, so learners observe an issue, make changes, and compare results before validating. | Suggested |
| <code>dotnet run</code> displayed all 10 tasks at once; suggested letting learners run individual scenarios so they can focus on the issue they're investigating. | Suggested |
