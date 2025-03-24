# Knowledge Base Article: How to Use Whatfix for Onboarding New Users

_Last Edit: 3/2025_

## Overview
This article explains how to use Whatfix to create onboarding experiences for new users within your application. Onboarding helps new users understand how to navigate and utilize your product effectively. By using Whatfix, you can deliver in-app guidance that is contextually relevant, interactive, and easily accessible.

---

## Table of Contents
1. [Prerequisites](#prerequisites)
2. [Creating a Whatfix Flow](#creating-a-whatfix-flow)
3. [Configuring Flow Triggers](#configuring-flow-triggers)
4. [Testing and Deploying Your Flow](#testing-and-deploying-your-flow)
5. [Best Practices for Onboarding](#best-practices-for-onboarding)
6. [Troubleshooting](#troubleshooting)
7. [Further Resources](#further-resources)

---

## Prerequisites
Before you begin creating onboarding experiences with Whatfix, ensure you have:
- A Whatfix account with appropriate permissions.
- Access to the web application where you want to implement onboarding.
- A basic understanding of Whatfix Flows and the Whatfix Editor.

---

## Creating a Whatfix Flow

### Step 1: Log in to Whatfix
1. Open the Whatfix application and log in with your credentials.
2. Navigate to the **Editor** section from the main dashboard.

### Step 2: Create a New Flow
1. In the **Editor** section, click on **Create New Flow**.
2. Choose the **Flow Type** – for onboarding, select **Interactive Walkthrough**.
3. Name your flow (e.g., "Onboarding: Getting Started").

### Step 3: Add Steps to Your Flow
1. In the Whatfix editor, click **Add Step** and select the type of element to guide (e.g., buttons, fields, text boxes).
2. Use **Tooltips** and **Spotlights** to focus on key elements.
3. Provide clear instructions or tips for each step. Keep the text concise and actionable.

### Step 4: Customize Your Flow
1. **Adjust step timing**: Choose whether to delay each step for a better user experience.
2. **Add multimedia**: Enhance your flow with images or videos to further guide users.
3. **Select your target audience**: Choose user segments or roles to customize the flow.

---

## Configuring Flow Triggers

### Step 1: Choose the Trigger Type
1. Navigate to the **Triggers** section in the flow editor.
2. Select from various triggers:
   - **Page Load**: Trigger the flow when a user visits a specific page.
   - **Element Interaction**: Start the flow when a user interacts with a specific element (e.g., clicks a button).
   - **URL Path**: Set the flow to start when a user visits a certain URL.

### Step 2: Set Conditions
- You can configure conditions to ensure the flow triggers at the right time. For instance, you might only show onboarding steps after a user logs in for the first time.

---

## Testing and Deploying Your Flow

### Step 1: Preview the Flow
1. Use the **Preview** feature to test the flow within the Whatfix editor.
2. Ensure that each step behaves as expected, and make adjustments as necessary.

### Step 2: Deploy the Flow
1. Once you're satisfied with the flow, click **Publish** to deploy it.
2. You can choose to deploy it on specific pages or for specific user groups.

### Step 3: Monitor Performance
1. After deployment, monitor user interaction through the **Analytics** section in Whatfix.
2. Track how many users complete the flow and analyze areas where users may drop off.

---

## Best Practices for Onboarding

1. **Keep It Simple**: Focus on the most important tasks users need to accomplish. Don't overwhelm them with too many steps.
2. **Use Visuals**: Use screen annotations, arrows, and highlights to guide users through each step.
3. **Be Concise**: Use short, clear instructions. Avoid lengthy explanations to maintain engagement.
4. **Interactive Elements**: Engage users with interactive elements such as quizzes or checklists to encourage active participation.
5. **Timing**: Trigger flows at key points in the user journey (e.g., immediately after sign-up or after a user completes a key action).

---

## Troubleshooting

### Issue 1: Flow Not Triggering
- **Cause**: Incorrect trigger settings or wrong element selection.
- **Solution**: Double-check the trigger conditions and ensure they match the intended interaction or page.

### Issue 2: Steps Not Appearing Correctly
- **Cause**: Incorrect step timings or z-index conflicts with other page elements.
- **Solution**: Adjust the step timing and review any potential conflicts with other on-page elements.

### Issue 3: User Dropped Off Mid-Flow
- **Cause**: A complicated step or interruption in the flow.
- **Solution**: Review the analytics to identify the drop-off point and simplify or clarify that section.

---

## Further Resources
- [Whatfix Knowledge Base](https://help.whatfix.com/)
- [Whatfix Blog for Product Updates and Tips](https://www.whatfix.com/blog/)
- [Video Tutorial: Creating Interactive Walkthroughs](link)
