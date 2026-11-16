---
layout: post
title: "Intune Enterprise Application Management"
date: 2026-07-07 13:57:00 +0200
categories: [Intune]
tags: [Intune, Enterprise App Catalog, Win32 apps, Windows]
description: "Microsoft Intune Enterprise App Management enables you to easily discover and deploy applications and keep them up to date from the Enterprise App Catalog."
---

{% assign img = '/assets/images/intune-enterprise-application-management/' %}

## What is Enterprise Application Management?

Microsoft Intune Enterprise App Management enables you to easily discover and deploy applications and keep them up to date from the Enterprise App Catalog. The Enterprise App Catalog is a collection of prepared Microsoft and non-Microsoft applications. These apps are Win32 apps that are prepared as Win32 apps and hosted by Microsoft.

[Microsoft Intune Enterprise Application Management - Microsoft Intune | Microsoft Learn](https://learn.microsoft.com/en-us/intune/app-management/deployment/enterprise-app-management)

## Configuration

How to configure it. We don’t need to configure that much. If you have a Microsoft 365 E5 license this feature is included for you.

Go to your Intune Admin Center – Apps – Create – Enterprise App Catalog app

<figure>
  <img src="{{ img | append: '01-image1.png' | relative_url }}" alt="Go to your Intune Admin Center – Apps – Create – Enterprise App Catalog app">
</figure>

Search for an available app that you want to publish.

<figure>
  <img src="{{ img | append: '02-image2.png' | relative_url }}" alt="Search for an available app that you want to publish.">
</figure>

There is a great list of applications that are available.

<figure>
  <img src="{{ img | append: '03-image3.png' | relative_url }}" alt="There is a great list of applications that are available.">
</figure>

Select the configuration of this app. If there is more than one version available you could select the version of your choice.

<figure>
  <img src="{{ img | append: '04-image4.png' | relative_url }}" alt="Select the configuration of this app. If there is more than one version available you could select the version of your choice.">
</figure>

## Automatically update

There are two options Automatically update and with Supersedence. With Automatically update you will keep the app up-to-date automatically. If you select Update with supersedence you can customize settings and it will create the latest version of the selected application.

<figure>
  <img src="{{ img | append: '05-image5.png' | relative_url }}" alt="There are two options Automatically update and with Supersedence. With Automatically update you will keep the app up-to-date automaticall...">
</figure>

With Intune Enterprise Application Management you don’t have to package every new version of your third party applications anymore.

If you have selected Automatically update, you can’t change the application package afterwards.

Some features are greyed out when you’ve selected Automatically update, because these options have been selected for you.

<figure>
  <img src="{{ img | append: '06-image6.png' | relative_url }}" alt="Some features are greyed out when you’ve selected Automatically update, because these options have been selected for you.">
</figure>

You can only assign your application Required to your Groups, Users or Devices.

<figure>
  <img src="{{ img | append: '07-image7.png' | relative_url }}" alt="You can only assign your application Required to your Groups, Users or Devices.">
</figure>

Review and create your application.

<figure>
  <img src="{{ img | append: '08-image8.png' | relative_url }}" alt="Review and create your application.">
</figure>

## Update with supersedence

Using the option Update with supersedence is a great way to update your manually packaged applications and you get the ability to configure a lot of settings. You can first deploy it to a selected group. You will need to create a new package for every version.

<figure>
  <img src="{{ img | append: '09-image9.png' | relative_url }}" alt="Using the option Update with supersedence is a great way to update your manually packaged applications and you get the ability to configu...">
</figure>

Configure your program settings. You can add specific install commands.

<figure>
  <img src="{{ img | append: '10-image10.png' | relative_url }}" alt="Configure your program settings. You can add specific install commands.">
</figure>

In the Requirements section you can specify the system architecture. In my case to be able to deploy it to ARM64 systems.

<figure>
  <img src="{{ img | append: '11-image11.png' | relative_url }}" alt="In the Requirements section you can specify the system architecture. In my case to be able to deploy it to ARM64 systems.">
</figure>

Detection rules are already preconfigured for you. And you can add custom options if you want.

<figure>
  <img src="{{ img | append: '12-image12.png' | relative_url }}" alt="Detection rules are already preconfigured for you. And you can add custom options if you want.">
</figure>

You can add the app that you want to supersede.

<figure>
  <img src="{{ img | append: '13-image13.png' | relative_url }}" alt="You can add the app that you want to supersede.">
</figure>

With this option you can assign the application Available for enrolled devices to let your users install the application from the Company Portal only if they need it.

<figure>
  <img src="{{ img | append: '14-image14.png' | relative_url }}" alt="With this option you can assign the application Available for enrolled devices to let your users install the application from the Company...">
</figure>

You now have created the latest version of the application you’ve selected as a Win32 app.

<figure>
  <img src="{{ img | append: '15-image15.png' | relative_url }}" alt="You now have created the latest version of the application you’ve selected as a Win32 app.">
</figure>

You can see that the application can update itself.

<figure>
  <img src="{{ img | append: '16-image16.png' | relative_url }}" alt="You can see that the application can update itself.">
</figure>

Now check your device to see if it has been installed. If

<figure>
  <img src="{{ img | append: '17-image17.png' | relative_url }}" alt="Now check your device to see if it has been installed. If">
</figure>

In Intune you will see it’s installed on your device.

<figure>
  <img src="{{ img | append: '18-image18.png' | relative_url }}" alt="In Intune you will see it’s installed on your device.">
</figure>

## Wrap up

The big difference between Automatically Update and Update with Supersedence is that Automatically Update directly updates to the latest version and without any options to change settings. Where Update with Supersedence gives you the ability to create a new package for every version, change settings and do a pilot.

So if you’re using Microsoft 365 E5 licenses why don’t you try it!


