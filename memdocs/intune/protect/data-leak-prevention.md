---
# required metadata

title: Prevent data leaks on non-managed devices
titleSuffix: Microsoft Intune
description: Allow access to corporate data on devices and protect data from data leaks using Microsoft Intune. 
keywords: data protection prevent leaks device M365 Microsoft 365
ms.author: dougeby
author: dougeby
manager: dougeby
ms.date: 01/02/2018
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology:
ms.assetid: b1512c3a-3bbd-4111-a0df-c874a0a335df

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: pchacon
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---
# Prevent data leaks on non-managed devices using Microsoft Intune

If you allow access to company data hosted by Microsoft 365, you can control how users share and save data without risking intentional or accidental data leaks. Microsoft Intune provides app protection policies that you set to secure your company data on user-owned devices. The devices do not need to be enrolled in the Intune service. 

App protection policies set up with Intune also work on devices managed with a non-Microsoft device management solution. The personal data on the devices is not touched; only company data is managed by the IT department. 

You can set app protection policies for Office mobile apps on devices running Windows, iOS/iPadOS, or Android to protect company data. These policies let you set policies such as app-based PIN or company data encryption, or more advanced settings to restrict how your cut, copy, paste, and save-as features are used by users between managed and unmanaged apps. You can also remotely wipe company data without requiring users enroll devices.

Intune app protection policies are independent of device management. App protection policies let you manage Office mobile apps on both unmanaged and Intune-managed devices, as well as device managed by non-Microsoft MDM solutions.

## Before you begin

The following action plan can be used when you meet the following requirements:

* Your company is ready to transition securely to the cloud.
* Your company uses Microsoft 365 Exchange Online, SharePoint Online, OneDrive for Business, or Yammer.
* Your company has licenses for Microsoft 365, Enterprise Mobility + Security (EMS), or Azure Information Protection.
* Your company allows users to access company data from company-owned or personally-owned Windows, iOS/iPadOS, or Android devices.
* Your company does not want to require enrollment of personally-owned devices in a device management service.

## Action plan

For iOS/iPadOS and Android devices:

1. Learn how [app protection policies](../apps/app-protection-policy.md) work.
2. Learn how to [create and deploy app protection policies](../apps/app-protection-policies.md) for Office mobile apps.
3. [Monitor the app protection policies](../apps/app-protection-policies-monitor.md) that you create and deploy.

For Windows 10/11 devices:

1. Learn [how Windows Information Protection (WIP) works](/windows/threat-protection/windows-information-protection/protect-enterprise-data-using-wip).
2. Get ready to configure [app protection policies for Windows 10/11](../apps/app-protection-policies-configure-windows-10.md).
3. [Create and deploy WIP app protection policies with Intune](../apps/windows-information-protection-policy-create.md).

## What to tell employees and students

As appropriate, share the following links to provide additional information:

* [Where to find work or school apps for iOS/iPadOS](../user-help/use-managed-apps-on-your-device-ios.md) 
* [Where to find work or school apps for Android](../user-help/use-managed-apps-on-your-device-android.md)

## Next steps

Want help enabling this or other EMS or Microsoft 365 scenarios? If you have at least 150 licenses for Microsoft 365, Enterprise Mobility + Security, or Azure Active Directory Premium, use your [FastTrack benefits](/enterprise-mobility-security/solutions/enterprise-mobility-fasttrack-program).