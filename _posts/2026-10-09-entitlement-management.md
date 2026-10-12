---
layout: post
title: "Configure Entitlement Management in Microsoft Entra ID Governance"
date: 2026-10-12 10:00:00 +0200
categories: [Entra]
tags: [Entra ID, Identity Governance, Entitlement Management]
description: "A step-by-step guide to setting up catalogs, access packages, approvals, lifecycle settings and access removal in Entitlement Management."
---

{% assign img = '/assets/images/entitlement-management/' %}

Entitlement Management is an Identity Governance process that automates access requests, approvals, and lifecycle management for enterprise resources. It makes sure that users, both internal employees and external partners, receive only the permissions they need for their role. It also revokes access automatically when those permissions are no longer needed.

## Before you begin

Some options in this guide, such as selecting all applications in a catalog, require the Global Administrator or Identity Governance Administrator role. Microsoft Entra roles as a resource and sponsors as approvers require a Microsoft Entra ID Governance subscription.

## Step 1: Create a catalog

Go to **ID Governance** → **Entitlement management** and open **Catalogs**. Select **New catalog**.

<figure>
  <img src="{{ img | append: '01-catalog-menu.png' | relative_url }}" alt="ID Governance menu in the Microsoft Entra admin center with Entitlement management selected and the Catalogs page open">
  <figcaption>Entitlement management under ID Governance, with the Catalogs page open.</figcaption>
</figure>

Give the catalog a **Name** and a **Description**. Set **Enabled for users to request** to *Yes*. Only set **Enabled for external users to request** to *Yes* if external partners should be able to request access. In this demo, I only enable requests for internal users.

<figure>
  <img src="{{ img | append: '02-new-catalog.png' | relative_url }}" alt="New catalog form with Name and Description fields and the options for requests by internal and external users">
  <figcaption>The new catalog form with requests enabled for internal users only.</figcaption>
</figure>

## Step 2: Add resources to the catalog

Resources are the items that users can request access to. You can add groups and teams, applications (enterprise applications that are available in Entra ID), SharePoint sites, and Microsoft Entra roles. To add Microsoft Entra roles, you need a Microsoft Entra ID Governance subscription.

You can now start adding resources to the catalog.

<figure>
  <img src="{{ img | append: '03-catalog-resources.png' | relative_url }}" alt="Resources page of the Demo catalog with the Add resources button">
  <figcaption>The Resources page of the catalog, where you add resources.</figcaption>
</figure>

For this example, I added security groups and an application.

## Step 3: Create an access package

Next, create an access package. Open the **Access packages** page of the catalog and select **New access package**.

<figure>
  <img src="{{ img | append: '04-catalog-access-packages.png' | relative_url }}" alt="Access packages page of the Demo catalog with the New access package button">
  <figcaption>The Access packages page of the catalog.</figcaption>
</figure>

You only see the groups and applications you added as resources. If you select **See all application(s)** (or **See all group(s) and team(s)**), you can select everything. These resources are then added to your catalog. Only a Global Administrator or Identity Governance Administrator can use this option.

<figure>
  <img src="{{ img | append: '05-select-applications.png' | relative_url }}" alt="Select applications pane with the option to see all applications that are not in the catalog">
  <figcaption>The option to select all applications, which is only available to Global Administrators and Identity Governance Administrators.</figcaption>
</figure>

## Step 4: Configure who can request access

A good way to let users request the access they need is to configure the access package as shown below. You can still scope it to specific users or groups. This way, you can give a department access while still letting its members request access when they need it. You can also require approval and let requesters provide a justification.

<figure>
  <img src="{{ img | append: '06-access-package-requests.png' | relative_url }}" alt="Requests tab of a new access package with the scope set to specific users and groups">
  <figcaption>The Requests tab: who can get access, and the scope set to specific users and groups.</figcaption>
</figure>

<figure>
  <img src="{{ img | append: '07-who-can-request-approval.png' | relative_url }}" alt="Who can request access section with Self selected, approval set to Yes and the first approver set to the manager">
  <figcaption>Who can request access, the approval setting, and the approver configuration.</figcaption>
</figure>

## Step 5: Configure the lifecycle

In the **Lifecycle** tab, you configure when the assignments to the access package expire. You also configure whether requesters can choose a specific timeline, and whether an access review is needed and who performs it.

