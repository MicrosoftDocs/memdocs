---
# required metadata

title: Windows Information Protection in Microsoft Intune
titleSuffix: Microsoft Intune
description: Learn about using Windows Information Protection with Microsoft Intune.
keywords:
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 04/08/2022
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
# optional metadata

#ROBOTS:
#audience:

ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
- Windows
- privacy
- sub-data-privacy
---

# Learn about Windows Information Protection and Microsoft Intune

[!INCLUDE [wip-deprecation](../../includes/wip-deprecation.md)]
<!-- MAXADO-6010051 -->

With the increase of employee-owned devices in the enterprise, there's also an increasing risk of accidental data leaks through apps and services, like email, social media, and the public cloud, which are outside of the enterprise's control. For example, an employee sends the latest engineering pictures from a personal email account, copies and pastes product info into a tweet, or saves an in-progress sales report to public cloud storage.

**Windows Information Protection** helps to protect against this potential data leakage without otherwise interfering with the employee experience. It also helps to protect enterprise apps and data against accidental data leaks on enterprise-owned devices and personal devices that employees bring to work without requiring changes to your environment or other apps.

You can use the Intune Windows Information Protection policy to manage the list of apps protected by Windows Information Protection, enterprise network locations, protection level, and encryption settings.

>[!NOTE]
> To use the Company Portal app with Windows Information Protection, you must add the Company Portal app under the Windows Information Protection mode of **Exempt**.

For more information, see:

- [Protect your enterprise data using Windows Information Protection](/windows/security/information-protection/windows-information-protection/protect-enterprise-data-using-wip).
- [Create a Windows Information Protection (WIP) policy using the Azure portal for Microsoft Intune](/windows/threat-protection/windows-information-protection/create-wip-policy-using-intune)
