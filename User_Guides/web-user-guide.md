---
last_updated: 2026-10-14
---
# User Guide: Getting Started with GuideFlow on Web

> **About this sample**
>
> - **Type:** Getting-started user guide
> - **Audience:** Customer admins and content creators setting up in-app guidance
> - **My role:** Wrote the guide while implementing the platform for enterprise customers
- **Source:** Earlier freelance work, anonymized, not current Pluralsight work
>
> This sample is based on documentation I wrote for a digital adoption platform. Product names, URLs, and identifiers have been replaced with a fictional product, *GuideFlow*, to protect client and employer confidentiality.

## Table of contents

1. [Introduction](#introduction)
1. [Set up GuideFlow](#set-up-guideflow)
1. [Create a flow](#create-a-flow)
1. [Publish and test a flow](#publish-and-test-a-flow)
1. [Review flow analytics](#review-flow-analytics)
1. [Troubleshoot common issues](#troubleshoot-common-issues)
1. [Additional resources](#additional-resources)

## Introduction

GuideFlow shows step-by-step guidance inside your web application, so users can learn a task without leaving the page they're on. A set of these steps is called a *flow*.

This guide shows you how to set up GuideFlow, build and publish your first flow, and use analytics to see how users interact with it.

## Set up GuideFlow

### Create an account

1. Open the invitation email from the GuideFlow onboarding team and click the sign-up link. If you didn't receive an invitation, sign up on the [GuideFlow website](https://www.example.com/).
1. Sign up with your work email address and create a password.
1. Sign in to the GuideFlow dashboard.

### Choose a delivery method

GuideFlow can add content to your application in one of two ways:

- **JavaScript embed:** You add a script to your application, and GuideFlow content appears for every user automatically. This guide uses this method.
- **Browser extension:** Each user installs an extension to see GuideFlow content.

### Add the deployment script to your application

> **Note:** Only users with the **Account Manager** role can complete this task.

GuideFlow uses a single line of JavaScript to display content in your application. Add it to a part of your application that loads on every page, such as the header, so that flows can appear anywhere.

To get the script and deploy it:

1. On the GuideFlow dashboard, click **Settings**.
1. Click **Content Deployment**.
1. In the **Ready** section, select a condition and an operator, and then enter the value that identifies your development or UAT environment.
1. In the **Production** section, select a condition and an operator, and then enter the value that identifies your production environment.
1. In the **Deployment Script** section, click **Copy**.
1. Paste the script into the `<head>` or footer of your application for each environment.
1. On the GuideFlow dashboard, click **Save**.

## Create a flow

### Open GuideFlow Studio

1. Sign in to the application where you want the flow to appear.
1. Open **GuideFlow Studio**.
1. In the content section, click **Flow**.

### Add steps

1. Enter a name for the flow.
1. Click **+ Add Step**.
1. Select the element on the page that you want the step to point to.
1. In Studio, set the step's position, appearance, and completion rule.
1. Go to the place in your application where the next step should start, and then click **+ Add Step**.
1. Repeat steps 3 through 5 for each step in the flow.
1. Click **Save Flow**.

### Customize each step

1. Enter the step's instruction text. Keep it short and start with a verb, such as "Click **Submit** to save your request."
1. Optional: Add an image or video to show the action.
1. Under **Configurations**, expand **Appearance**, and then select the tooltip style, tooltip color, and close button color.
1. Expand **Position**, and then select where the tooltip appears.
1. In the **Step Completion Rules** section, select the action that moves the user to the next step.

### Add display rules

Display rules show a step only when conditions that you set are met, such as when a user has a specific role.

1. Click **Advanced Options**.
1. Expand **Display Rules**, and then click **+ Add Rule**.
1. Set the conditions.
1. Click **Save Step**.

> **Tip:** To see the flow as users will, click **Preview**. The flow opens in a new tab. You need at least one saved step before you can preview a flow.

## Publish and test a flow

New flows start in the **Draft** stage. Send a flow to **Ready** to test it in your development environment, and then push it to production.

### Publish the flow

1. On the GuideFlow dashboard, click **Content**.
1. Click **Flows**.
1. In the **Draft** stage, select your flow, and then click **Send to ready**.
1. In the **Ready** stage, select your flow, and then click **Push to production**.

You can also use the dashboard to choose which pages a flow appears on and which users or roles see it.

### Test the flow

1. Go to the page where the flow should start.
1. Complete each step as a user would, and confirm that each step appears in the right place and moves on when it should.
1. If a step doesn't behave as expected, edit the flow, and then test it again. For help, see [Troubleshoot common issues](#troubleshoot-common-issues).

## Review flow analytics

### See results for all flows

1. On the GuideFlow dashboard, go to **Guidance analytics**.
1. Click **Flows**.

The report shows three totals:

- **Completed:** The number of times users finished the flow.
- **Failed:** The number of times the flow stopped because of a problem, such as a step that didn't appear.
- **Exited:** The number of times users left the flow. This total is the sum of the times users closed a tooltip, went to another page, or started a different flow.

### See results for one flow

1. Click **By Flow**.
1. Select a flow.

| Report | What it shows |
| --- | --- |
| Flow usage by day | How many times the flow was used each day. |
| Times flow played | How many times the flow ran, and which widget users started it from. |
| Flow completion rate | How many users started the flow, how many finished it, and how many left partway through. |
| Most exited or failed steps | Where users dropped out. Hold the pointer over a step to see how often it failed or was exited, and why. |
| Flow history | Who edited the flow, and when. |
| Flow feedback | How many users rated the flow as useful or not useful, and how many left no rating. |
| Feedback responses | How many users chose each predefined feedback response. |
| Feedback comments | The comments users wrote, if any. |

## Troubleshoot common issues

### The flow can't find the element for the next step

**Possible causes:**

- The flow was created in a development or UAT environment and is running in production. Element IDs often differ between environments.
- The application changed, and the element is gone or has moved.
- The page has several similar elements, and GuideFlow can't tell which one to use.

**To fix it:**

- Create flows in the environment where they'll run, usually production.
- Edit the flow and select the element again. For instructions, see "Reselect elements to manage UI changes" in the GuideFlow Help Center.
- If the page has several similar elements, identify the right one with a CSS selector.

### Steps don't appear or behave correctly

Symptoms include the following:

- The flow doesn't start.
- The flow doesn't move to the next step after the user clicks the element.
- A tooltip appears in the wrong place.
- The flow skips a step.

**Possible causes:**

- The step's conditions are wrong, or the step is optional and its conditions don't match.
- The rule that shows the step runs before the page finishes loading. For example, if a step uses the **On click of selected element** rule but the element hasn't loaded yet, the step doesn't appear.
- The application changed, and GuideFlow can't find the element selected when the flow was created.
- The step needs a CSS selector instead of a simple element selection.
- The flow was created in a non-production environment and is running in production.

**To fix it**, work through these checks in order:

1. **Select the element again.** Edit the failing step and reselect its target element.
1. **Add a CSS selector.** If reselecting doesn't help, add a CSS selector to the step. To learn how, see "Find the CSS selector of an element" in the GuideFlow Help Center.
1. **Check the step conditions.** Make sure the conditions for the failing step are set correctly. If the page loads slowly, try the **On page refresh** rule instead of **On click of selected element**.
1. **Compare environments.** Make sure the environment where you created the flow matches production. Element attributes can differ between UAT and production.
1. **Check element IDs.** If you created the flow in UAT and your account is set to trust element IDs, confirm that the IDs match in both environments.
1. **Start the flow on a global element.** The **Always start a flow from step 1** setting only works when the first step points to an element that appears on every page, such as the main navigation bar.

### Users leave partway through a flow

**Possible cause:** The flow has too many steps, or the instructions are unclear.

**To fix it:** Remove steps that users don't need, and rewrite each instruction as a single, specific action. Use the **Most exited or failed steps** report to find where users leave.

## Additional resources

- [GuideFlow Knowledge Base](https://support.example.com/)
- [GuideFlow Blog](https://www.example.com/blog/)
