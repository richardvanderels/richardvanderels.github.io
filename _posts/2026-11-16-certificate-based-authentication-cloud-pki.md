---
layout: post
title: "Certificated-based Authentication"
date: 2026-11-16 09:20:00 +0100
categories: [Entra, Security]
tags: [Entra ID, Certificate-based authentication, Cloud PKI, Conditional Access]
description: "In this next blog we will even go even further, and we will setup Certificated-based Authentication by the certificate distribution by your Cloud PKI."
---

{% assign img = '/assets/images/certificate-based-authentication-cloud-pki/' %}

In this next blog we will even go even further, and we will setup Certificated-based Authentication by the certificate distribution by your Cloud PKI.

In our second blog we’ve already downloaded the Root CA and Issuing CA. We will need that in the upcoming steps.

Some of the key benefits of Certificated-based Authentication is that is a phishing resistant MFA authentication method and it protects the accounts to work seamlessly with Entra ID Conditional Access policies.

<figure>
  <img src="{{ img | append: '01-image1.png' | relative_url }}" alt="Some of the key benefits of Certificated-based Authentication is that is a phishing resistant MFA authentication method and it protects t...">
</figure>

Login to your Entra Admin portal [https://entra.microsoft.com/](https://entra.microsoft.com/)

Go to Identity Secure Score – Public key infrastructure

<figure>
  <img src="{{ img | append: '02-image2.png' | relative_url }}" alt="Go to Identity Secure Score – Public key infrastructure">
</figure>

## Setup PKI

Click Create PKI

<figure>
  <img src="{{ img | append: '03-image3.png' | relative_url }}" alt="Click Create PKI">
</figure>

Provide a Display name

<figure>
  <img src="{{ img | append: '04-image4.png' | relative_url }}" alt="Provide a Display name">
</figure>

Open your newly created PKI by clicking the name of your PKI.

<figure>
  <img src="{{ img | append: '05-image5.png' | relative_url }}" alt="Open your newly created PKI by clicking the name of your PKI.">
</figure>

Choose Add certificate authority.

<figure>
  <img src="{{ img | append: '06-image6.png' | relative_url }}" alt="Choose Add certificate authority.">
</figure>

You will need to add your Root and Issuing CA also known as Intermediate.

We will first add the Root CA. Browse to your Root CA and add the Certificate revocation list URL. You can find this at the properties of the Root CA or Issuing CA in Intune – Cloud PKI. If the URL isn’t set revoked certificates don’t fail during authentication.

<figure>
  <img src="{{ img | append: '07-image7.png' | relative_url }}" alt="We will first add the Root CA. Browse to your Root CA and add the Certificate revocation list URL. You can find this at the properties of...">
</figure>

Also Adding the Issuing CA. But change the option is this certificate authority the root to No.

<figure>
  <img src="{{ img | append: '08-image8.png' | relative_url }}" alt="Also Adding the Issuing CA. But change the option is this certificate authority the root to No.">
</figure>

When you’ve added both Root and Issuing certificates you will see them in your Certificate Authority.

<figure>
  <img src="{{ img | append: '09-image9.png' | relative_url }}" alt="When you’ve added both Root and Issuing certificates you will see them in your Certificate Authority.">
</figure>

## Authentication methods

Before you will you start setting up the Authentication methods It’s good to have a group to target the Certificate-based authentication method.

Go to Authentication methods in your Entra Admin Center and select Certificate-based authentication.

<figure>
  <img src="{{ img | append: '10-image10.png' | relative_url }}" alt="Go to Authentication methods in your Entra Admin Center and select Certificate-based authentication.">
</figure>

Enable it and select groups – Add groups to add your group which Users who will be able to use Certificate-based authentication.

<figure>
  <img src="{{ img | append: '11-image11.png' | relative_url }}" alt="Enable it and select groups – Add groups to add your group which Users who will be able to use Certificate-based authentication.">
</figure>

Now Configure some settings. Enable Require CRL validation this will check the CRL for every CA. Enable Issuer Hints this will only show valid certificates during your users authentication.

<figure>
  <img src="{{ img | append: '12-image12.png' | relative_url }}" alt="Now Configure some settings. Enable Require CRL validation this will check the CRL for every CA. Enable Issuer Hints this will only show ...">
</figure>

Add rule to add your Certificate issuer.

<figure>
  <img src="{{ img | append: '13-image13.png' | relative_url }}" alt="Add rule to add your Certificate issuer.">
</figure>

And provide the authentication binding policy rules. Select Certificate issuer and select your CAs by PKI to be able to select your Issuing CA as Certificate issuer.

<figure>
  <img src="{{ img | append: '14-image14.png' | relative_url }}" alt="And provide the authentication binding policy rules. Select Certificate issuer and select your CAs by PKI to be able to select your Issui...">
</figure>

Let’s keep the rest of the settings default and Save.

<figure>
  <img src="{{ img | append: '15-image15.png' | relative_url }}" alt="Let’s keep the rest of the settings default and Save.">
</figure>

Acknowledge the warning before you can Save your actions.

<figure>
  <img src="{{ img | append: '16-image16.png' | relative_url }}" alt="Acknowledge the warning before you can Save your actions.">
</figure>

## Login with your user with a certificate

If you now open a Microsoft portal, for example [https://myaccount.microsoft.com](https://myaccount.microsoft.com) and login with a user that is assigned to the group for Certificate-based Authentication.

In this test case I will use an In Private browser session to not get logged in with your already approved MFA.

Fill in the username and click Next.

<figure>
  <img src="{{ img | append: '17-image17.png' | relative_url }}" alt="Fill in the username and click Next.">
</figure>

Instead of entering your Password click Sign in another way.

<figure>
  <img src="{{ img | append: '18-image18.png' | relative_url }}" alt="Instead of entering your Password click Sign in another way.">
</figure>

Choose the option Use a certificate or smart card.

<figure>
  <img src="{{ img | append: '19-image19.png' | relative_url }}" alt="Choose the option Use a certificate or smart card.">
</figure>

You will now see the available certificates. Because you set the option Issuer Hint you will only see valid options. Select your Certificate and click OK.

<figure>
  <img src="{{ img | append: '20-image20.png' | relative_url }}" alt="You will now see the available certificates. Because you set the option Issuer Hint you will only see valid options. Select your Certific...">
</figure>

When your certificate will be granted you will see. A request to stay signed in? If this is still configured in your tentant.

<figure>
  <img src="{{ img | append: '21-image21.png' | relative_url }}" alt="When your certificate will be granted you will see. A request to stay signed in? If this is still configured in your tentant.">
</figure>

Check the sign-in logs of the user to see that the user is certificate-based authenticated.

Go to Users – select your user – Sign-in logs

<figure>
  <img src="{{ img | append: '22-image22.png' | relative_url }}" alt="Go to Users – select your user – Sign-in logs">
</figure>

In Additional Details you can see the details of your certificate-based authentication.

<figure>
  <img src="{{ img | append: '23-image23.png' | relative_url }}" alt="In Additional Details you can see the details of your certificate-based authentication.">
</figure>

Is Legacy Store Used 0 means that PKI-based store is used. If the value indicates a 1 the classic or legacy store is used.

In the Authentication methods of your user, you can also see the System preferred multifactor authentication method.

<figure>
  <img src="{{ img | append: '24-image24.png' | relative_url }}" alt="In the Authentication methods of your user, you can also see the System preferred multifactor authentication method.">
</figure>

