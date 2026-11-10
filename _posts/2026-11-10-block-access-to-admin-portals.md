---
layout: post
title: "Block access to admin portals"
date: 2026-11-10 10:00:00 +0100
categories: [Entra, Security]
tags: [Conditional Access, Entra ID, Admin Portals, Restrict Access]
description: "Normal users still have access to information in your tenant via Admin portals. Even if you’ve blocked access via the Restrict access to Microsoft Entra Admin center."
---

{% assign img = '/assets/images/block-access-to-admin-portals/' %}

Normal users still have access to information in your tenant via Admin portals. Even if you’ve blocked access via the Restrict access to Microsoft Entra Admin center.

You can restrict access to Microsoft Entra admin center via the setting in User Settings.

![Microsoft Entra admin center User settings with Restrict access to Microsoft Entra admin center set to Yes]({{ img | append: '01-user-settings-restrict-admin-center.png' | relative_url }})

This will restrict access in the first place. And your users will get the message You don’t have access.

![You don't have access error page in the Microsoft Entra admin center]({{ img | append: '02-you-dont-have-access.png' | relative_url }})

But they still can search for all Resources.

![Search results for the R_AdminUsers group in the Microsoft Entra admin center]({{ img | append: '03-search-group.png' | relative_url }})

You can select that group and even see its members.In this overview you could see all members of the group and their email address.

![Members of the R_AdminUsers group in the Microsoft Entra admin center]({{ img | append: '04-group-members.png' | relative_url }})

Or even devices.`

![Search results for a device in the Microsoft Entra admin center]({{ img | append: '05-search-device.png' | relative_url }})

You can now select the device and see the name of the owner and even his UPN.

![Device properties showing the owner and user principal name]({{ img | append: '06-device-properties.png' | relative_url }})

With Conditional Access we can block for All Users to the Admin Portals.

I’ve created a Conditional Access policy to block access to the Admin Portals and excluded a specific group of users.

The reason why we’ve excluded a group and not just admin roles is that we don’t have admin users with permanent assigned roles except for our Break Glass accounts.

Included the Target resource Microsoft Admin Portals. And Grant Block Acces to block access to the Admin Portals for all your users excluded the group that you want to exclude for this.

![Conditional Access policy with Microsoft Admin Portals as target resource and Block access as grant control]({{ img | append: '07-conditional-access-policy.png' | relative_url }})

All your users will now get the message that they don’t have access.

![Access denied message after signing in with a user account]({{ img | append: '08-access-denied-sign-in.png' | relative_url }})
