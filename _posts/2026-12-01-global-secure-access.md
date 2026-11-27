---
layout: post
title: "Global Secure Access"
date: 2026-12-01 09:00:00 +0100
categories: [Entra, Security]
tags: [Global Secure Access, Entra ID, Conditional Access, Traffic forwarding, Microsoft 365]
description: "People no longer work only from the office."
---

{% assign img = '/assets/images/global-secure-access/' %}

## Why Global Secure Access

People no longer work only from the office. They work from home, on the road, and on networks you don't control. The traditional corporate network is no longer the place where security is enforced. Security has to follow the identity of the user and the state of the device, wherever they are. Global Secure Access is Microsoft's answer to this, and the Microsoft 365 traffic profile is the part that applies directly to the services your people use every day.

The Microsoft 365 traffic profile routes traffic to Exchange Online, SharePoint, OneDrive, and Teams through the Global Secure Access service. From there, Conditional Access can make decisions based on that path. With the **compliant network check**, you can allow access to Microsoft 365 only when the traffic comes through the service. That reduces the risk of stolen session tokens and replay attacks, and you no longer have to maintain lists of egress IP addresses for your policies.

## Set up Global Secure Access

Activate Global Secure Access

Go to Entra admin center – **Global Secure Access** and click **Activate**.

<figure>
  <img src="{{ img | append: '01-image1.png' | relative_url }}" alt="Go to Entra admin center – Global Secure Access and click Activate.">
</figure>

Your tenant is getting onboarded

<figure>
  <img src="{{ img | append: '02-image2.png' | relative_url }}" alt="Your tenant is getting onboarded">
</figure>

Activation is completed

<figure>
  <img src="{{ img | append: '03-image3.png' | relative_url }}" alt="Activation is completed">
</figure>

Get Started

<figure>
  <img src="{{ img | append: '04-image4.png' | relative_url }}" alt="Get Started">
</figure>

Go to **Traffic forwarding** and first let’s **switch to v2**. But be aware this is still in preview.

If you switch to v2 you can’t switch back.

<figure>
  <img src="{{ img | append: '05-image5.png' | relative_url }}" alt="If you switch to v2 you can’t switch back.">
</figure>

Select OK to switch to **Traffic Forwarding Profiles v2**.

<figure>
  <img src="{{ img | append: '06-image6.png' | relative_url }}" alt="Select OK to switch to Traffic Forwarding Profiles v2.">
</figure>

The deployment is started

<figure>
  <img src="{{ img | append: '07-image7.png' | relative_url }}" alt="The deployment is started">
</figure>

And the deployment is done

<figure>
  <img src="{{ img | append: '08-image8.png' | relative_url }}" alt="And the deployment is done">
</figure>

You will see three traffic profiles: an M365 profile, a **Private profile** and an **Internet profile.**

<figure>
  <img src="{{ img | append: '09-image9.png' | relative_url }}" alt="You will see three traffic profiles: an M365 profile, a Private profile and an Internet profile.">
</figure>

We will only focus on the **Microsoft 365 Traffic forwarding profile**. Because this is the only profile that’s included in the Entra ID P1 or P2 license. For the other two you need an additional Microsoft Entra Internet Access or Microsoft Entra Suite license.

