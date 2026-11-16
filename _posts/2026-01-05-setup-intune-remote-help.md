---
layout: post
title: "Setup Intune Remote Help"
date: 2026-01-05 17:11:00 +0100
categories: [Intune, Security]
tags: [Intune, Remote Help, Quick Assist, Support]
description: "Microsoft Intune Remote Help is a cloud-based remote support solution that allows IT support teams to connect securely to an end-user's device for real-time assistance."
---

{% assign img = '/assets/images/setup-intune-remote-help/' %}

## What is Intune Remote Help

## Microsoft Intune Remote Help is a cloud-based remote support solution that allows IT support teams to connect securely to an end-user's device for real-time assistance.

Remote Help will be added to your Microsoft 365 E3 license from July 2026. This will increase the price of this license from $23 to $26 per user per month.

And a great benefit compared to Quick Assist is that Remote Help supports elevated access, Enterprise authentication, Intune RBAC and auditing.

Remote Help only works within your organization's tenant – helpers can't assist users in another tenant or external organization.

## Setup

How to set up Intune Remote Help.

Go to Intune – Tenant Administration – Remote Help – Configure

<figure>
  <img src="{{ img | append: '01-image1.png' | relative_url }}" alt="Go to Intune – Tenant Administration – Remote Help – Configure">
</figure>

After you’ve enabled it you will see Remote Help Enabled.

Set Enable Remote Help to Enabled. If you want you can Allow Remote Help to enrolled devices and you can Disable Chat.

<figure>
  <img src="{{ img | append: '02-image2.png' | relative_url }}" alt="Set Enable Remote Help to Enabled. If you want you can Allow Remote Help to enrolled devices and you can Disable Chat.">
</figure>

After you’ve enabled it you will see Remote Help Enabled.

<figure>
  <img src="{{ img | append: '03-image3.png' | relative_url }}" alt="After you’ve enabled it you will see Remote Help Enabled.">
</figure>

## Configure Custom Roles

You can also create Custom roles to give your Remote Helpers specific rights to do their job and also only do the things they need.

Go to Tenant Administration - Roles

<figure>
  <img src="{{ img | append: '04-image4.png' | relative_url }}" alt="Go to Tenant Administration - Roles">
</figure>

Click Create – Intune role

<figure>
  <img src="{{ img | append: '05-image5.png' | relative_url }}" alt="Click Create – Intune role">
</figure>

Once again provide the Basics.

<figure>
  <img src="{{ img | append: '06-image6.png' | relative_url }}" alt="Once again provide the Basics.">
</figure>

You can configure the Remote Help app options.

<figure>
  <img src="{{ img | append: '07-image7.png' | relative_url }}" alt="You can configure the Remote Help app options.">
</figure>

And you need to enable at least the Remote tasks Offer remote assistance.

<figure>
  <img src="{{ img | append: '08-image8.png' | relative_url }}" alt="And you need to enable at least the Remote tasks Offer remote assistance.">
</figure>

When your Custom intune role is created you can assign it to a specific group.

Open your Custom Intune role.

<figure>
  <img src="{{ img | append: '09-image9.png' | relative_url }}" alt="Open your Custom Intune role.">
</figure>

Go to Assignments and click Assign

<figure>
  <img src="{{ img | append: '10-image10.png' | relative_url }}" alt="Go to Assignments and click Assign">
</figure>

Provide a Name for your Role Assignment.

<figure>
  <img src="{{ img | append: '11-image11.png' | relative_url }}" alt="Provide a Name for your Role Assignment.">
</figure>

Click Add groups and select your group.

<figure>
  <img src="{{ img | append: '12-image12.png' | relative_url }}" alt="Click Add groups and select your group.">
</figure>

Scope the Users, Groups or Devices that you want your group to be able to provide remote tasks.

<figure>
  <img src="{{ img | append: '13-image13.png' | relative_url }}" alt="Scope the Users, Groups or Devices that you want your group to be able to provide remote tasks.">
</figure>

Proceed with the steps: Review and Create.

## Install the Remote Help application on your devices

Download it from Microsoft [https://aka.ms/downloadremotehelp](https://aka.ms/downloadremotehelp) create a package for it in Intune and deploy it to your devices.

This application is required to set up the connection to your devices.

## Help your users

If you want to help a user on the device go to Devices – All devices and select the device that you want to give support.

<figure>
  <img src="{{ img | append: '14-image14.png' | relative_url }}" alt="If you want to help a user on the device go to Devices – All devices and select the device that you want to give support.">
</figure>

Select the three dots on the right side and select New remote assistance session.

<figure>
  <img src="{{ img | append: '15-image15.png' | relative_url }}" alt="Select the three dots on the right side and select New remote assistance session.">
</figure>

Select your device.

<figure>
  <img src="{{ img | append: '16-image16.png' | relative_url }}" alt="Select your device.">
</figure>

Intune is now sending the request to the device.

<figure>
  <img src="{{ img | append: '17-image17.png' | relative_url }}" alt="Intune is now sending the request to the device.">
</figure>

Your user will get a notification to accept Remote Help.

<figure>
  <img src="{{ img | append: '18-image18.png' | relative_url }}" alt="Your user will get a notification to accept Remote Help.">
</figure>

If your user clicks it your Remote Help will start.

<figure>
  <img src="{{ img | append: '19-image19.png' | relative_url }}" alt="If your user clicks it your Remote Help will start.">
</figure>

Your Administrator can now click Open Remote Help and the session will get started.

<figure>
  <img src="{{ img | append: '20-image20.png' | relative_url }}" alt="Your Administrator can now click Open Remote Help and the session will get started.">
</figure>

It will prompt your administrator to open the Remote Help application on his device.

<figure>
  <img src="{{ img | append: '21-image21.png' | relative_url }}" alt="It will prompt your administrator to open the Remote Help application on his device.">
</figure>

You can also get or provide Remote Help in two other ways. Via the web portal and directly via the Remote Help tool on your device.

Get Help from the web portal

Go to [https://aka.ms/rh](https://aka.ms/rh) in a browser and sign in with their organization's credentials.

Enter the code provided by the helper, and review and accept the prompts.

<figure>
  <img src="{{ img | append: '22-image22.png' | relative_url }}" alt="Enter the code provided by the helper, and review and accept the prompts.">
</figure>

To get the code to provide Help via the web portal

Sign in to [https://aka.ms/rhh](https://aka.ms/rhh)

Copy and share the eight-digit session code with the sharer that you're trying to help.

<figure>
  <img src="{{ img | append: '23-image23.png' | relative_url }}" alt="Copy and share the eight-digit session code with the sharer that you're trying to help.">
</figure>

And you can also use the Remote Help app directly.

Open the Remote Help app on your user device and ask for the code.

<figure>
  <img src="{{ img | append: '24-image24.png' | relative_url }}" alt="Open the Remote Help app on your user device and ask for the code.">
</figure>

Open the Remote Help app on your administrator’s device. Be aware that in all cases this should be a Managed device within the same tenant.

<figure>
  <img src="{{ img | append: '25-image25.png' | relative_url }}" alt="Open the Remote Help app on your administrator’s device. Be aware that in all cases this should be a Managed device within the same tenant.">
</figure>

In Intune you can see Remote Help sessions. In Remote Help sessions you can check who provided help to which recipient.

<figure>
  <img src="{{ img | append: '26-image26.png' | relative_url }}" alt="In Intune you can see Remote Help sessions. In Remote Help sessions you can check who provided help to which recipient.">
</figure>


