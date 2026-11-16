---
layout: post
title: "Temporary Access Pass"
date: 2025-12-18 10:44:00 +0100
categories: [Entra, Security]
tags: [Entra ID, Temporary Access Pass, Authentication methods, MFA]
description: "What is a Temporary Access Pass and when will it be useful?"
---

{% assign img = '/assets/images/temporary-access-pass/' %}

What is a Temporary Access Pass and when will it be useful? A Temporary Access Pass also known as TAP is a time-limited passcode. This code will also be seen as multi-factor authentication method. A key benefit to use this is for new users when they are required to provide MFA when enrolling a device. With TAP they can satisfy this MFA request. And it will be available for a short period of time.

## Configure Temporary Access Pass

Log in to your Entra Admin portal

Navigate to Authentication methods – Temporary Access Pass

<figure>
  <img src="{{ img | append: '01-image1.png' | relative_url }}" alt="Navigate to Authentication methods – Temporary Access Pass">
</figure>

Enable it and target it to All users or Select groups

<figure>
  <img src="{{ img | append: '02-image2.png' | relative_url }}" alt="Enable it and target it to All users or Select groups">
</figure>

You can also edit the preconfigured settings. I’ve kept it standard for now.

<figure>
  <img src="{{ img | append: '03-image3.png' | relative_url }}" alt="You can also edit the preconfigured settings. I’ve kept it standard for now.">
</figure>

## Create a Temporary Access Pass

Browse to Users select your user and Add authentication method to create TAP.

<figure>
  <img src="{{ img | append: '04-image4.png' | relative_url }}" alt="Browse to Users select your user and Add authentication method to create TAP.">
</figure>

Choose method – Temporary Access Pass

As you can see you can set a time limitation between 1 and 8 hours and you can set it as one-time use.

<figure>
  <img src="{{ img | append: '05-image5.png' | relative_url }}" alt="As you can see you can set a time limitation between 1 and 8 hours and you can set it as one-time use.">
</figure>

You can now see a Usable authentication method for this user.

<figure>
  <img src="{{ img | append: '06-image6.png' | relative_url }}" alt="You can now see a Usable authentication method for this user.">
</figure>

## Use a Temporary Access Pass User experience

Open a web browser and sign-in to a Microsoft portal for example [https://myaccount.microsoft.com](https://myaccount.microsoft.com) and enter the user’s email address.

<figure>
  <img src="{{ img | append: '07-image7.png' | relative_url }}" alt="Open a web browser and sign-in to a Microsoft portal for example https://myaccount.microsoft.com and enter the user’s email address.">
</figure>

In the setup step we’ve included All Users. This will result in the screen asking our test user to enter a Temporary Access Pass to get access.

<figure>
  <img src="{{ img | append: '08-image8.png' | relative_url }}" alt="In the setup step we’ve included All Users. This will result in the screen asking our test user to enter a Temporary Access Pass to get access.">
</figure>

After you’ve provided the TAP code your user will be directly logged in.