[Global Secure Access traffic forwarding profiles - Global Secure Access | Microsoft Learn](https://learn.microsoft.com/en-us/entra/global-secure-access/concept-traffic-forwarding)

Select the Microsoft 365 traffic forwarding profile and enable it.

<figure>
  <img src="{{ img | append: '10-image10.png' | relative_url }}" alt="Select the Microsoft 365 traffic forwarding profile and enable it.">
</figure>

For this demo I’ve assigned the profile to All users/devices. When this has been done, all devices with the Global Secure Access client receive the profile. Up next we will package and deploy the client.

<figure>
  <img src="{{ img | append: '11-image11.png' | relative_url }}" alt="For this demo I’ve assigned the profile to All users/devices. When this has been done, all devices with the Global Secure Access client r...">
</figure>

## Session Management

We will also set up compliant network enforcement. This reduces the risk of token theft and replay attacks. Microsoft Entra ID performs authentication plane enforcement at the time of user authentication.

Go to **Global Secure Access – Settings – Session management**

<figure>
  <img src="{{ img | append: '12-image12.png' | relative_url }}" alt="Go to Global Secure Access – Settings – Session management">
</figure>

## Download and install client

You need to install the client to acquire Microsoft traffic

<figure>
  <img src="{{ img | append: '13-image13.png' | relative_url }}" alt="You need to install the client to acquire Microsoft traffic">
</figure>

Go to **Global Secure Access – Connect** – **Client** **download** to download the client for your devices.

<figure>
  <img src="{{ img | append: '14-image14.png' | relative_url }}" alt="Go to Global Secure Access – Connect – Client download to download the client for your devices.">
</figure>

Create an **Intunewin** package.

<figure>
  <img src="{{ img | append: '15-image15.png' | relative_url }}" alt="Create an Intunewin package.">
</figure>

Microsoft has made a great script to use and shows how to package it. https://[learn.microsoft.com/en-us/entra/global-secure-access/how-to-install-windows-client#package-the-client](https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-install-windows-client)

We will upload this package in **Intune**.

Go to Intune – Devices – All apps – Create

Create a Windows app (Win32)

<figure>
  <img src="{{ img | append: '16-image16.png' | relative_url }}" alt="Create a Windows app (Win32)">
</figure>

Select your **Intunewin** package you just created. And provide your app information.

<figure>
  <img src="{{ img | append: '17-image17.png' | relative_url }}" alt="Select your Intunewin package you just created. And provide your app information.">
</figure>

Provide the **Installer type** and **Uninstaller type**. The Uninstall command is **"GlobalSecureAccessClient.exe" /uninstall /quiet /norestart.** Change **Allow** **available uninstall** to **No** because we don’t want our users to be able to uninstall this agent. And set Device restart behavior to Determine behavior based on return codes. These are the standard codes that get provided, you should have at least **0, 3010** and **1618** for a positive installation.

<figure>
  <img src="{{ img | append: '18-image18.png' | relative_url }}" alt="Provide the Installer type and Uninstaller type. The Uninstall command is 'GlobalSecureAccessClient.exe' /uninstall /quiet /*...">
</figure>

Because our installer is a PowerShell script we can select the script so we don’t have to provide the PowerShell run command.

<figure>
  <img src="{{ img | append: '19-image19.png' | relative_url }}" alt="Because our installer is a PowerShell script we can select the script so we don’t have to provide the PowerShell run command.">
</figure>

In the **Requirements** step provide the **OS** **architecture** and **Minimum OS version**.

<figure>
  <img src="{{ img | append: '20-image20.png' | relative_url }}" alt="In the Requirements step provide the OS architecture and Minimum OS version.">
</figure>

Use a manual detection rule and enter the **path filename** and the **detection method**. You can check the **file version** in the details of your EXE.

<figure>
  <img src="{{ img | append: '21-image21.png' | relative_url }}" alt="Use a manual detection rule and enter the path filename and the detection method. You can check the file version in the detai...">
</figure>

Assign the package to your All Users**, All Devices** or **selected groups** and change the **Restart grace period to Enabled so that your users** need to reboot their device after installation.

<figure>
  <img src="{{ img | append: '22-image22.png' | relative_url }}" alt="Assign the package to your All Users, All Devices or selected groups and change the Restart grace period to Enabled so that you...">
</figure>

## Remediation scripts

We can use remediation scripts to prevent standard users from disabling the client.

Microsoft has made these scripts also for you. You only have to add them in Intune. https://[learn.microsoft.com/en-us/entra/global-secure-access/how-to-install-windows-client#configure-global-secure-access-client-settings-by-using-intune](https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-install-windows-client)

Go to Intune – Devices – Scripts and remediations – Create

<figure>
  <img src="{{ img | append: '23-image23.png' | relative_url }}" alt="Go to Intune – Devices – Scripts and remediations – Create">
</figure>

Add the scripts you’ve downloaded from Microsoft and set **Run script in 64-bit PowerShell** to **Yes**. In both scripts, set the following values in $gsaSettings: HideSignOutButton = 1, HideDisablePrivateAccessButton = 1, HideDisableButton = 1 and RestrictNonPrivilegedUsers = 1.

Standard users can then no longer disable the client, and the related menu buttons are hidden.

<figure>
  <img src="{{ img | append: '24-image24.png' | relative_url }}" alt="Standard users can then no longer disable the client, and the related menu buttons are hidden.">
</figure>

And assign it to your Users, Devices or specific group(s).

## Conditional Access Policy

You need to create a **Conditional Access Policy** to enforce when and where your traffic management policies will be applied.

The following diagram illustrates Universal Conditional Access targeting internet resources and Microsoft apps with Global Secure Access as provided by Microsoft.

<figure>
  <img src="{{ img | append: '25-image25.png' | relative_url }}" alt="The following diagram illustrates Universal Conditional Access targeting internet resources and Microsoft apps with Global Secure Access ...">
</figure>

[https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-target-resource-microsoft-profile#create-a-conditional-access-policy-targeting-global-secure-access-internet-traffic](https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-target-resource-microsoft-profile)

For this demo I’ve only assigned to a single user. For a production environment, be aware that you should at least exclude your break-glass accounts.

Select **All internet resources** under Target resources and exclude All Compliant Network locations; the policy will block access. In short, if you’re not on a Compliant Network location, you will be blocked.

<figure>
  <img src="{{ img | append: '26-image26.png' | relative_url }}" alt="Select All internet resources under Target resources and exclude All Compliant Network locations; the policy will block access. In sh...">
</figure>

## User experience

Intune has installed the agent but requires a reboot as expected.

<figure>
  <img src="{{ img | append: '27-image27.png' | relative_url }}" alt="Intune has installed the agent but requires a reboot as expected.">
</figure>

You can see that your Global Secure Access client is installed and active in your **icon tray**. The icon will have a green circle.

<figure>
  <img src="{{ img | append: '28-image28.png' | relative_url }}" alt="You can see that your Global Secure Access client is installed and active in your icon tray. The icon will have a green circle.">
</figure>

<figure>
  <img src="{{ img | append: '29-image29.png' | relative_url }}" alt="You can see that your Global Secure Access client is installed and active in your icon tray. The icon will have a green circle.">
</figure>

As you can see you can’t disable the client. This is configured with the remediation script.

If you try to access Microsoft pages with the **Global Secure Access** client **disabled**, you will be blocked from this resource.

<figure>
  <img src="{{ img | append: '30-image30.png' | relative_url }}" alt="If you try to access Microsoft pages with the Global Secure Access client disabled, you will be blocked from this resource.">
</figure>

In the **sign-in logs** you will see that the access is blocked.

<figure>
  <img src="{{ img | append: '31-image31.png' | relative_url }}" alt="In the sign-in logs you will see that the access is blocked.">
</figure>

Blocked by our Conditional Access policy “Global Secure Access – Compliant Networks”.

<figure>
  <img src="{{ img | append: '32-image32.png' | relative_url }}" alt="Blocked by our Conditional Access policy “Global Secure Access – Compliant Networks”.">
</figure>

In the **Global Secure Access** **Dashboard** you can see the **Traffic Usage**.

<figure>
  <img src="{{ img | append: '33-image33.png' | relative_url }}" alt="In the Global Secure Access Dashboard you can see the Traffic Usage.">
</figure>

## Prerequisites

You must have an administrator with at least the following roles assigned. Global

**Secure Access Administrator** role in **Microsoft Entra ID to enable traffic profiles. Conditional**

**Access Administrator** role to create and interact with **Conditional Access policies.** An **Entra ID P1** or **P2 license** needs to be assigned.

to your tenant to be able to set up **Traffic** **Forwarding Profiles** for **Microsoft 365 traffic.** For all other profiles you need to have additional licenses.

Check the following Microsoft link to compare features:

https://[learn.microsoft.com/en-gb/entra/global-secure-access/overview-what-is-global-secure-access#feature-comparison-table](https://learn.microsoft.com/en-gb/entra/global-secure-access/overview-what-is-global-secure-access)




