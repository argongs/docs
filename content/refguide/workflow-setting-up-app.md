---
title: "Adding a Workflow to an Existing App: Setting Up the Basics"
parent: "workflows"
description: "Describes how to use Workflow Commons in an existing app in Mendix Studio Pro."
menu_order: 55
tags: ["studio pro", "workflow", "task", "onboarding"]
#If moving or renaming this doc file, implement a temporary redirect and let the respective team know they should update the URL in the product. See Mapping to Products for more details.
---

## 1 Introduction

**Workflow Commons** is a workflow-specific module that contains a lot of preconfigured documents, such as pages, snippets, page templates, microflows. You can download the [Workflow Commons module](https://marketplace.mendix.com/link/component/117066) from the Mendix Marketplace and integrate it in your app, however, this requires some preparation first. 

Before adding the Workflow Commons module to your app, make sure you have completed the following:

* Upgrade your application to Mendix 9
* Install Atlas 3 from the Mendix Marketplace, as Workflow Commons depends on it 
* As a result of installing Atlas 3, your app should contain the following modules that Workflow Commons depends on: Atlas Core, Atlas Web Content, and Data Widgets

## 2 Preparing Your App

By default, Workflow Commons will integrate with [Mendix SSO](https://marketplace.mendix.com/link/component/117212) that allows you to invite and manage users and roles in the [Manage App Users page](/developerportal/collaborate/general-settings) in the Developer Portal. You can download Mendix SSO from the Mendix Marketplace. If you do not have Mendix SSO installed, you will see some consistency errors after installing Workflow Commons. After adding the Mendix SSO module, the consistency errors caused by the installation of Workflow Commons will be gone. If you want to implement a different user authentication and user management method, you can replace the references made to Mendix SSO in Workflow Commons with the user entity of your preference.

## 3 Workflow Commons Components {#components}

The purpose of Workflow Commons is to provide you with useful pages, page templates, snippets, and microflows that can save you development time. All documents in the **Private** folder are meant for internal purposes within the module itself, but you can find a couple of useful documents that you can make use of in the **UseMe** folder.

### 3.1 Pages

There are three pages provided with the Workflow Commons module to get you and your users started with workflows. The functionality contained in these pages works out-of-the-box. Simply add these pages to the [navigation](navigation) of your app to start using them. 
You can find the following pages in Workflow Commons:

*   **DefaultWorkflowAdmin** – The default workflow admin page that a workflow administrator can use to view and manage a workflow instance. This page can be used in the **Show workflow admin page** microflow activity and button action.
*   **TaskDashboard** –  This page gives end-users an overview of their performance in your app's workflows. It contains such information as how many tasks your users have completed, how long they take on average to complete a task, and what percentage of their tasks they complete within the deadline.
*   **TaskInbox** – This page contains a handy list of all tasks that a user can interact with. **My open tasks** shows the tasks assigned to current users, **All open tasks** is a list of tasks they could pick up, **Unassigned tasks** shows all unassigned tasks, and **Completed tasks** gives an overview of all tasks that were finished.
*   **WorkflowAdminCenter** – A navigational page for workflow administrators. From here, a workflow administrator can go the the **Workflow Dashboard**, which gives them general statistics of workflows, much like the **TaskDashboard** does for users. Workflow administrators also gain access to the **Workflow Admin Center**, where they can see all the instances of specific workflows and make changes to their data or even abort workflows.
*   **WorkflowDashboard** – This page gives you workflow/task based metrics and direct access to all *Workflow* and *WorkflowUserTask* data. When you want to use the Workflow Dashboard as your only admin go-to page, add this to the navigation instead of the **WorkflowAdminCenter**. 
*   **MyInitiatedWorkflows** – A useful page for those users who initiate workflows. This page gives them an overview of all their initiated workflows. They can view the current state, task timeline and can withdraw (abort) workflows that are in progress, paused, or incompatible.

### 3.2 Page Templates

Workflow Commons contains page templates to easily get you started with building workflow-related pages. These templates are automatically suggested to you when you make a new page from either the user task or workflow properties. 
You can find the following page templates in Workflow Commons:

*   **MyInitiatedWorkflows** – This page template allows users who initiate workflows keep track of their progress. A user is also able to withdraw a workflow if it is still in progress.
*   **UserTask_Basic** – A basic template that shows a header with the task name and description, a sidebar with details about the assignee and status of the task, and a main view where input elements and buttons to complete the task are generated.
*   **UserTask_Extended** –  This page template does exactly the same as the basic user task template, but extends it by adding attachments and comments sections, as well as an activity timeline to see what has previously happened in this workflow.
*   **Workflow_Admin** – This template can be used to easily generate an overview page for a specific workflow. It contains a header with the name of the workflow, as well as an action menu for administrators. There are three tabs, **General information**, **Task details**, and **Notes and attachments**. In the **General information** tab, you see the current state of the workflow, start and end date and time, as well as the due date and potential reasons for failure. The activity timeline is displayed, and there is a section with generated input elements that allows administrators to make changes to the data in the workflow. In the **Task details** tab, you can view information on individual tasks: who worked on them and who would have been able to pick them up. Finally, the **Notes and attachments** tab provides an overview of all the notes and attachments that were added for this workflow.
*   **Workflow_TaskDashboard** – This page template can be used to generate your own **TaskDashboard**, for example, when you want to use your own metrics or add context information.
*   **Workflow_TaskInbox** – This page template can be used to generate your own ***TaskInbox*** page, for example, when you would like to add context information from your business data to this page.

### 3.3 Snippets

If you would like to customize page templates, you can do that with the help of the snippets provided by Workflow Commons. You can find them in the **Snippets** folder of the Workflow Commons module.

### 3.4 Microflows

Preconfigured microflows help you assigning user tasks, and one allows you to abort workflows.
You can find the following microflows in Workflow Commons:

*   **ACT_UserTask_AssignToMe** – Assigns a user task, which is passed as a parameter, and assigns it to the current user.
*   **ACT_UserTask_AssignToUser** – Assigns a user task to a specified user, both passed as parameters.
*   **ACT_UserTask_Unassign** – Removes the assignee from a user task, which is passed as a parameter.
*   **ACT_Workflow_Abort** – Aborts a workflow instance and all of its currently running user tasks. The workflow instance is passed in as a parameter.

## 4 Setting Up User Assignment and Security

The Workflow Commons module has two module roles for you to make use of. Users with the **User** module role will gain access to the **MyTaskDashboard** and **MyTaskInbox** pages, as well as the ability to create and change their own attachments and notes on workflows. Giving someone **Administrator** privileges allows them to explore the **WorkflowAdminCenter**, manage attachments and notes from anyone, and abort workflows.

Depending on the required user roles for your application, you may have the need to distinguish workflow administrators from regular administrators. If that is the case, follow the steps below:

1.   Make a new user role for workflow administrators.
2.   Link the user role to the **Administrator** module role in Workflow Commons.
3.   Link the user role to both the **User** and **WorkflowAdministrator** module roles in the System module.

Finally, go to the Workflows tab in your [app settings](project-settings#workflows) and select the same user entity as the one you are using in Workflow Commons. If you using Mendix SSO, set it to **MendixSSO.MendixSSOUser**. You can then use the properties of this entity to filter the users that can pick up a task in the task's user assignment property. For more information on user task properties, see [User Task](user-task).

## 5 Customizing Workflow Commons

While Workflow Commons does provide useful documents out-of-the-box, you might have the need to change the content and, for example, make pages company-specific. When doing so, we recommend that you make a copy of the document that you will be changing to a local module called **WorkflowCommonsCustomizations**, so that you do not accidentally overwrite your changes in the future when upgrading to a newer version. Feel free to also browse around in the **Private** folder of the module to discover the snippets and sub-microflows.

## 6 Workflow Best Practices

We recommend the following best practices when working with workflows:

*   When creating your workflow entity, use associations to connect to relevant information and only create attributes that are related to the current workflow instance. An example could be an **Expense** entity containing a description and amount, associated with an **ExpenseApproval** entity which has attributes for the approval state and a reason for rejection.
*   When creating a user task, add a short description of the target users to the caption of the task. An example could be **HR: Schedule onboarding training** in an employee onboarding workflow.
*   When creating a microflow for a system task, prefix it with **WF\_**, so everyone knows it is being used in a workflow.

## 7 Read More

*   [Workflows](workflows)

