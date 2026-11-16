---
layout: post
title: "Distribute your Cloud PKI certificates"
date: 2026-11-16 09:10:00 +0100
categories: [Intune, Security]
tags: [Intune, Cloud PKI, PKI, SCEP]
description: "Now head over to distribute your certificates to your devices with Intune."
---

{% assign img = '/assets/images/distribute-cloud-pki-certificates/' %}

Now head over to distribute your certificates to your devices with Intune. In the previous blog post we have created Cloud PKI.

Login to your Intune Admin portal [https://intune.microsoft.com](https://intune.microsoft.com)

And navigate to Tenant Administration – Cloud PKI

## Download the certificates

Select your Root CA and Download the certificate.

<figure>
  <img src="{{ img | append: '01-image1.png' | relative_url }}" alt="Select your Root CA and Download the certificate.">
</figure>

Select your Issuing CA and go to Properties to copy the SCEP URI and Download the certificate.

<figure>
  <img src="{{ img | append: '02-image2.png' | relative_url }}" alt="Select your Issuing CA and go to Properties to copy the SCEP URI and Download the certificate.">
</figure>

## Create Intune policies

Let’s headover to Device – Configuration

<figure>
  <img src="{{ img | append: '03-image3.png' | relative_url }}" alt="Let’s headover to Device – Configuration">
</figure>

Click Create – New Policy

<figure>
  <img src="{{ img | append: '04-image4.png' | relative_url }}" alt="Click Create – New Policy">
</figure>

## Trusted certificates

First we need to add the Trusted Certificates to Intune. Select Platform Windows 10 and later, select Profile type Templates and select Template name Trusted certificate.

<figure>
  <img src="{{ img | append: '05-image5.png' | relative_url }}" alt="First we need to add the Trusted Certificates to Intune. Select Platform Windows 10 and later, select Profile type Templates and select T...">
</figure>

Provide the basics for the certificate.

<figure>
  <img src="{{ img | append: '06-image6.png' | relative_url }}" alt="Provide the basics for the certificate.">
</figure>

Browse to your Root CA and select the Destination store Computer certificate store - Root for your Root CA.

<figure>
  <img src="{{ img | append: '07-image7.png' | relative_url }}" alt="Browse to your Root CA and select the Destination store Computer certificate store - Root for your Root CA.">
</figure>

On the Assignments page select the groups that you want to include.

<figure>
  <img src="{{ img | append: '08-image8.png' | relative_url }}" alt="On the Assignments page select the groups that you want to include.">
</figure>

Review your settings and Create.

Now repeat these steps again for your Intermediate, which is your Issuing CA. Provide the basics.

<figure>
  <img src="{{ img | append: '09-image9.png' | relative_url }}" alt="Now repeat these steps again for your Intermediate, which is your Issuing CA. Provide the basics.">
</figure>

Browse to your Issuing CA and select the Destination store Computer certificate store – Intermediate.

<figure>
  <img src="{{ img | append: '10-image10.png' | relative_url }}" alt="Browse to your Issuing CA and select the Destination store Computer certificate store – Intermediate.">
</figure>

On the assignment page select the groups that you want to include. Review your settings and Create.

## SCEP certificate

Now we need to create a SCEP certificate profile to deploy your certificates. Create a new policy select Platform Windows 10 and later, select Profile type Templates and select Template name SCEP certificate.

<figure>
  <img src="{{ img | append: '11-image11.png' | relative_url }}" alt="Now we need to create a SCEP certificate profile to deploy your certificates. Create a new policy select Platform Windows 10 and later, s...">
</figure>

Provide the basics.

<figure>
  <img src="{{ img | append: '12-image12.png' | relative_url }}" alt="Provide the basics.">
</figure>

You can now choose between a User or Device certificate. We will first create the User Certificate type. This user certificate will be useful for things like Wi-Fi, VPN or Certificated-based Authentication.

Select the Key Storage Provider (KSP), select the Key usage, we will select both Digital signature and Key encipherment, select your Key Size be aware that only Software KSP can be used with a 4096 key size and select the Hash alogorithm.

<figure>
  <img src="{{ img | append: '13-image13.png' | relative_url }}" alt="Select the Key Storage Provider (KSP), select the Key usage, we will select both Digital signature and Key encipherment, select your Key ...">
</figure>

Select your Root certificate.

<figure>
  <img src="{{ img | append: '14-image14.png' | relative_url }}" alt="Select your Root certificate.">
</figure>

You can now select the Trusted Certificates you’ve added in the previous step.

<figure>
  <img src="{{ img | append: '15-image15.png' | relative_url }}" alt="You can now select the Trusted Certificates you’ve added in the previous step.">
</figure>

Select the Extended key usage one of the predefined values. This will automatically fill in the Object identifier and paste the SCEP URI you’ve copied from the properties of your Issuing CA in SCEP Server URLs.

<figure>
  <img src="{{ img | append: '16-image16.png' | relative_url }}" alt="Select the Extended key usage one of the predefined values. This will automatically fill in the Object identifier and paste the SCEP URI ...">
</figure>

On the Assignments page select the groups that you want to include.

<figure>
  <img src="{{ img | append: '17-image8.png' | relative_url }}" alt="On the Assignments page select the groups that you want to include.">
</figure>

Review your settings and Create.

<figure>
  <img src="{{ img | append: '18-image17.png' | relative_url }}" alt="Review your settings and Create.">
</figure>

Now we will repeat these steps for a Device Certificate type.

Provide the Basics and go to Configuration settings.

Select Certificate type Device your Subject name format will be filled automatically.

Select your Root certificate. The rest you can copy from previous steps.

<figure>
  <img src="{{ img | append: '19-image18.png' | relative_url }}" alt="Select your Root certificate. The rest you can copy from previous steps.">
</figure>

The Microsoft Architecture in the situation will look like this.

<figure>
  <img src="{{ img | append: '20-image19.png' | relative_url }}" alt="The Microsoft Architecture in the situation will look like this.">
</figure>

Source of the information:

[https://learn.microsoft.com/en-us/intune/intune-service/protect/microsoft-cloud-pki-overview#architecture](https://learn.microsoft.com/en-us/intune/intune-service/protect/microsoft-cloud-pki-overview)

## Verify the certificate distribution

Now check the certificate distribution navigate to Tenant Administration – Cloud PKI and select your Issuing CA. Click View all certificates to see the issued certificates.

As you can see there are already 2 active issued certificates.

<figure>
  <img src="{{ img | append: '21-image20.png' | relative_url }}" alt="As you can see there are already 2 active issued certificates.">
</figure>

We have a user and a device certificate active.

<figure>
  <img src="{{ img | append: '22-image21.png' | relative_url }}" alt="We have a user and a device certificate active.">
</figure>

And you can check it on your users device if your certificate is deployed well also.

Open MMC and Add Certificate snap-in for Current User and/or Local Computer.

Your User certificate

<figure>
  <img src="{{ img | append: '23-image22.png' | relative_url }}" alt="Your User certificate">
</figure>

And your Computer certificate

<figure>
  <img src="{{ img | append: '24-image23.png' | relative_url }}" alt="And your Computer certificate">
</figure>

And your Root CA

<figure>
  <img src="{{ img | append: '25-image24.png' | relative_url }}" alt="And your Root CA">
</figure>

And Issuing CA created with the Trusted Certificate Configuration Profiles.

<figure>
  <img src="{{ img | append: '26-image25.png' | relative_url }}" alt="And Issuing CA created with the Trusted Certificate Configuration Profiles.">
</figure>

