---
layout: post
title: "Block countries with Conditional Access and grant temporary exceptions with Access Packages"
date: 2026-10-12 10:00:00 +0200
categories: [Entra, Security]
tags: [Conditional Access, Entitlement Management, Access Packages, Named Locations, Entra ID]
image: /assets/images/conditional-access-and-access-packages/01-ca-signal-decision-enforcement.png
description: "Block sign-ins from countries outside Europe with a Conditional Access policy, and let users request a temporary exception through an Entitlement Management access package."
---

{% assign img = '/assets/images/conditional-access-and-access-packages/' %}

We received a request to allow access from countries outside the EU, but we did not want to grant that access permanently. The solution combines two features. A Conditional Access policy blocks sign-ins from countries outside Europe. An Entitlement Management access package gives users a temporary exception to that policy, so they can work from outside Europe for a limited period while we stay in control.

## Before you begin

Entitlement Management requires a Microsoft Entra ID Governance or Microsoft Entra Suite subscription for your organization's users. Some capabilities within this feature may work with a Microsoft Entra ID P2 subscription.

Conditional Access requires Microsoft Entra ID P1 licenses. Customers with Microsoft 365 Business Premium licenses can also use Conditional Access. Risk-based policies, based on sign-in risk or user risk, require Microsoft Entra ID Protection, which is a Microsoft Entra ID P2 feature.

## What is Entitlement Management Access Packages?

An access package is a bundle of all the resources, with the access an identity needs, to work on a project or perform a task. You can use access packages to govern access for internal identities, and also for identities from outside your organization.

## What is Conditional Access?

Microsoft Entra Conditional Access brings signals together to make decisions and enforce organizational policies. It is Microsoft's Zero Trust policy engine. It takes signals from various sources into account when it decides whether to allow access, require additional assurance, or block access.

<figure>
  <img src="{{ img | append: '01-ca-signal-decision-enforcement.png' | relative_url }}" alt="Diagram showing how Conditional Access takes signals, makes a decision, and enforces the organizational policy">
  <figcaption>Conditional Access in three steps: signals, decision, and enforcement.</figcaption>
</figure>

## Setup

Here we configure all the parts needed to fulfill this request. The setup consists of a named location and a Conditional Access policy that blocks everything except that location. After that, we create an access package that gives selected users a temporary exception.

## Step 1: Create a named location

Go to **Named locations** in the Conditional Access section of the Microsoft Entra admin center.

<figure>
  <img src="{{ img | append: '02-named-locations-menu.png' | relative_url }}" alt="Conditional Access section of the Microsoft Entra admin center with the Named locations option selected">
  <figcaption>The Named locations option in the Conditional Access section.</figcaption>
</figure>

Create a named location and add all EU countries.

<figure>
  <img src="{{ img | append: '03-named-location-countries.png' | relative_url }}" alt="Update location pane with a list of countries and checkboxes for selecting them">
  <figcaption>Selecting the countries for the named location. Select all EU countries and save the named location.</figcaption>
</figure>

## Step 2: Create a Conditional Access policy that blocks all other countries

Create a Conditional Access policy that blocks all countries except the EU countries from the named location you created in the previous step. Include all locations, and exclude the allowed countries.

<figure>
  <img src="{{ img | append: '04-block-countries-policy.png' | relative_url }}" alt="Conditional Access policy named Generic - BLOCK - Countries not Allowed, with the network condition set to any location and the named location excluded">
  <figcaption>The policy Generic - BLOCK - Countries not Allowed. It applies to any location, excluding the EU named location, and grants block access.</figcaption>
</figure>

Assign a group that will be excluded from this policy.

<figure>
  <img src="{{ img | append: '05-exclude-group.png' | relative_url }}" alt="Conditional Access policy with the Exclude tab showing the group Exclude-Block-Countries">
  <figcaption>The group Exclude-Block-Countries is excluded from the policy.</figcaption>
</figure>

We want to be flexible in assigning this exclusion, and we also want to keep the option of permanent exclusions. That is why we create an Entitlement Management access package.

## Step 3: Set up the access package

### Create a catalog

Go to **ID Governance**, open **Entitlement management**, and create a new catalog.

<figure>
  <img src="{{ img | append: '06-identity-governance-catalogs.png' | relative_url }}" alt="Identity Governance section of the Microsoft Entra admin center with the Catalogs and Entitlement management options">
  <figcaption>Identity Governance, with the Catalogs and Entitlement management options.</figcaption>
</figure>

Enable the catalog for user requests. This allows users to request access.

<figure>
  <img src="{{ img | append: '07-new-catalog.png' | relative_url }}" alt="New catalog form with the name Exclude Block Countries and requests enabled for users">
  <figcaption>The new catalog, with requests enabled for users and not for external users.</figcaption>
</figure>

### Create the access package

Create a new access package within this catalog. Select **See all Groups** to add groups as resources to the catalog.

<figure>
  <img src="{{ img | append: '08-select-groups.png' | relative_url }}" alt="Select groups pane with the option to see all groups and the group Exclude-Block-Countries selected">
  <figcaption>Adding the Exclude-Block-Countries group as a resource.</figcaption>
