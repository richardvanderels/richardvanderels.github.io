---
layout: post
title: "Cross-tenant synchronization setup"
date: 2026-11-23 09:00:00 +0100
categories: [Entra, Security]
tags: [Entra ID, Cross-tenant synchronization, B2B, External Identities]
description: "This blog describes how to configure cross-tenant synchronization settings."
---

{% assign img = '/assets/images/cross-tenant-synchronization-setup/' %}

This blog describes how to configure cross-tenant synchronization settings. With Cross-tenant synchronization you can automate the creation, updating and deleting of B2B accounts. This is useful when you manage 2 or more tenants and want to access them with just 1 single identity. Accounts need to automatically be provisioned to the target tenant.

<figure>
  <img src="{{ img | append: '01-image1.png' | relative_url }}" alt="This blog describes how to configure cross-tenant synchronization settings. With Cross-tenant synchronization you can automate the creati...">
</figure>

Source: [Cross-tenant synchronization overview - Microsoft Learn](https://learn.microsoft.com/en-gb/entra/identity/multi-tenant-organizations/cross-tenant-synchronization-overview)

## Setup

Everything we will do for this will be in the **Entra Admin Portal**.

We will start with the configuration of settings in our destination tenant.

It’s always good to set up a good baseline for your default cross-tenant settings.

We’ve configured the **External collaboration settings** to make it most restrictive.

Go to **External Identities** – **External collaboration settings**

<figure>
  <img src="{{ img | append: '02-image2.png' | relative_url }}" alt="Go to External Identities – External collaboration settings">
</figure>

Configure your settings to make it most restrictive.

<figure>
  <img src="{{ img | append: '03-image3.png' | relative_url }}" alt="Configure your settings to make it most restrictive.">
</figure>

And we’ve set **Collaboration restrictions** to only **Allow domains** that you’ve selected.

<figure>
  <img src="{{ img | append: '04-image4.png' | relative_url }}" alt="And we’ve set Collaboration restrictions to only Allow domains that you’ve selected.">
</figure>

After you’ve configured the default settings we will add an organization to the **External Identities**. Go to **External Identities** – **Cross-tenant access** settings and **Add organization**

<figure>
  <img src="{{ img | append: '05-image5.png' | relative_url }}" alt="After you’ve configured the default settings we will add an organization to the External Identities. Go to External Identities – ...">
</figure>

Provide the **domain name** or **tenantID** if it is another Microsoft cloud.

<figure>
  <img src="{{ img | append: '06-image6.png' | relative_url }}" alt="Provide the domain name or tenantID if it is another Microsoft cloud.">
</figure>

In the **Inbound settings** in de **Target** **tenant** we only have to configure to **Automatically redeem invitations with the tenant**.

<figure>
  <img src="{{ img | append: '07-image7.png' | relative_url }}" alt="In the Inbound settings in de Target tenant we only have to configure to Automatically redeem invitations with the tenant.">
</figure>

And in the Cross-tenant sync tab we will Allow user synchronization into this tenant.

<figure>
  <img src="{{ img | append: '08-image8.png' | relative_url }}" alt="And in the Cross-tenant sync tab we will Allow user synchronization into this tenant.">
</figure>

In the **Source tenant** we will setup the same **External Identities settings**. But in the organization, we will setup the **Oubound** **Access settings** to **Automatically redeem invitations with the tenant**.

<figure>
  <img src="{{ img | append: '09-image9.png' | relative_url }}" alt="In the Source tenant we will setup the same External Identities settings. But in the organization, we will setup the Oubound ...">
</figure>

Microsoft has made a Diagram for this. To see which settings you have to set in your **Source** and **Target tenant**.

<figure>
  <img src="{{ img | append: '10-image10.png' | relative_url }}" alt="Microsoft has made a Diagram for this. To see which settings you have to set in your Source and Target tenant.">
</figure>

Source: [Cross-tenant synchronization overview - Microsoft Learn](https://learn.microsoft.com/en-gb/entra/identity/multi-tenant-organizations/cross-tenant-synchronization-overview)

After we’ve configured the **External Identity settings** in **both** **tenants,** we will configure the **Cross-tenant synchronization settings** in the **Source tenant**.

<figure>
  <img src="{{ img | append: '11-image11.png' | relative_url }}" alt="After we’ve configured the External Identity settings in both tenants, we will configure the Cross-tenant synchronization s...">
</figure>

Provide a **Configuration name**

<figure>
  <img src="{{ img | append: '12-image12.png' | relative_url }}" alt="Provide a Configuration name">
</figure>

Set **Provisioning mode** to **Automatically** and provide the **TenantId**.

<figure>
  <img src="{{ img | append: '13-image13.png' | relative_url }}" alt="Set Provisioning mode to Automatically and provide the TenantId.">
</figure>

Because we sync only specific users, we will add a group with the users to Users and groups.

Now you can start **Provisioning**. When your provisioning is completed, you will see that the sync is completed.

<figure>
  <img src="{{ img | append: '14-image14.png' | relative_url }}" alt="Now you can start Provisioning. When your provisioning is completed, you will see that the sync is completed.">
</figure>

In the **destination** **tenant** you will now see the **provisioned user**. And you can assign access to this user.

As you can see, we now have our user Han Burger **provisioned** from our **Source tenant** via **Cross-Tenant synchronization** into our **Destination tenant Test**.

<figure>
  <img src="{{ img | append: '15-image15.png' | relative_url }}" alt="As you can see, we now have our user Han Burger provisioned from our Source tenant via Cross-Tenant synchronization into our ...">
</figure>

Hope this blog helped you with the set up of your **Cross-tenant Synchronization**



