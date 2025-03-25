# User Guide: 
# Getting Started with Whatfix on Web

### Table of Contents
1. [Introduction](#introduction)
2. [Setting Up Whatfix](#setting-up-whatfix)
3. [Creating and Configuring Flows](#creating-and-configuring-flows)
4. [Deploying Flows](#deploying-flows)
5. [Analyzing Flow Performance](#analyzing-flow-performance)
6. [Troubleshooting Common Issues](#troubleshooting-common-issues)
7. [Additional Resources](#additional-resources)

---

### Introduction
Whatfix allows organizations to deliver contextual, in-app guidance to users. This article provides an overview of how to use Whatfix to create effective onboarding flows that help new users get familiar with your product quickly and efficiently.

---

### Setting Up Whatfix

#### Step 1: Creating an Account
1. The Whatfix onboarding team will send you an invitation link to sign up. Alternatively, you can visit the [Whatfix website](https://www.whatfix.com/) to begin the sign-up process.
2. Sign up using your work email address and create a secure password.
3. After creating an account, log in to your Whatfix dashboard.

#### Step 2: Choose a Delivery Method
Whatfix content can be deployed to your application using one of the following methods:
- **JS Embed**
- **Browser Extension**

> **Note**: For this guide, we will be using the **JS Embed** method.

#### Step 3: Use JavaScript Code to Display Whatfix Content
> **Note**: Only an **Account Manager** can perform this task.

Whatfix requires a single line of JavaScript code to display the content and widgets within your application. This code needs to be inserted into the header of your application so that the content can be accessed from every page.

To obtain and deploy the JavaScript code, follow these steps:

1. On the **Whatfix Guidance dashboard**, click **Settings**.
2. Click **Content Deployment**.
3. Under the **Ready** section:
   - Select the appropriate condition and operator.
   - Enter the value for your **Development** or **UAT** environment.
4. Under the **Production** section:
   - Select the appropriate condition and operator.
   - Enter the value for your **Production** environment.
5. Under the **Deployment Script** section, click **Copy** to copy the script provided.
   
   > **Info**: This script must be inserted in the `<head>` or `<footer>` of your application instance (either Development or Production) for the Whatfix content to be displayed on every page.
   
6. Click **Save** to confirm the deployment.

---

### Creating and Configuring Flows

#### Step 1: Launch Whatfix Studio
1. Log in to the application where you want to create content, and then launch the **Whatfix Studio**.
2. Click **Flow** under the content section.

#### Step 2: Adding Steps to Your Flow
1. Enter the name of the Flow.
2. Click on **+ Add Step**.
3. Use Studio to add configurations like position, appearance, and step completion rules.
4. Go to where you want to start the next step and click **+Add Step** on the Studio.
5. Repeat steps 2 to 4 to add additional steps.
6. Click **Save Flow**.

#### Step 3: Customizing the Flow
1. Add text instructions for each step, ensuring they are clear and concise.
2. Optionally, include images or videos to explain each action further.
3. Customize the flow’s appearance, such as the colors, animations, or step timings.
4. Under **CONFIGURATIONS**, expand **Appearance**. Make the following configurations:
   - Select a Tool tip appearance.
   - Select the tip Color.
   - Select the Close (X) color.
5. Expand **Position** and select the desired position of the tooltip.
6. Under the **Step Completion Rules** section, select the desired rule.

> **Note**: Display Rules enable you to configure Flows to display the tooltip only when pre-determined conditions are met.

Use the following steps to add Display Rules to Flow steps:
   1. Click **ADVANCED OPTIONS**.
   2. Expand the **Display Rules** section and then click **+ Add Rule**. Display Rules enable you to configure Flows to display the tooltip only when pre-determined conditions are met.
   3. Set the desired conditions. 
   4. Click **Save Step**.

> **Note**: Click **Preview** to preview the Flow during the Flow creation on Studio. The Flow opens in a new tab and displays the steps that are created on the application. You must create and save at least one step to enable **Preview**.

---

### Deploying Flows

#### Step 1: Publishing the Flow
1. Once on the Whatfix Guidance dashboard, click **Content**.
2. Click **Flows**.
3. In the **Draft** stage, select your Flow and click **Send to ready**.
4. Go to the **Ready** stage and click on **Push to production**.

 > **Info**: Within the Whatfix Dashboard you can choose the pages where you want the flow to be deployed, set user conditions, and target specific user roles.

#### Step 2: Testing the Flow
1. After publishing, test the flow by navigating to the target page and ensuring that the flow is triggered correctly.
2. Make any necessary adjustments to the flow based on your test results.

---

### Analyzing Flow Performance

#### Step 1: Accessing Analytics
1. From the Whatfix Guidance dashboard, navigate to the **Guidance analytics** section.
2. Click **Flows**.
4. View key reports such as:
   - **Completed**: How many users completed the Flow.
   - **Failed**: Number of times the Flow failed and users could not complete it. For example, broken Flow, a Flow step does not display, and more.
   - **Exited**: Number of times users failed to complete the Flow due to their actions. The exit count is always equal to the sum of closed via tooltip, navigated away, and Flow transitions. i.e., **Exited = Close via tooltip + Navigated away + Flow transition**.

#### Step 2: Analtyics by Flow
1. Click **By Flow**
2. Select the Flow you want to analyze.
3. View key reports such as:

| **Report Name**              | **Description**                                                                                         |
|------------------------------|---------------------------------------------------------------------------------------------------------|
| Flow Usage by Day            | The chart displays the number of times that Flow was used each day.                                       |
| No. of Times Flow Played     | The chart shows the number of times the Flow was run and also the widget used to play the flow.          |
| Flow Completion Rate         | The chart shows how many started the Flow and completed it, as well as those who could not complete it and dropped out in between. |
| Most Exited or Failed Steps  | This section shows the dropouts at each step of the Flow. If you hover the cursor over each step, the failure can be analyzed by how many times the steps weren't successful, how many times the steps were exited, and the reasons for exit. |
| Flow History                 | The Flow History section shows who edited the Flow and when.                                             |
| Flow Feedback                | The Flow Feedback section shows how many users found the Flow useful compared to those who didn't find it useful and the users who gave no feedback. |
| Feedback Responses           | This section shows the pre-defined feedback responses recorded for the Flow. Hovering the cursor over each response displays the number of users who have selected those responses. |
| Feedback Comments            | At the end of the page, Feedback Comments (if any) can be viewed verbatim.                              |

---

### Troubleshooting Common Issues

#### Issue 1: Flow could not detect the element for the next step
**Cause**:
  - Flow may have been created using the elements captured in a non-production (developer/UAT) environment, and an attempt is made to play the Flow in the Production environment. Element IDs are different for UAT and Production environments.
  - The underlying application has changed, or the specific element is missing.
  - If there are multiple similar elements on the application, Whatfix fails to recognize the right element.

**Solution**:
  - Ensure that the Flow is created in the Production environment.
  - Edit the Flow and reselect the element. See, Reselect Elements to manage UI changes.
  - In case of multiple similar elements, use CSS selectors to identify the right element.

#### Issue 2: Flow Steps Not Displaying Correctly
The Flow fails to work correctly when displayed to the end users. The following are some instances of a Flow breaking:
- The Flow fails to start.
- The Flow fails to move to the next step even after clicking on the element.
- The Flow Tooltip appears in an incorrect position.
- The Flow skips a step.

**Cause**:
- The step conditions for the Flow may be incorrect or the step may be optional and the conditions don't match.
   - For example, one of the reasons could be that the step condition is being evaluated while the page is still loading. So if you are using the On click of selected element visibility rule, try switching to the On-page refresh rule.
- Something may have changed in the underlying application, and Whatfix is unable to find the element that was selected when the flow was created.
- Instead of simple element selection, a CSS Selector may be needed to ensure that the Flow step runs correctly.
- The Flow may have been created in a non-production environment but is being run in the production environment.
- The application may be taking time to load and the visibility rule that determines the content display may not be optimized. For example, the rule may be set to be triggered by the On-click of selected element because the page has not refreshed, the element that is supposed to trigger the next step has not yet been displayed, and thus, the step does not display.

**Solution**:
If a step in your Flow is not functioning as expected, follow these steps to troubleshoot the issue:  

1. Reselect the Element  
   - Navigate to the step that is failing and attempt to reselect the target element.  
   - For detailed instructions, refer to [Reselect Elements to Manage UI Changes](#).  

2. Use a CSS Selector  
   - If element reselection does not resolve the issue, consider adding a CSS selector.  
   - For guidance on finding a CSS selector, see [How to Find the CSS Selector of an Element Using Whatfix Studio](#).  

3. Verify Step Conditions  
   - Ensure that the step conditions for the failed step are correctly configured.  

4. Check Environment Consistency  
   - Confirm that the Flow was created in an environment identical to the production environment.  
   - Element attributes may differ between UAT and production, causing unexpected behavior.  

5. Validate Element IDs  
   - If the Flow was created in a UAT environment and your account is configured to trust element IDs, verify that the IDs are consistent across both environments.  

6. Ensure the First Step Uses a Global Element  
   - The **Always Start a Flow from Step 1** feature functions only when the first step is placed on a global element—one that is present across multiple pages.  
   - If the first step is not on a global element, enabling this feature may cause the Flow to break.  
   - Ensure that the first step is placed on a global element for seamless execution.  

#### Issue 3: Users Dropping Off Mid-Flow
**Cause**:
- Over-complicated steps or unclear instructions.

**Solution**:
- Simplify the flow by reducing the number of steps and making the instructions more straightforward.

---

### Additional Resources
- [Whatfix Knowledge Base](https://support.whatfix.com/)
- [Whatfix Blog](https://www.whatfix.com/blog/)
- [Whatfix Tutorials](link)

---

### Conclusion
Whatfix provides a powerful platform for creating in-app guidance to help users navigate your application more effectively. By following this guide, you’ll be able to set up, deploy, and analyze flows that will streamline your users’ experience. For more advanced configurations and troubleshooting, explore our resources and support documentation.
