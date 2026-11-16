---
layout: post
title: "Setup Cloud PKI in Intune"
date: 2026-11-16 09:00:00 +0100
categories: [Intune, Security]
tags: [Intune, Cloud PKI, PKI, Security]
description: "In this blog I will explain how to setup Cloud PKI in Intune step-by-step."
---

{% assign img = '/assets/images/setup-cloud-pki-in-intune/' %}

In this blog I will explain how to setup Cloud PKI in Intune step-by-step. I certainly will not be the first one who will write about this. But now that Microsoft is adding this feature to your E5 license it’s a good idea to get a look into this.

See this blog post from Microsoft about the additions to licenses:

[Advancing Microsoft 365: New capabilities and pricing update | Microsoft 365 Blog](https://www.microsoft.com/en-us/microsoft-365/blog/2025/12/04/advancing-microsoft-365-new-capabilities-and-pricing-update/)

<figure>
  <img src="{{ img | append: '01-image1.png' | relative_url }}" alt="Advancing Microsoft 365: New capabilities and pricing update | Microsoft 365 Blog">
</figure>

Cloud PKI is a great way to make use of PKI without having to setup a complete infrastructure. It’s a PKI infrastructure in the cloud. And there is no need to maintain (on-premises) servers.

But keep in mind that this solution will only work for Intune managed devices.

There are some known issues and limitations. You can only create up to 6 CA’s in your Intune tenant. And Intune will only show to first 1000 issued certificates in the portal.

Login to your Intune Admin portal [https://intune.microsoft.com](https://intune.microsoft.com)

And navigate to Tenant Administration – Cloud PKI and click Create.

<figure>
  <img src="{{ img | append: '02-image2.png' | relative_url }}" alt="And navigate to Tenant Administration – Cloud PKI and click Create.">
</figure>

## Root CA

Create your Root CA first and provide the Basics.

<figure>
  <img src="{{ img | append: '03-image3.png' | relative_url }}" alt="Create your Root CA first and provide the Basics.">
</figure>

Select your CA type, you will need to start with creating your Root CA.

<figure>
  <img src="{{ img | append: '04-image4.png' | relative_url }}" alt="Select your CA type, you will need to start with creating your Root CA.">
</figure>

And select the Validity period.

<figure>
  <img src="{{ img | append: '05-image5.png' | relative_url }}" alt="And select the Validity period.">
</figure>

Select the Extended Key Usages. Be aware that you can’t change this anymore after you’ve created your Root CA.

<figure>
  <img src="{{ img | append: '06-image6.png' | relative_url }}" alt="Select the Extended Key Usages. Be aware that you can’t change this anymore after you’ve created your Root CA.">
</figure>

Provide the Subject attributes and select the Encryption Key size and algorithm click Next.

<figure>
  <img src="{{ img | append: '07-image7.png' | relative_url }}" alt="Provide the Subject attributes and select the Encryption Key size and algorithm click Next.">
</figure>

In the Review + create step you can check all your settings and you will also be warned once again that you can’t edit the CA after it’s created.

<figure>
  <img src="{{ img | append: '08-image8.png' | relative_url }}" alt="In the Review + create step you can check all your settings and you will also be warned once again that you can’t edit the CA after it’s ...">
</figure>

## Issuing CA

Now let’s create your Issuing CA. These steps will look the same. Once again click Create and provide your Basics.

<figure>
  <img src="{{ img | append: '09-image9.png' | relative_url }}" alt="Now let’s create your Issuing CA. These steps will look the same. Once again click Create and provide your Basics.">
</figure>

Select the CA type Issuing CA the Root CA source will be Intune in this case. When you select this option you will be able to select your Root CA you’ve created in the previous step and select a Validity period. This period can’t be longer than your Root CA.

<figure>
  <img src="{{ img | append: '10-image10.png' | relative_url }}" alt="Select the CA type Issuing CA the Root CA source will be Intune in this case. When you select this option you will be able to select your...">
</figure>

You can now select the Extended Key Usages you want to be able to be issued by this Issuing CA. You also can create multiple Issuing CA’s for different purposes.

<figure>
  <img src="{{ img | append: '11-image11.png' | relative_url }}" alt="You can now select the Extended Key Usages you want to be able to be issued by this Issuing CA. You also can create multiple Issuing CA’s...">
</figure>

Provide the Subject attributes and click Next. As you can see you can’t change this encryption. This has already been set with your Root CA.

<figure>
  <img src="{{ img | append: '12-image12.png' | relative_url }}" alt="Provide the Subject attributes and click Next. As you can see you can’t change this encryption. This has already been set with your Root CA.">
</figure>

In the Review + create step you can check all your settings and you will also be warned once again that you can’t edit the CA after it’s created.

<figure>
  <img src="{{ img | append: '13-image13.png' | relative_url }}" alt="In the Review + create step you can check all your settings and you will also be warned once again that you can’t edit the CA after it’s ...">
</figure>

Your Root CA en Issuing CA are now created and Active.

<figure>
  <img src="{{ img | append: '14-image14.png' | relative_url }}" alt="Your Root CA en Issuing CA are now created and Active.">
</figure>

You have now successfully setup your Cloud PKI environment within minutes.

You can use these certificates to distribute certificates to your users and clients. In the upcoming blog posts I will show you how to distribute certificates and where you can use them for.

