---
title: Reseller, distributor, or partner registration of Windows Autopilot devices
description: How partners add devices to Windows Autopilot
keywords: mdm, setup, windows, windows 10, oobe, manage, deploy, autopilot, ztd, zero-touch, partner, msfb, intune
ms.prod: windows-client
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 11/17/2022
ms.topic: how-to
ms.collection: 
  - M365-modern-desktop
  - m365initiative-coredeploy
ms.technology: itpro-deploy
---

# Reseller, distributor, or partner registration

*Applies to:*

- Windows 11
- Windows 10
- Windows Holographic, version 2004

Customers may purchase devices from resellers, distributors, or other partners. As long as these resellers, distributors, and partners are part of the [Cloud Solution Partners (CSP) program](https://partner.microsoft.com/cloud-solution-provider), they too can register devices for the customer. 

As with OEMs, CSP partners must be granted permission to register devices for an organization. This process is described in the [CSP authorization](registration-auth.md#csp-authorization) section of the Windows Autopilot customer consent article. In summary:
- The CSP partner requests a relationship with the organization. That organization's global administrator approves the request. 
- After the approval, CSP partners add devices using [Partner Center](https://partner.microsoft.com/pcv/dashboard/overview), either directly through the web site or via available APIs that can automate the same tasks.

For Surface devices, Microsoft Support can help with device registration.  For more information, see [Surface Registration Support for Windows Autopilot](/surface/surface-autopilot-registration-support).

Windows Autopilot doesn't require delegated administrator permissions when establishing the relationship between the CSP partner and the organization. As part of the global administrator's approval process, they can choose to uncheck the "Include delegated administration permissions" checkbox.

> [!Note]
> While resellers, distributors, or partners could boot each new Windows device to obtain the hardware hash (for purposes of providing them to customers or direct registration by the partner), this isn't recommended. Instead, these partners should register devices using the PKID information obtained from the device packaging (barcode) or obtained electronically from the OEM or upstream partner (e.g. distributor).

> [!Note]
> Partner Center does not have access to profiles created in Intune or Microsoft Store for Business. It only has access to the Autopilot profiles created through Partner Center.


**Also see**

[Registration overview](registration-overview.md)
