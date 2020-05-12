---
# required metadata

title: Windows Information Protection settings in Microsoft Intune
titleSuffix: Microsoft Intune
description: Learn about the Microsoft Intune settings you can use to manage Windows Information Protection.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/18/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# How to configure Windows Information Protection in Microsoft Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

With the increase of employee-owned devices in the enterprise, there's also an increasing risk of accidental data leaks through apps and services, like email, social media, and the public cloud, which are outside of the enterprise's control. For example, an employee sends the latest engineering pictures from a personal email account, copies and pastes product info into a tweet, or saves an in-progress sales report to public cloud storage.

**Windows Information Protection** helps to protect against this potential data leakage without otherwise interfering with the employee experience. It also helps to protect enterprise apps and data against accidental data leaks on enterprise-owned devices and personal devices that employees bring to work without requiring changes to your environment or other apps.

This Intune policy manages the list of apps protected by Windows Information Protection, enterprise network locations, protection level, and encryption settings.

>[!NOTE]
> To use the Windows 10 Company Portal app with Windows Information Protection, you must add the Company Portal app under the Windows Information Protection mode of **Exempt**. 

For more information, see:
- [Protect your enterprise data using Windows Information Protection](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip).
- [Create a Windows Information Protection (WIP) policy using the classic console for Microsoft Intune](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/create-wip-policy-using-intune)
- [Create a Windows Information Protection (WIP) policy with MDM using the Azure portal for Microsoft Intune](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/create-wip-policy-using-intune-azure)
- [Create a Windows Information Protection (WIP) policy with MAM using the Azure portal for Microsoft Intune](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/create-wip-policy-using-mam-intune-azure)
