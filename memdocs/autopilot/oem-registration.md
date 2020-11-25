---
title: OEM registration
ms.reviewer: 
manager: laurawi
description: How to add devices to Windows Autopilot
keywords: mdm, setup, windows, windows 10, oobe, manage, deploy, autopilot, ztd, zero-touch, partner, msfb, intune
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.topic: how-to
ms.collection: 
- M365-modern-desktop
- m365initiative-coredeploy
---

# OEM registration

**Applies to**

- Windows 10
- Windows Holographic, version 2004

When you purchase devices from an OEM, that OEM can automatically register the devices with the Windows Autopilot. For the list of OEMs that support registration, see the "Participant device manufacturers and resellers" section of the [Windows Autopilot page](https://aka.ms/windowsautopilot).

Before an OEM can register devices for an organization, the organization must grant the OEM permission to do so. The OEM starts this process, with approval granted by an Azure AD global administrator from the organization. See the "Customer Consent" section of the [Customer consent page](registration-auth.md#oem-authorization).

> [!Note]
> While the hardware hashes (also known as hardware IDs) are generated as part of the OEM device manufacturing process, these should not be provided directly to customers or CSP partners. Instead, the OEM should register devices on the customer's behalf. In cases where devices are being registered by CSP partners, OEMs may provide PKID information to those partners to support the device registration process.
