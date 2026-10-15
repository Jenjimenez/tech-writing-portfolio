---
last_updated: 2026-10-14
---
# Knowledge Base: Creating Onboarding Flows

> **About this sample**
>
> - **Type:** Task-based knowledge base article
> - **Audience:** Content creators building their first onboarding flow
> - **My role:** Wrote the article to support customers during platform rollout
>
> This sample is based on documentation I wrote for a digital adoption platform. Product names, URLs, and identifiers have been replaced with a fictional product, *GuideFlow*, to protect client and employer confidentiality.

An onboarding flow is a short, interactive walkthrough that shows new users how to complete key tasks in your application. This article explains how to build one in GuideFlow, how to keep it effective, and what to check if it doesn't work as expected.

## Table of contents

1. [What a flow is](#what-a-flow-is)
1. [Create an onboarding flow](#create-an-onboarding-flow)
1. [Best practices](#best-practices)
1. [Troubleshooting](#troubleshooting)
1. [Additional resources](#additional-resources)

## What a flow is

A *flow* is a series of steps that appear on top of your application and guide a user through a task, one action at a time. Because the guidance appears where the user is working, they don't need to leave the page to read separate documentation.

Each step uses one of these elements:

- **Tooltip:** A small message that points to a specific button, field, or link.
- **Spotlight:** A highlight that dims the rest of the page to draw attention to one area.
- **Checklist:** A list of tasks that users can complete in any order.

## Create an onboarding flow

1. Open the **GuideFlow Editor**.
1. Click **Interactive Walkthrough**.
1. Click **+ Add Step**, and then select the element on the page that the step should point to.
1. Choose **Tooltip** to explain an element, or **Spotlight** to highlight an area of the page.
1. Enter the step's instruction. Start with a verb and describe one action, such as "Click **New project** to create your first project."
1. Repeat steps 3 through 5 for each action in the task.
1. Click **Save**.

For detailed instructions, including display rules and deployment, see [User Guide: Getting Started with GuideFlow on Web](../User_Guides/web-user-guide.md).

## Best practices

### Keep flows short

Limit each flow to three to five actions. If a task needs more, split it into separate flows so that users can finish each one without losing track.

### Show, don't just tell

Add arrows, highlights, or short videos where text alone could be unclear, such as when an element is easy to miss.

### Show flows at the right moment

Start a flow when the user needs it, such as right after they sign up or when they open a complex feature for the first time. A flow that appears at the wrong time is easy to dismiss and forget.

## Troubleshooting

### The flow doesn't start

**Cause:** The flow's trigger or conditions don't match what the user is doing.

**Solution:** Check that the flow uses the correct trigger, and that its conditions, such as a page load or a click on a specific element, match the action that should start it.

### Steps appear in the wrong place or don't appear

**Cause:** CSS or JavaScript on the page conflicts with the flow, or the step runs before the element it points to has loaded.

**Solution:** Check the page's CSS and JavaScript for conflicts, and adjust the timing or placement of the step. For more troubleshooting steps, see [Troubleshoot common issues](../User_Guides/web-user-guide.md#troubleshoot-common-issues).

## Additional resources

- [GuideFlow Help Center](https://help.example.com/)
- [GuideFlow Blog](https://www.example.com/blog/)