<figure>
  <img src="{{ img | append: '08-access-package-lifecycle.png' | relative_url }}" alt="Lifecycle tab of a new access package with an expiration of 30 days and access review settings">
  <figcaption>The Lifecycle tab with expiration and access review settings.</figcaption>
</figure>

## Step 6: Request access as a user

Now let's request access to the access package as a user. Go to [https://myaccess.microsoft.com/](https://myaccess.microsoft.com/) and sign in with a user who is eligible for the access package. Select **Request** next to the package.

<figure>
  <img src="{{ img | append: '09-myaccess-request.png' | relative_url }}" alt="My Access portal listing the Demo access package with a Request link">
  <figcaption>The access package in My Access, with the Request link.</figcaption>
</figure>

The user can request the access package for themselves.

<figure>
  <img src="{{ img | append: '10-request-for-myself.png' | relative_url }}" alt="Request dialog with Myself selected as the requestor">
  <figcaption>Requesting the access package for yourself.</figcaption>
</figure>

The user can also request access for a **specific period**. They need to provide a **Business justification** before they select **Submit request**.

<figure>
  <img src="{{ img | append: '11-request-additional-questions.png' | relative_url }}" alt="Additional questions with the option to request for a specific period, start and end date fields and the business justification field">
  <figcaption>Requesting access for a specific period, with a business justification.</figcaption>
</figure>

The status of the request is visible in **Request history**. As you can see, the request is **Pending approval**.

<figure>
  <img src="{{ img | append: '12-request-history-pending.png' | relative_url }}" alt="Request history with the Demo request in Pending approval status">
  <figcaption>The request in Request history, with the status Pending approval.</figcaption>
</figure>

## Step 7: Approve the request

Now switch to the manager of this user, or to their backup. Go to **Approvals** and select **Approve** for the request.

<figure>
  <img src="{{ img | append: '13-approvals-pending.png' | relative_url }}" alt="Approvals page with the pending request selected and the Approve button">
  <figcaption>The pending request on the Approvals page.</figcaption>
</figure>

Choose **Approve** or **Deny**, add a reason if needed, and select **Submit**.

<figure>
  <img src="{{ img | append: '14-approve-decision.png' | relative_url }}" alt="Access request decision panel with Approve and Deny options and a reason field">
  <figcaption>The decision panel, with Approve or Deny and an optional reason.</figcaption>
</figure>

## Step 8: Verify the result

The test user is now a member of the two groups that were added to the access package in Entitlement Management.

<figure>
  <img src="{{ img | append: '15-user-groups.png' | relative_url }}" alt="Groups I am in page showing the group memberships of the test user">
  <figcaption>The test user's group memberships after approval.</figcaption>
</figure>

If you don't set a specific end date, the access lasts one month.

<figure>
  <img src="{{ img | append: '16-active-access-package.png' | relative_url }}" alt="Active access packages in My Access with start and end dates for the Demo package">
  <figcaption>The active access package, with a start date and an end date one month later.</figcaption>
</figure>

## Step 9: Remove access

A user can remove access they no longer need from **My Access**. In practice, though, users rarely do this themselves.

<figure>
  <img src="{{ img | append: '17-remove-access-menu.png' | relative_url }}" alt="Access packages page in My Access with the actions menu open and Remove access selected">
  <figcaption>Removing an access package from My Access.</figcaption>
</figure>

As an approver or administrator, you can also revoke access if needed. Select the approved assignment in the approval history and choose **Remove access**.

<figure>
  <img src="{{ img | append: '18-approvals-history-remove.png' | relative_url }}" alt="Approvals history with the Remove access button">
  <figcaption>Revoking an approved assignment from the approval history.</figcaption>
</figure>

Provide a reason for removing the access, and confirm.

<figure>
  <img src="{{ img | append: '19-remove-access-dialog.png' | relative_url }}" alt="Remove access confirmation dialog with a reason field and the Remove and Cancel buttons">
  <figcaption>The confirmation dialog, with a reason for the removal.</figcaption>
</figure>

After a few moments, the access is revoked.

## Summary

With catalogs, access packages, approvals, and lifecycle settings, Entitlement Management gives users access when they need it and removes that access when it is no longer needed.
