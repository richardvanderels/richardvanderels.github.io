---
layout: post
title: "Setup Endpoint Privileged Management"
date: 2025-12-12 16:31:00 +0100
categories: [Intune, Security]
tags: [Intune, Endpoint Privilege Management, Security, Windows]
description: "What is Endpoint Privileged Management in Intune."
---

{% assign img = '/assets/images/setup-endpoint-privileged-management/' %}

What is Endpoint Privileged Management in Intune. It’s a feature to let your standard users without any administrator rights run tasks that require elevated permissions like installing applications. This allows you to provide them temporarily privileged rights to install or update an application for example.

Endpoint Privileged Management will also become an addition on the E5 license. The price of the E5 license will increase by $3 a month per user.

<figure>
  <img src="{{ img | append: '01-image1.png' | relative_url }}" alt="Endpoint Privileged Management will also become an addition on the E5 license. The price of the E5 license will increase by $3 a month pe...">
</figure>

[Advancing Microsoft 365: New capabilities and pricing update | Microsoft 365 Blog](https://www.microsoft.com/en-us/microsoft-365/blog/2025/12/04/advancing-microsoft-365-new-capabilities-and-pricing-update/)

Which is a lot less than what the Intune Suite license costs with $10 a month per user with all these features.

<figure>
  <img src="{{ img | append: '02-image2.png' | relative_url }}" alt="Which is a lot less than what the Intune Suite license costs with $10 a month per user with all these features.">
</figure>

[Microsoft Intune Plans and Pricing](https://www.microsoft.com/en-us/security/business/microsoft-intune-pricing)

## How to set up Endpoint Privileged Management step-by-step

Log in to your Intune Admin portal [https://intune.microsoft.com](https://intune.microsoft.com)

Go to Endpoint Security – Endpoint Privilege Management

<figure>
  <img src="{{ img | append: '03-image3.png' | relative_url }}" alt="Go to Endpoint Security – Endpoint Privilege Management">
</figure>

You can create Elevation settings and Elevation rules. Settings are default responses for any elevated request. Where Rules are specific just-in-time rules to apps and files on your device.

## Elevation settings policy

We will start creating settings policies. Click Create and start with creating an Elevation settings policy. Optional you can add Elevation rules policies to it. And click Create again.

<figure>
  <img src="{{ img | append: '04-image4.png' | relative_url }}" alt="We will start creating settings policies. Click Create and start with creating an Elevation settings policy. Optional you can add Elevati...">
</figure>

Provide the Basics

<figure>
  <img src="{{ img | append: '05-image5.png' | relative_url }}" alt="Provide the Basics">
</figure>

Open the dropdown menu of Privilege management elevation client settings.

Below you can see the standard settings.

<figure>
  <img src="{{ img | append: '06-image6.png' | relative_url }}" alt="Below you can see the standard settings.">
</figure>

Default elevation response needs to be set. You will have 4 options.

Deny all requests, this will block every elevated prompt.

Require user confirmation, a user needs to confirm what they’re going to do.

Require support approval, someone from your support team will need to approve this request.

Not configured, if you leave it not configured you will still have normal user behaviour and your user will get blocked in an elevated prompt.

In this case we will do a test with Require support approval to users interface but also the interface for your support team.

<figure>
  <img src="{{ img | append: '07-image7.png' | relative_url }}" alt="In this case we will do a test with Require support approval to users interface but also the interface for your support team.">
</figure>

The other settings Send elevation data for reporting and Reporting scope will give you the option if you will send a report and what your scope will be. We will leave standard for now, as it wouldn’t impact your users in this test.

You can now also assign this policy to one or more groups, or to all your users or all your device. That’s up to you. In test cases I will always prefer to assign it to a test group first.

<figure>
  <img src="{{ img | append: '08-image8.png' | relative_url }}" alt="You can now also assign this policy to one or more groups, or to all your users or all your device. That’s up to you. In test cases I wil...">
</figure>

Review your settings and click Create

Your policy is now created.

<figure>
  <img src="{{ img | append: '09-image9.png' | relative_url }}" alt="Your policy is now created.">
</figure>

The setting that we have created in this case is Require support approval.

<figure>
  <img src="{{ img | append: '10-image10.png' | relative_url }}" alt="The setting that we have created in this case is Require support approval.">
</figure>

EPM is using a client on your devices. This client will automatically get installed on the devices that are assigned to an Elevation settings policy.

Now let’s head over to the device of your user. Check if the EPM Agent is installed on the users device.

Go to C:\Program Files and check if the folder Microsoft EPM Client is there.

<figure>
  <img src="{{ img | append: '11-image11.png' | relative_url }}" alt="Go to C:\Program Files and check if the folder Microsoft EPM Client is there.">
</figure>

## Require support approval

Right-click the installer that you want to install. And you should see Run with elevated access.

<figure>
  <img src="{{ img | append: '12-image12.png' | relative_url }}" alt="Right-click the installer that you want to install. And you should see Run with elevated access.">
</figure>

Provide the Business justification and click Send.

<figure>
  <img src="{{ img | append: '13-image13.png' | relative_url }}" alt="Provide the Business justification and click Send.">
</figure>

Your request will be sent to your administrator.

<figure>
  <img src="{{ img | append: '14-image14.png' | relative_url }}" alt="Your request will be sent to your administrator.">
</figure>

Because we have configured the option Require support approval you will see the message that an administrator should approve this request.

<figure>
  <img src="{{ img | append: '15-image15.png' | relative_url }}" alt="Because we have configured the option Require support approval you will see the message that an administrator should approve this request.">
</figure>

Now it’s time for your administrator or support team go to Intune – Endpoint Security – Endpoint Privilege Management – Elevation Requests.

You will see all requests approved, pending and denied. Select your pending request to approve or deny it.

<figure>
  <img src="{{ img | append: '16-image16.png' | relative_url }}" alt="You will see all requests approved, pending and denied. Select your pending request to approve or deny it.">
</figure>

Click the pending request to review it and Approve or Deny this request.

<figure>
  <img src="{{ img | append: '17-image17.png' | relative_url }}" alt="Click the pending request to review it and Approve or Deny this request.">
</figure>

And provide the Reason.

<figure>
  <img src="{{ img | append: '18-image18.png' | relative_url }}" alt="And provide the Reason.">
</figure>

Now let’s go back to your user. The user will get a notification when the request is approved.

<figure>
  <img src="{{ img | append: '19-image19.png' | relative_url }}" alt="Now let’s go back to your user. The user will get a notification when the request is approved.">
</figure>

Right-click Run with elevated access again.

<figure>
  <img src="{{ img | append: '20-image12.png' | relative_url }}" alt="Right-click Run with elevated access again.">
</figure>

Your user will see that his request is approved and can click Continue.

<figure>
  <img src="{{ img | append: '21-image20.png' | relative_url }}" alt="Your user will see that his request is approved and can click Continue.">
</figure>

And you can finish the installation.

Now let’s check the other 2 available options in Endpoint Privilege Management Require user confirmation and Deny all requests.

## Require user confirmation

For User confirmation you will get two options for Validation Business justification or Windows authentication.

<figure>
  <img src="{{ img | append: '22-image21.png' | relative_url }}" alt="For User confirmation you will get two options for Validation Business justification or Windows authentication.">
</figure>

Business justification will let your users provide a reason why they want to use elevated access.

When right click Run with elevated access your users will get to Enter business justification and can click Continue to use elevated access.

<figure>
  <img src="{{ img | append: '23-image22.png' | relative_url }}" alt="When right click Run with elevated access your users will get to Enter business justification and can click Continue to use elevated access.">
</figure>

Windows Authentication will only give a warning if they want to verify their action.

<figure>
  <img src="{{ img | append: '24-image23.png' | relative_url }}" alt="Windows Authentication will only give a warning if they want to verify their action.">
</figure>

## Deny all requests

For Deny all request we will only check the User Interface. When they right click Run with elevated access.

Your user will get the message.

<figure>
  <img src="{{ img | append: '25-image24.png' | relative_url }}" alt="Your user will get the message.">
</figure>

Now that we’ve completely walked through the settings policy let’s check the elevation rules.

## Elevation rules policy

Let’s go back to Intune – Endpoint Security – Endpoint Privilege Management – Create

<figure>
  <img src="{{ img | append: '26-image25.png' | relative_url }}" alt="Let’s go back to Intune – Endpoint Security – Endpoint Privilege Management – Create">
</figure>

Select Elevation rules policy

<figure>
  <img src="{{ img | append: '27-image26.png' | relative_url }}" alt="Select Elevation rules policy">
</figure>

Provide the Basics.

<figure>
  <img src="{{ img | append: '28-image27.png' | relative_url }}" alt="Provide the Basics.">
</figure>

Click + Edit instance

<figure>
  <img src="{{ img | append: '29-image28.png' | relative_url }}" alt="Click + Edit instance">
</figure>

Provide a rule name. A description is not required.

<figure>
  <img src="{{ img | append: '30-image29.png' | relative_url }}" alt="Provide a rule name. A description is not required.">
</figure>

Select your Elevation type. Because in this case you only allow a specific file or path you could set this setting to Automatic.

<figure>
  <img src="{{ img | append: '31-image30.png' | relative_url }}" alt="Select your Elevation type. Because in this case you only allow a specific file or path you could set this setting to Automatic.">
</figure>

Also the Child processes behavior can be allowed if you trust the process that you’re going to allow.

<figure>
  <img src="{{ img | append: '32-image31.png' | relative_url }}" alt="Also the Child processes behavior can be allowed if you trust the process that you’re going to allow.">
</figure>

Provide the File information. File name and File hash are required.

<figure>
  <img src="{{ img | append: '33-image32.png' | relative_url }}" alt="Provide the File information. File name and File hash are required.">
</figure>

You can get the file hash via Powershell with the command Get-FileHash

<figure>
  <img src="{{ img | append: '34-image33.png' | relative_url }}" alt="You can get the file hash via Powershell with the command Get-FileHash">
</figure>

Assign your rule to your users, devices or group(s).

Review and create your rule.

Now let’s check it on your user device. Right-click the installer Run with Elevated access. Your user will be able to install the application directly.

<figure>
  <img src="{{ img | append: '35-image34.png' | relative_url }}" alt="Now let’s check it on your user device. Right-click the installer Run with Elevated access. You user will get satisfied to install the ap...">
</figure>

<figure>
  <img src="{{ img | append: '36-image35.png' | relative_url }}" alt="Now let’s check it on your user device. Right-click the installer Run with Elevated access. You user will get satisfied to install the ap...">
</figure>

In the log files on the device you can see that the file path is successfully retrieved.

<figure>
  <img src="{{ img | append: '37-image36.png' | relative_url }}" alt="In the log files on the device you can see that the file path is successfully retrieved.">
</figure>

Thank you for reading this blog post. I hope it will help you to set up Endpoint Privilege Management.


