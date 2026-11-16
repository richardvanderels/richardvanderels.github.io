---
layout: post
title: "Setup LAPS"
date: 2026-01-05 13:08:00 +0100
categories: [Intune, Security]
tags: [Intune, Windows LAPS, Entra ID, Security]
description: "If you don’t use Endpoint Privilege Management tooling you can still provide elevated permissions on your client devices with Windows LAPS."
---

{% assign img = '/assets/images/setup-laps/' %}

If you don’t use Endpoint Privilege Management tooling you can still provide elevated permissions on your client devices with Windows LAPS.

Windows LAPS is a Windows feature that automatically saves your local administrator account password on your Microsoft Entra-joined devices.

Windows LAPS to regularly rotate and manage local administrator account passwords.

## Enable LAPS in Entra ID

To enable LAPS in Entra ID, go to your Entra Admin portal.

Devices – Device Settings – Enable Microsoft Entra Local Administrator Password Solution (LAPS).

<figure>
  <img src="{{ img | append: '01-image1.png' | relative_url }}" alt="Devices – Device Settings – Enable Microsoft Entra Local Administrator Password Solution (LAPS).">
</figure>

## Configure Configuration Profile in Intune

Now let’s create a Configuration Profile in Intune go to your Intune Admin portal.

Endpoint security – Account protection – Create policy – Local admin password solution (LAPS).

<figure>
  <img src="{{ img | append: '02-image2.png' | relative_url }}" alt="Endpoint security – Account protection – Create policy – Local admin password solution (LAPS).">
</figure>

Provide the Basics.

<figure>
  <img src="{{ img | append: '03-image3.png' | relative_url }}" alt="Provide the Basics.">
</figure>

Configuration settings.

Because I’m only using Entra ID-only devices we can select Backup Directory Backup the password to Microsoft Entra ID only.

Password Age Days we kept standard to 30 days. But I will recommend a shorter amount of time.

Password Complexity kept Default

Password Length is set to 14

Automatic Account Management Enabled – The target account will be automatically managed. I will show that a new WLapsAdmin account will be created by this setting.

Automatically Account Management Enable Account – The target account will be enabled will also enable this account.

<figure>
  <img src="{{ img | append: '04-image4.png' | relative_url }}" alt="Automatically Account Management Enable Account – The target account will be enabled will also enable this account.">
</figure>

Assign it to your devices. Review and create.

<figure>
  <img src="{{ img | append: '05-image5.png' | relative_url }}" alt="Assign it to your devices. Review and create.">
</figure>

Now let’s check if we can see a LAPS password in Intune and Entra ID.

For Intune go to your Intune Admin Portal – Devices – Select your device – Local admin password.

<figure>
  <img src="{{ img | append: '06-image6.png' | relative_url }}" alt="For Intune go to your Intune Admin Portal – Devices – Select your device – Local admin password.">
</figure>

For Entra ID go to your Entra Admin Portal – Devices – All Devices – Select your device – Local administrator password recovery.

<figure>
  <img src="{{ img | append: '07-image7.png' | relative_url }}" alt="For Entra ID go to your Entra Admin Portal – Devices – All Devices – Select your device – Local administrator password recovery.">
</figure>

You can see that there is a local administrator password. You can also see when it is created at Last password rotation and when it will be the Next password rotation. Because we selected Password Age Days to 30 in the settings the next rotation will be after 30 days.

Go to your user device to check the LAPS account and the password.

To check the account that’s created for LAPS with your Configuration Profile go to Local Users and Groups.

<figure>
  <img src="{{ img | append: '08-image8.png' | relative_url }}" alt="To check the account that’s created for LAPS with your Configuration Profile go to Local Users and Groups.">
</figure>

Right-click your installer for example and click Run as a different user.

<figure>
  <img src="{{ img | append: '09-image9.png' | relative_url }}" alt="Right-click your installer for example and click Run as a different user.">
</figure>

Select Use a different account and enter the LAPS username and password.

<figure>
  <img src="{{ img | append: '10-image10.png' | relative_url }}" alt="Select Use a different account and enter the LAPS username and password.">
</figure>

And your installer will start.

<figure>
  <img src="{{ img | append: '11-image11.png' | relative_url }}" alt="And your installer will start.">
</figure>


