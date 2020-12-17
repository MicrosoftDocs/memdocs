---
title: Troubleshoot Windows Autopilot Azure AD join issues
description: Troubleshoot issues with Azure AD join issues during the Windows Autopilot deployment process.
keywords: mdm, setup, windows, windows 10, oobe, manage, deploy, autopilot, ztd, zero-touch, partner, msfb, intune
ms.reviewer: mniehaus
manager: laurawi
ms.technology: windows
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.date: 12/16/2020
ms.collection: M365-modern-desktop
ms.topic: troubleshooting
---


## Troubleshoot Azure AD join issues

**Applies to: Windows 10**

The most common issue joining a device to Azure AD is related to Azure AD permissions. Make sure that [the correct configuration is in place](configuration-requirements.md) to allow users to join devices to Azure AD. Errors can also happen if the user exceeds the number of devices that they're allowed to join. This limit is configured in Azure AD.

An Azure AD device is created upon import. It's important this object isn't deleted. The object acts as Autopilot's anchor in Azure AD for group membership and targeting (including the profile). Deleting it may lead to join errors. If this object is deleted, you can fix the issue by deleting and reimporting this autopilot hash so it can recreate the associated object.

Error code 801C0003 will typically be reported on an error page titled "Something went wrong". This error means that the Azure AD join failed.

## Related topics

[Windows Autopilot - known issues](known-issues.md)<br>
[Diagnose MDM failures in Windows 10](/windows/client-management/mdm/diagnose-mdm-failures-in-windows-10)<br>