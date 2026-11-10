---
layout: post
title: "Block access to the Microsoft admin portals with Conditional Access"
date: 2026-11-10 10:00:00 +0100
categories: [Entra, Security]
tags: [Conditional Access, Entra ID, Admin Portals, Restrict Access, Microsoft Entra admin center]
description: "Restricting the Microsoft Entra admin center is not enough. Normal users can still see group members and device owners. Use a Conditional Access policy to block the admin portals for everyone except an exclusion group."
---

Normal users still have access to information in your tenant through the admin portals, even when you have blocked access with the setting *Restrict access to Microsoft Entra admin center*.

## The problem

You can restrict access to the Microsoft Entra admin center with the setting under **User settings**. This stops users from opening the portal, and they will see the message *You don't have access*. However, they can still search for resources.

For example, a user can search for a group, select it, and see its members, including their email addresses. In the same way, a user can select a device and see the name of its owner and even their UPN.

## The solution: a Conditional Access policy

To block access to the admin portals for all users, I created a Conditional Access policy with the following configuration:

- **Users:** All users, excluding a specific group of users who are allowed to use the admin portals.
- **Target resources:** Microsoft Admin Portals.
- **Grant:** Block access.

I chose to exclude a group instead of excluding admin roles. We do not have admin users with permanently assigned roles, except for our break glass accounts. The group therefore controls who can work in the admin portals.

After the policy is enabled, all users who are not in the excluded group will receive the message that they don't have access.

Conditional Access requires a Microsoft Entra ID P1 license. You can find more information in the [Conditional Access documentation](https://learn.microsoft.com/entra/identity/conditional-access/overview).
