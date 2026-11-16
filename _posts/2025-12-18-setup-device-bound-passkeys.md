---
layout: post
title: "Setup Device-bound passkeys"
date: 2025-12-18 08:48:00 +0100
categories: [Entra, Security]
tags: [Entra ID, Passkeys, FIDO2, Authenticator, Security]
description: "How to prepare your environment to enable device-bound passkeys."
---

{% assign img = '/assets/images/setup-device-bound-passkeys/' %}

How to prepare your environment to enable device-bound passkeys. But first what are device-bound passkeys and what are the benefits.

Passkeys are resistant to phishing attacks because they rely on physical possession of a device rather than passwords, which can be guessed and entered by anyone on any device. Even if you did fall victim to a phishing attempt when using a passkey, the attacker would still need the physical passkey (which is only stored on your device) to access your account.

As I didn’t have an Android device at this moment, I’ve only done the setup for an iOS device. But the steps in the Authenticator app will look the same.

## Prepare your environment

Go to your Entra Admin Portal [https://entra.microsoft.com/](https://entra.microsoft.com/)

Navigate to Authentication methods – Passkey (FIDO2)

<figure>
  <img src="{{ img | append: '01-image1.png' | relative_url }}" alt="Navigate to Authentication methods – Passkey (FIDO2)">
</figure>

You can enable it for All Users or Selected groups.

<figure>
  <img src="{{ img | append: '02-image2.png' | relative_url }}" alt="You can enable it for All Users or Selected groups.">
</figure>

Enable the following settings.

Allow self-service set up. This allows users to set up their passkey.

Enforce key restriction. This option will only allow the restricted keys.

Restrict specific keys will let you select which keys you will allow or block. Select Microsoft Authenticator to add the AAGUID for both Android and iOS Authenticator apps.

Enforce key restrictions to No to allow users to register any supported passkey, including passkey registration directly in the Authenticator app. If you set Enforce key restrictions to Yes and already have active passkey usage, you should collect and add the AAGUIDs of the passkeys being used today.

<figure>
  <img src="{{ img | append: '03-image3.png' | relative_url }}" alt="Enforce key restrictions to No to allow users to register any supported passkey, including passkey registration directly in the Authentic...">
</figure>

## Prerequisites

Before your users can enroll passkeys your users’ devices need to have some minimum requirements. Android 14 and later or iOS 17 and later. And the latest Microsoft Authenticator application needs to be installed.

## End User enrollment of passkeys on iOS

Log in to your Security info portal [https://mysignins.microsoft.com/security-info](https://mysignins.microsoft.com/security-info) or shorten [https://aka.ms/mysecurityinfo](https://aka.ms/mysecurityinfo)

Add sign-in method and select Passkey in Microsoft Authenticator

<figure>
  <img src="{{ img | append: '04-image4.png' | relative_url }}" alt="Add sign-in method and select Passkey in Microsoft Authenticator">
</figure>

Select Next

<figure>
  <img src="{{ img | append: '05-image5.png' | relative_url }}" alt="Select Next">
</figure>

Now you need to run the steps on your mobile device.

Open the Authenticator App and select + to Add an authentication method.

<figure>
  <img src="{{ img | append: '06-image6.png' | relative_url }}" alt="Open the Authenticator App and select + to Add an authentication method.">
</figure>

Select Work or School account. My apologies for the Dutch screenshots in the Authenticator app screenshots on my mobile device.

<figure>
  <img src="{{ img | append: '07-image7.png' | relative_url }}" alt="Select Work or School account. My apologies for the Dutch screenshots in the Authenticator app screenshots on my mobile device.">
</figure>

Choose the option Sign-In when you don’t have a QR code to scan on your laptop.

<figure>
  <img src="{{ img | append: '08-image8.png' | relative_url }}" alt="Choose the option Sign-In when you don’t have a QR code to scan on your laptop.">
</figure>

Sign-In with your account and provide your Username and Password.

In the next screen you will see what will be created and click Next.

<figure>
  <img src="{{ img | append: '09-image9.png' | relative_url }}" alt="In the next screen you will see what will be created and click Next.">
</figure>

Your passkey will be created. And look at the nice Dutch word wachtwoordsleutel

<figure>
  <img src="{{ img | append: '10-image10.png' | relative_url }}" alt="Your passkey will be created. And look at the nice Dutch word wachtwoordsleutel">
</figure>

Register your device to be able to use passwordless sign-in. You can also skip this for the setting up your passkey.

<figure>
  <img src="{{ img | append: '11-image11.jpeg' | relative_url }}" alt="Register your device to be able to use passwordless sign-in. You can also skip this for the setting up your passkey.">
</figure>

When you’re done you will see that your account is added.

<figure>
  <img src="{{ img | append: '12-image12.png' | relative_url }}" alt="When you’re done you will see that your account is added.">
</figure>

After you’ve finished the steps on your mobile device you can go back to your laptop and finish the steps. When everything has gone well you will see this screen.

<figure>
  <img src="{{ img | append: '13-image13.png' | relative_url }}" alt="After you’ve finished the steps on your mobile device you can go back to your laptop and finish the steps. When everything has gone well y...">
</figure>

Or if you already have registered the account with your Authenticator directly go to your Authenticator App and open your account.

Click create passkey.

<figure>
  <img src="{{ img | append: '14-image14.png' | relative_url }}" alt="Click create passkey.">
</figure>

Click Sign-in to create your passkey.

<figure>
  <img src="{{ img | append: '15-image15.png' | relative_url }}" alt="Click Sign-in to create your passkey.">
</figure>

Provide your Username and Password.

<figure>
  <img src="{{ img | append: '16-image16.png' | relative_url }}" alt="Provide your Username and Password.">
</figure>

Your passkey will be created.

<figure>
  <img src="{{ img | append: '17-image10.png' | relative_url }}" alt="Your passkey will be created.">
</figure>

Your passkey is created.

<figure>
  <img src="{{ img | append: '18-image17.png' | relative_url }}" alt="Your passkey is created.">
</figure>

## Sign-In with passkey

Your user can sign-in with the passkey. Log in to [https://myaccount.microsoft.com](https://myaccount.microsoft.com) for example.

Choose a way to sign-in and select Face, fingerprint, PIN or security key.

<figure>
  <img src="{{ img | append: '19-image18.png' | relative_url }}" alt="Choose a way to sign-in and select Face, fingerprint, PIN or security key.">
</figure>

Choose a passkey and select iPhone, iPad, or Android device

<figure>
  <img src="{{ img | append: '20-image19.png' | relative_url }}" alt="Choose a passkey and select iPhone, iPad, or Android device">
</figure>

Scan the QR code with your mobile device.

<figure>
  <img src="{{ img | append: '21-image20.png' | relative_url }}" alt="Scan the QR code with your mobile device.">
</figure>

Sign in with passkey

<figure>
  <img src="{{ img | append: '22-image21.png' | relative_url }}" alt="Sign in with passkey">
</figure>

Your user is now signed in with his passkey.

In the user’s Security info, you can see that the passkey (device-bound) has been setup.

<figure>
  <img src="{{ img | append: '23-image22.png' | relative_url }}" alt="In the user’s Security info, you can see that the passkey (device-bound) has been setup.">
</figure>

## Microsoft sources for this documentation

Enable passkeys in Entra ID:

[Enable passkeys in Authenticator for Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn](https://learn.microsoft.com/en-us/entra/identity/authentication/how-to-enable-authenticator-passkey)

Register passkeys on your device:

[Register a Passkey (FIDO2) - Microsoft Entra ID | Microsoft Learn](https://learn.microsoft.com/en-us/entra/identity/authentication/how-to-register-passkey)

[Register a passkey using a mobile device - Microsoft Entra ID | Microsoft Learn](https://learn.microsoft.com/en-us/entra/identity/authentication/how-to-register-passkey-mobile?tabs=iOS)



