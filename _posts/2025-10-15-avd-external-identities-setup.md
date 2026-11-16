---
layout: post
title: "AVD External Identities setup"
date: 2025-10-15 08:39:00 +0200
categories: [Azure, Entra]
tags: [Azure Virtual Desktop, External Identities, Entra ID, Guest accounts]
description: "AVD for External Identities is a great way to provide your external contractors access!"
---

{% assign img = '/assets/images/avd-external-identities-setup/' %}

AVD for External Identities is a great way to provide your external contractors access!

How to set up AVD for External Identities.

Since last month Microsoft announced authentication for External Identities for Azure Virtual Desktop (in Preview). A great new feature for AVD.

In this blog post I will write down the steps I have taken to implement this.

Create the basics: a Resource Group, an NSG and a VNet.

Create an Entra ID group. This should be an Entra ID group to be able to add Guest Accounts to this group.

<figure>
  <img src="{{ img | append: '01-image1.png' | relative_url }}" alt="Create an Entra ID group. This should be an Entra ID group to be able to add Guest Accounts to this group.">
</figure>

Add the group to the Resource Group and assign them the Virtual Machine User Login role. Later you will add the Guest Accounts to this group.

<figure>
  <img src="{{ img | append: '02-image2.png' | relative_url }}" alt="Add the group to the Resource Group and assign them the Virtual Machine User Login role. Later you will add the Guest Accounts to this gr...">
</figure>

Now create your Host Pool. In my case I’ve created Pooled Host Pool.

Create your Session Host. To ensure you’re really getting the latest Windows Update with KB5065789, I’ve preferred to take the Windows 11 Enterprise 25H2 image. Add the machine to Microsoft Entra ID and Enroll VM in Intune.

<figure>
  <img src="{{ img | append: '03-image3.png' | relative_url }}" alt="Create your Session Host. To ensure you’re really getting the latest Windows Update with KB5065789, I’ve preferred to take the Windows 11...">
</figure>

<figure>
  <img src="{{ img | append: '04-image4.png' | relative_url }}" alt="Create your Session Host. To ensure you’re really getting the latest Windows Update with KB5065789, I’ve preferred to take the Windows 11...">
</figure>

Make sure to set the RDP Properties to Authenticate with Microsoft Entra.

<figure>
  <img src="{{ img | append: '05-image5.png' | relative_url }}" alt="Make sure to set the RDP Properties to Authenticate with Microsoft Entra.">
</figure>

Now invite a guest user and add them to the group you have assigned to the Virtual Machine User Login role.

<figure>
  <img src="{{ img | append: '06-image6.png' | relative_url }}" alt="Now invite a guest user and add them to the group you have assigned to the Virtual Machine User Login role.">
</figure>

Let your guest users log in via [https://windows.cloud.microsoft/](https://windows.cloud.microsoft/) the web portal of the Windows App.

In the login screen you choose Sign-In options. There you will see Sign in to an organization.

<figure>
  <img src="{{ img | append: '07-image7.png' | relative_url }}" alt="In the login screen you choose Sign-In options. There you will see Sign in to an organization.">
</figure>

<figure>
  <img src="{{ img | append: '08-image8.png' | relative_url }}" alt="In the login screen you choose Sign-In options. There you will see Sign in to an organization.">
</figure>

You need to inform your guest users of your domain name.

<figure>
  <img src="{{ img | append: '09-image9.png' | relative_url }}" alt="You need to inform your guest users of your domain name.">
</figure>

The users will now see an AVD desktop, as we used to see.

<figure>
  <img src="{{ img | append: '10-image10.png' | relative_url }}" alt="The users will now see an AVD desktop, as we used to see.">
</figure>

Another option is to log in to [https://windows.cloud.microsoft/](https://windows.cloud.microsoft/)

Click on your profile Picture and click on the 3 dots. You will see Switch Organization.

<figure>
  <img src="{{ img | append: '11-image11.png' | relative_url }}" alt="Click on your profile Picture and click on the 3 dots. You will see Switch Organization.">
</figure>

The users will see their own company tenant and the tenant where they are as a guest user.

<figure>
  <img src="{{ img | append: '12-image12.png' | relative_url }}" alt="The users will see their own company tenant and the tenant where they are as a guest user.">
</figure>

The Windows App doesn’t have the switch Directory option in the interface directly, but you can enable this in the Registry.



