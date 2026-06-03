# TCP Author Onboarding and Messaging Playbook

## Intro and purpose

This page provides standardized onboarding message templates and information for the Hands-on Technical Content Production (TCP) team. The goal is to create a consistent, professional, and supportive author experience across all lab types.

These templates are designed to be high-level and flexible.

## Template best practices

- **Personalize content:** Add the author’s name, lab details, and relevant links.
- **Use a friendly tone:** Keep communication supportive and encouraging.
- **Keep content concise:** Avoid long paragraphs. Use lists for readability.
- **Be proactive:** Send follow-ups and check in if progress stalls.

## Handy resources

- Hands-on content standards
- Slides standards and guidelines
- Video content standards
- Design services
- Design Request Form
- TCP messages workflow diagram
- TCP high-level messages and workflow for all lab types

## Publication message template

Use the publication template when notifying the author that their content has published. You can share the external link upon publication. See [External link structure examples](#external-link-structure-examples).

```text
<@author>, thank you for all your hard work! The lab is now published! 🎉

Here’s the information for your lab:

Published Lab

Lab: The lab-title w/ www hyperlink embedded (external link)
Feedback Sheet: Feedback sheet URL
CC: <@PC>

Action Items

I’ve noted a few suggestions you can keep in mind for your next lab. You can find them in our feedback sheet under Criticality: Suggested Fix and Criticality: Future Fix.
```

## External link structure examples

Upon publication, external-facing links are not immediately generated. The following patterns allow you to share links with authors upon publication. Some discrepancies are noted below.

### Exceptions to note

When a lab title has punctuation, the punctuation is excluded from the URL. This includes:

- Periods (`.`)
- Parentheses (`()`)
- Dashes (`-`)
- Colons (`:`)
- Ampersands (`&`)

<br>

# General templates for all lab types

## New author

Connect with a new author to share resources and schedule an onboarding call to walk through our tooling.

```text
Hi @{author}, nice to meet you!

I’d like to set up an onboarding call to walk through our tooling and answer any questions you may have.

My availability is as follows {start_time}–{end_time} {timezone}, Monday–Friday.

Or feel free to choose a slot on my calendar: {calendar_link}.

Before the call, please review the following resources:

- Hands-on content standards
- [INSERT SPECIFIC LAB TYPE STANDARDS]

I look forward to working with you!
```

## New author: Post-onboarding call

After the initial onboarding call, share resources, expectations, and next steps.

```text
Hi @{author}, it was great meeting with you! Here are the resources to help you get started:

- Hands-on content standards
- Example Labs:
  - [add relevant links]
- [Relevant documentation link]

I’ll check in with you next week to see how things are going. In the meantime, let me know if you need any help!
```

## Returning author

If the author has previously built a lab of this type, you may skip the tooling walkthrough. Focus instead on resources and project setup, if necessary.

```text
Hi @{author}, welcome back! Since you’re already familiar with the lab environment, here are some resources for your reference during this project:

- Hands-on content standards
- [Link specific lab type standards]

If you’d like examples or additional resources, let me know and I’ll share them. I look forward to working with you!
```

## Check-in message

Check in with authors, especially if progress has stalled.

```text
Hi @{author}, I hope you’re doing well!

I wanted to check in on your lab progress. If you need help, please let me know!
```

<br>

# Desktop labs

## Important information to share with authors

- Restrict authors from accessing the lab when it is under review to prevent saving issues.
- Bring attention to banners authors might see when a lab is not published. Let them know they can still work on the lab.
- Remind authors that we have a single slide deck to be used for all content.

## TCP checklist

- **Outline/instruction alignment**
  - Ensure the lab instructions cover all key objectives from the Outline.
- **Environment setup**
  - Inspect the `.zip` files to confirm no credentials or proxy information remain and that Springtail services are not commented out.
- **Checklist compliance**
  - Check that the author completed all items on the Desktop Labs Checklist.
- **Testing**
  - Test the lab as a learner.

## Templates

### New Desktop Labs author

```text
Hi <@author>, welcome to Desktop Labs! I’m excited to be working with you. I’ll be assisting you throughout the production of this lab.

To begin, I’ll share a couple of resources and sample labs to help you get familiar with Pluralsight’s hands-on content standards and the lab tooling. Once you’ve had a chance to review, we can schedule a Zoom call to walk through the tooling and answer any questions you may have.

Things to keep in mind:

- The lab environment for learners does not have internet access.
- If you need a GitHub repo to host files for learners, you'll need to use one of ours. Let me know and I can create one for you.

Review prior to introduction call:

- Hands-on content standards
- Desktop labs standards

Action items:

- Provide a GitHub username so I can give you access to the Terrarium, the template you’ll use to configure the lab environment.
- Schedule an onboarding call. Send a time that works for you, or choose a slot on my calendar: {calendar_link}.

Here is my availability: [list times and time zone].

Please feel free to reach out with any questions in the meantime. My office hours are Monday–Friday, [insert hours and timezone].
```

### Returning Desktop Labs author

```text
Hi <@author>, I’m excited to be working with you again!

Please provide your GitHub repository username if you’ll need to host resources for this lab. If you have any questions or need assistance throughout the lab production, don’t hesitate to reach out.

Resources:

- Desktop labs checklist
- Desktop lab standards
```

<br>

# Code labs

## Important information to share with authors

- The learner environment does **not** have internet access. Ensure that all required dependencies are included in the lab environment.
- Before requesting a review, exit the lab, as it will default to read-only mode for other users.
- Before TCP review, test the lab using Preview mode to help avoid delays in the review process.

## TCP checklist

- **Outline/instruction alignment**
  - Ensure the lab instructions cover all key objectives from the Outline.
- **Environment setup**
  - Correct stack is selected.
  - All required dependencies are included.
- **Testing**
  - Test the lab as a learner using the **Preview** button.

## Templates

### New Code Labs author

```text
Hi @{author}, it’s great to meet you! I’d like to set up an onboarding call to walk through the Code Labs tooling and answer your questions.

I’m generally available <insert availability>. Let me know a time that works for you, or choose a slot on my calendar: <calendar_link>.

Before the call, please review the following resources:

- Universal standards
- Code lab standards
- Code lab onboarding doc

I look forward to working with you!
```

### Code Labs post-onboarding call

```text
Hi @{author}, it was great meeting with you! Here are the resources we discussed:

- Hands-on content standards
- Example Code Labs:
  - [add relevant links]
- Guided pattern doc (only for Developer labs)
- Semgrep documentation [if applicable]

I’ll check in with you next week to see how things are going. In the meantime, let me know if you need any help!
```

### Returning Code Labs author

```text
Hi @{author}, welcome back! Since you’re already familiar with the Code Labs environment, here are the key resources for this project:

- Universal Standards
- Code Lab Standards

If you’d like examples or additional resources, let me know and I’ll share them.

I look forward to working with you!
```

## Resources

- Guided labs pattern doc
- Semgrep documentation: a lightweight validation option
- Code lab onboarding doc

<br>

# Hands-on cloud labs

## Important information to share with authors

- Do **not** access the lab while it is under review, as this can cause saving issues.
- When previewing your lab, you may see warning banners if the lab is not yet published. You can ignore these messages, as the lab will still function correctly. For example:
  - “Sorry, but you do not have access to this content.”
  - “This lab has been retired.”
- Please use the most up-to-date slide deck.

## TCP checklist

- **Outline/instruction alignment**
  - Ensure the lab instructions cover all key objectives from the Outline.
- **Slides/lab diagram**
  - Slides or lab diagram must be reviewed before recording the intro video.
  - Must include the Pluralsight watermark.
- **Learning objectives**
  - Include 2 to 5 objectives based on those listed in the lab Outline.
  - Keep objectives short and written in full sentences.
  - Objectives should not be specific step-by-step instructions or include code.
- **Guide**
  - Steps must be numbered, short, and action oriented.
- **Environment**
  - Include a non-empty CloudFormation template. This only applies to AWS labs.
  - Include at least one managed AMI resource.
- **Video**
  - Keep each video under 12 minutes.
- **Testing**
  - Test the lab as a learner using the **Preview Lab** link.
  - Follow AWS sandbox limitations.

## Templates

### New Hands-on Cloud Labs author

```text
Hi {@author}, nice to meet you!

Before you get started, please note the following:

Important callouts:

- Do not access the lab when under review, as this can cause saving issues.
- When previewing your lab, you may see warning banners if the lab is not yet published. You can ignore these messages, as the lab will still function correctly. For example:
  - “Sorry, but you do not have access to this content.”
  - “This lab has been retired.”
- Please use the most up-to-date slide deck.

Standards and expectations:

When creating slides, videos, and Guide, please follow these guidelines:

- Hands-on Universal Standards
- Hands-on Cloud Labs Standards

Additional guidance:

- Each Objective description should be one to three sentences and can be a bulleted list. They are not to be step-by-step instructions.
- Your Lab Guide should be all of the written instructions from your video, provided as short, numbered steps.

Process guidelines:

- Please post your slide here before recording the Introductory video so we can review it.
- When creating your lab environment, be sure to follow the correct limitations: AWS sandbox, Azure sandbox, or GCP cloud sandbox.
- Make sure to test your lab environment early on. Use a non-empty AWS CloudFormation template and PS-managed AMIs only.

Before requesting a review:

Before asking for a review, make sure to test your lab as a learner by clicking **Environment** > **Start Instance** > **Preview Lab**. The **Preview Lab** link is on the right side toward the bottom of the tooling.

Messaging in Slack:

Please reach out with any questions and make sure to @ me so that I’m notified!

Excited to work with you!

Thanks @PC!
```

### Existing Hands-on Cloud Lab update

```text
Hi @Author, I’m looking forward to working with you on this lab!

Before you get started, please review the following:

- This is an existing lab that will be updated in the original shell.
- Do not modify the existing lab until I LIM it, which will make it unavailable to learners.
- Back up the existing lab locally, and first get things working in your own dev test lab shell.

The following applies to an Azure lab:

- To record the videos with a properly named Resource group, temporarily change your dev shell's name to match the lab's, adding in a hyphen to avoid a name conflict.

Once things are working in your dev shell, @ me and I’ll LIM the existing lab so you can update it.

When creating your slides, videos, and Guide, please follow these guidelines:

- Hands-on content standards
- Hands-on cloud labs standards

Some callouts from these standards:

- Each Objective description should be one to three sentences and can be a bulleted list. They are not to be step-by-step instructions.
- Your Guide should be all of the written instructions from your video, provided as short, numbered steps.

Some important tips to follow:

- Please post your slide here before recording the Intro video so I can review it.
- When creating your lab environment, be sure to follow the correct limitations: AWS sandbox, Azure sandbox, or GCP cloud sandbox.
- Make sure to test your lab environment early on. Use a non-empty AWS CloudFormation template, and use PS-managed AMIs only.

Before asking for a review, make sure to test your lab as a learner by clicking **Environment** > **Start Instance** > **Preview Lab**. The **Preview Lab** link is on the right side toward the bottom of the tooling.

Messaging in Slack:

- When messaging in our lab channel, make sure to @ me so that I’m notified.

Please feel free to reach out with any questions. I’ll check in with you in a few business days to make sure everything is going smoothly!
```

### Starter info for selected Hands-on Cloud Labs

```text
Hi @{author}, looking forward to the lab! Here's the starter info:

Standards to follow:

- Universal standards
- Cloud lab standards

Some exceptions:

- Don't have any videos.
- There won't be any screenshots.
- Do explain things well, including having explicit expected results from commands so learners know they're on the right track.
- Follow all feedback from past labs of this type.

Some callouts from our standards:

- Adhere to the outline for this lab.
- Each Objective's description should be 1 to 3 sentences and can be a bulleted list. They are not to be specific step-by-step instructions.
- All titles, including the Objective titles, section headings, and Lab Diagram title, are to be in sentence case.
- Use the recently updated slide deck.

Some important tips to follow:

- Please post your slide here for the Lab Diagram so I can review it.
- Use recent, stable operating systems, such as Ubuntu 24 or Amazon Linux 2023, and the latest stable versions explicitly for anything else you install.
- When creating your lab environment, be sure to follow the correct limitations: AWS sandbox.
- Use a non-empty AWS CloudFormation template, and use PS-managed AMIs only.

Before asking for a review:

Make sure to test your lab as a learner by clicking **Environment** > **Start Instance** > **Preview Lab**. The **Preview Lab** link is on the right side toward the bottom of the tooling.

Messaging in Slack:

- When sending me a message in this channel, make sure to @ me so that I’m notified.

Let me know if you need a repo, too!

Please feel free to reach out with any questions!
```

## Onboarding new authors

Use **Author your hands-on cloud lab** as a reference for your tooling walkthrough.

```text
Hi @{author}, so glad to have you join us! Here’s some info to get you started:

For slides, videos, and Lab Guide, please follow these guidelines:

- Hands-on Universal Standards
- Hands-on Cloud Labs Standards

Some callouts from these standards:

- Each Objective description should be 1-3 sentences and can be a bulleted list. They should not be specific step-by-step instructions.
- Your Lab Guide should be all of the written instructions from your video, provided as short, numbered steps.

Some important tips to follow:

- Please post your slide here before recording the Introductory video so we can review it.
- When creating your lab environment, be sure to follow the correct limitations: AWS sandbox or Azure sandbox.
- Make sure to test your lab environment early on. Use a non-empty AWS CloudFormation template and PS-managed AMIs only.

Before asking for a review, make sure to test your lab as a learner by clicking **Environment** > **Start Instance** > **Preview Lab**. The **Preview Lab** link is on the right side toward the bottom of the tooling.

Messaging in Slack:

Please reach out with any questions and make sure to @ me so that I’m notified!

Onboarding call action item:

I'd love to set up a walkthrough call. On the call, we can walk through the tooling and answer any questions you may have.

Let me know what times work for you and I’ll send you an invite!
```

### Post-onboarding call follow-up

```text
Hi @{author}, it was so nice chatting with you today! Please let us know if you need anymore information.

Environment considerations:

- Please remember to always shut down the instance when not testing or using the environment.
- Click **Stop Instance** under the **Environment** tab.
- Please ensure you save and close the Labs Builder window before notifying your TCP that any content is ready for review in the Lab Shell. If you do not save and close the window, work on either side could be lost due to caching.

Below are some points and links we covered in our meeting.

Author Kit Links:

- Slides standards and guidelines, including brand guidelines
- Author your hands-on lab
- Video content standards
- Design Services Support

Workflow:

1. Start with your lab diagram, and send it in chat to get it reviewed.
2. Move on to your intro, upload it to the lab, and @ me for review.
3. Upload your solution video and @ me for review.
4. Use your solution video as a reference for your Guide.

Video content:

- The Pluralsight logo is added automatically. Remove it when recording to avoid issues.
- Do not exceed 12 minutes per video.
- Break up your videos however you find best.

Branding notes:

- Use only Pluralsight Author Brand colors in your content. The primary colors should be the dominant colors in your slides and used before any tint.
- Downloads page
- You may notice that we are currently transitioning to new branding. Since you are going to be downloading the newest template, please follow the new branding, not the branding seen in the example I included.

Example lab for your reference:

- Build a Three-Tier Network VPC from Scratch in AWS
```

## Resources

- Slides standards and guidelines
- Video content standards
- Hands-on cloud lab standards

<br>

# AI-generated labs

## Important points

- Check that solution code includes only code requested by the task.
- Check for second person and active voice.
- Add approved AI disclosure language in Forge-generated labs.

## TCP checklist

- **Outline/instruction alignment**
  - Ensure the lab instructions cover all key objectives from the Outline.
- **Relevance and redundancy**
  - Avoid repetition or filler.
- **Feedback, solution, and validation**
  - Feedback is constructive.
  - Solution code only contains changes requested by the task.
  - Validation is passing with properly marked solutions.
- **Mark as AI content**
  - Ensure author is set to Pluralsight AI Lab.
  - Identifier: `41fa1e02-2087-4c41-a192-13dda105f026`
  - Add AI disclosure at the end of the first step for Forge-generated labs only.

## Review process

Follow these steps to review an AI-generated lab:

1. Run through the lab in Preview mode.
2. Run validation once without changes before answering tasks to confirm incorrect answers fail properly.
3. Check failed feedback to ensure it is constructive and not confusing.
4. Confirm task solutions are included.
5. Note mismatches or unclear validations for AI prompt improvements.
6. Before making content improvements, share this feedback with the author.

> **Note:** Share feedback with the author before making content improvements because authors often go back to the tooling and re-upload the lab, which can wipe out content changes and improvements.

<br>

# Resources

## Desktop labs

- Desktop Labs Checklist

## Code labs

- Code Labs Onboarding Guide

## Forge AI-generated labs

- Lab Test tool: Github Guide Link

<br>

# Suggested tools

You can use text-expansion tools to add templates more easily.

- Typinator for Mac
- AutoHotkey for Windows
- If neither of those works for you, there are alternatives for Windows, MacOS, and Linux: `https://alternativeto.net/category/productivity/text-expander/`
