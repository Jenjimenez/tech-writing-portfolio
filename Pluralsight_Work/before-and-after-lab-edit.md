---
wide: true
---
# Before and After: Editing a Hands-On AWS Lab

> **About this sample**
>
> - **Lab:** [Release and Roll Back an AWS Cloud-Native Workload](https://www.pluralsight.com/labs/aws/release-and-roll-back-an-aws-cloud-native-workload), a Pluralsight hands-on lab
> - **Audience:** Cloud engineers practicing canary releases and rollbacks with AWS Lambda, CodeDeploy, and CloudWatch
> - **My role:** Technical review and editing before publication: I ran the lab end to end, then revised the guide for accuracy, scannability, and Pluralsight and Google developer style
>
> In this lab, learners release a faulty Lambda version through a CodeDeploy canary, watch a CloudWatch alarm catch the errors, and roll the release back. Below are six edits from my review, each with the original text, my revision, and why I made the change.

The original guide was technically sound. My edits focused on one question: can a learner who has never seen this console follow every step without stopping to guess?

## Tell learners how to get there

<div class="compare" markdown="1">
<div class="compare-col before" markdown="1">
<p class="compare-label">Original</p>

1. In the AWS Console, open **Lambda**.

</div>
<div class="compare-col after" markdown="1">
<p class="compare-label">Revised</p>

1. In the AWS console, use the search bar to search for and select **Lambda** under **Services**.

</div>
</div>

**Why:** "Open **Lambda**" assumes the learner already knows where Lambda is in a console with more than 200 services. The revision gives them the fastest reliable path, and I applied the same pattern to every service the lab uses: CodeDeploy, CloudWatch, and CloudShell.

## Keep one action per step

<div class="compare" markdown="1">
<div class="compare-col before" markdown="1">
<p class="compare-label">Original</p>

{: start="20"}
20. Confirm that no CloudWatch alarm is attached to this deployment group. CodeDeploy does not interpret a Lambda invocation's `FunctionError` as a failed traffic-shift step. Because this independent alarm is not attached, CodeDeploy will continue the release unless you stop it. This lab keeps that decision visible so that you can interpret the evidence and trigger the rollback yourself.

</div>
<div class="compare-col after" markdown="1">
<p class="compare-label">Revised</p>

{: start="19"}
19. Confirm that no CloudWatch alarm is attached to this deployment group.

    > **Note:** CodeDeploy does not interpret a Lambda invocation's `FunctionError` as a failed traffic-shift step. Because this independent alarm is not attached, CodeDeploy will continue the release unless you stop it. This lab keeps that decision visible so that you can interpret the evidence and trigger the rollback yourself.

</div>
</div>

**Why:** The explanation matters, but inside the step it buries the action. Moving it into a note lets learners scan the numbered steps to see what to do, and read the note to understand why. I applied this throughout the lab, so most steps are now a single line.

## Cut what learners don't need

<div class="compare" markdown="1">
<div class="compare-col before" markdown="1">
<p class="compare-label">Original</p>

The final line starts the loop in the background and immediately saves its process ID as one compound shell command, preventing CloudShell from leaving the PID-file command unsubmitted at a new prompt. This loop repeatedly exercises the learner-facing `prod` alias so the 10-percent canary produces several real version 2 samples. Each request records the executed version and any function error in a log; the response body is overwritten because you will inspect the function response directly in the Lambda Console. At 120 requests, the sample normally contains multiple version 2 failures, while the one-second pause keeps traffic controlled and well inside the 30-minute bake window. [...]

</div>
<div class="compare-col after" markdown="1">
<p class="compare-label">Revised</p>

> **Note:** This loop runs in the background and saves its process ID so you can inspect the results later. It repeatedly invokes the production `prod` alias, allowing the 10-percent canary to route some requests to version 2. Each request records the executed version and any function error in `/home/cloud_user/lab/output/canary-traffic.log`.
>
> With 120 requests, you should normally see multiple version 2 failures while remaining within the 30-minute canary window.

</div>
</div>

**Why:** The original explained how the command was engineered, including a CloudShell workaround that matters to the author but not the learner. The revision keeps what learners need to understand the result, adds the path to the log file they'll check later, and replaces internal phrasing like "learner-facing alias" with plain language.

## Name the control, not just the label

<div class="compare" markdown="1">
<div class="compare-col before" markdown="1">
<p class="compare-label">Original</p>

<ol start="4"><li>Choose <strong>Aliases</strong>.</li></ol>
<ol start="11"><li>After the invocation result appears, choose <strong>Details</strong>.</li></ol>

</div>
<div class="compare-col after" markdown="1">
<p class="compare-label">Revised</p>

<ol start="4"><li>Choose the <strong>Aliases</strong> tab.</li></ol>
<ol start="10"><li>After the invocation result appears, expand <strong>Details</strong>.</li></ol>

</div>
</div>

**Why:** In the Lambda console, **Aliases** is a tab and **Details** is an expandable section. Saying what kind of control to look for helps learners find it faster, and using the verb that matches the control, such as *expand* for a collapsed section, tells them what will happen when they click.

## Mark what success looks like

<div class="compare" markdown="1">
<div class="compare-col before" markdown="1">
<p class="compare-label">Original</p>

{: start="15"}
15. Verify the workstation identity:

    ```bash
    aws sts get-caller-identity
    ```

    The `Arn` should contain `assumed-role/globomantics-orders-workstation-role`.

</div>
<div class="compare-col after" markdown="1">
<p class="compare-label">Revised</p>

{: start="12"}
12. Verify the workstation identity:

    ```bash
    aws sts get-caller-identity
    ```

    **Expected output:** The `Arn` should contain `assumed-role/globomantics-orders-workstation-role`.

</div>
</div>

**Why:** Learners check their work after almost every command. A consistent **Expected output** label makes those checks easy to spot, and I used the same pattern for each objective's summary, renamed from **Outcome** to **Expected outcome**.

## Plan for what can go wrong

<div class="compare" markdown="1">
<div class="compare-col before" markdown="1">
<p class="compare-label">Original</p>

*No guidance on reconnecting.*

</div>
<div class="compare-col after" markdown="1">
<p class="compare-label">Revised</p>

> **Note:** During this lab, your workstation session might disconnect. If this happens, return to CloudShell and repeat the SSH connection steps in this section to reconnect to the workstation.

</div>
</div>

**Why:** The lab runs for up to 30 minutes of canary time, and SSH sessions from CloudShell can time out while learners wait or switch tabs. Without this note, a dropped session looks like a broken lab. One sentence tells learners how to recover on their own.