</figure>

To allow users to request this access, set **Who can get access** to users in the directory, and choose the scope of users you want to give this ability.

<figure>
  <img src="{{ img | append: '09-access-package-requests.png' | relative_url }}" alt="Requests tab of the access package with who can get access set to users in the directory and who can request access set to Self">
  <figcaption>The Requests tab, with users in the directory able to request access.</figcaption>
</figure>

### Configure expiration

We don't want to grant lifetime access, so we configure expiration settings. In our situation, most users will not be outside Europe for longer than 14 days.

<figure>
  <img src="{{ img | append: '10-access-package-expiration.png' | relative_url }}" alt="Lifecycle settings of the access package with assignments expiring after 14 days and access reviews configured">
  <figcaption>The lifecycle settings. Assignments expire after 14 days, and access reviews run monthly.</figcaption>
</figure>

## Step 4: Request access as a user

Now let's get access as a user, so that you can work from outside Europe.

Sign in to <https://myaccess.microsoft.com/> as one of your test users.

<figure>
  <img src="{{ img | append: '11-myaccess-access-package.png' | relative_url }}" alt="My Access portal listing the Exclude Block Countries access package with a Request link">
  <figcaption>The access package in My Access, with the Request link.</figcaption>
</figure>

Select **Request** to request access to the resource in this access package.

<figure>
  <img src="{{ img | append: '12-request-for-myself.png' | relative_url }}" alt="Request dialog with Myself selected as the requestor">
  <figcaption>Requesting the access package for yourself.</figcaption>
</figure>

Then provide a business justification.

<figure>
  <img src="{{ img | append: '13-request-business-justification.png' | relative_url }}" alt="Additional questions dialog with the business justification field filled in">
  <figcaption>Entering the business justification for the request.</figcaption>
</figure>

The approver of the access package can now review the request and approve or deny it in the My Access portal.

<figure>
  <img src="{{ img | append: '14-approvals-pending.png' | relative_url }}" alt="Approvals page with one pending request for the Exclude Block Countries access package">
  <figcaption>The pending request on the Approvals page of the approver.</figcaption>
</figure>

<figure>
  <img src="{{ img | append: '15-approve-decision.png' | relative_url }}" alt="Access request decision panel with Approve selected and a reason entered">
  <figcaption>The approver selects Approve, enters a reason, and submits the decision.</figcaption>
</figure>

Administrators can also see the assignments of the access package in Microsoft Entra ID. As you can see, the assignment ends on the date that was specified.

<figure>
  <img src="{{ img | append: '16-assignment-end-date.png' | relative_url }}" alt="Assignments of the Exclude Block Countries access package with a delivered assignment and an end date">
  <figcaption>The assignment in Microsoft Entra ID, with the end date set.</figcaption>
</figure>

The group is also added to the user account.

<figure>
  <img src="{{ img | append: '17-user-groups.png' | relative_url }}" alt="Groups page of the test user showing the group Exclude-Block-Countries">
  <figcaption>The test user is now a member of the group Exclude-Block-Countries.</figcaption>
</figure>

## Step 5: Test sign-in from outside Europe

Now let's check whether we can sign in from outside Europe. We test with two users, to show that the block policy applies to the user who is not in the exclusion group. We use the What if tool in Conditional Access to run the test.

Select the necessary options, such as the user, the cloud app, the device platform, and the IP address and country.

### A user in the group

When we run this test with a user who is assigned to the group, the block policy does not apply.

<figure>
  <img src="{{ img | append: '18-whatif-member-top.png' | relative_url }}" alt="What if tool with the test user Jan Jansen selected, the cloud app My Apps, and Windows as the device platform">
  <figcaption>The What if test for a user in the exclusion group.</figcaption>
</figure>

<figure>
  <img src="{{ img | append: '19-whatif-member-result.png' | relative_url }}" alt="What if result with an IP address in Japan, where the block policy appears under policies that will not apply because of users and groups">
  <figcaption>The result: the block policy appears under policies that will not apply, because of users and groups.</figcaption>
</figure>

### A user who is not in the group

When we run this test with a user who is not assigned to the group, the policies that apply are shown in the results.

<figure>
  <img src="{{ img | append: '20-whatif-non-member-top.png' | relative_url }}" alt="What if tool with the user Bart Smit selected, the cloud app My Apps, and Windows as the device platform">
  <figcaption>The What if test for a user who is not in the exclusion group.</figcaption>
</figure>

<figure>
  <img src="{{ img | append: '21-whatif-non-member-result.png' | relative_url }}" alt="What if result with an IP address in Japan, where the block policy appears under policies that will apply with the action block access">
  <figcaption>The result: the block policy applies and grants block access.</figcaption>
</figure>

## Summary

We created a small Entitlement Management access package and tested it. We also created a Conditional Access policy that blocks all countries outside Europe. The access package gives users the ability to work temporarily from outside Europe, and we verified the result with the What if tool in Conditional Access.
