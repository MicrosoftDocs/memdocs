---
# required metadata

title: Manage access to Exchange without device management
titleSuffix: Microsoft Intune
description: Use Microsoft Intune to give employees access to their Microsoft 365 Exchange Online email without setting up a device management system.
keywords: Microsoft 365 Exchange email access
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/07/2024
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.topic: archived
ms.assetid: 88a0d3b9-2622-403b-8374-1396afd8066e

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: demerson
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
- sub-device-compliance
---

# Protect Microsoft 365 Exchange Online without requiring device management

When you use Microsoft Intune, you can still manage employee access to their work email through Microsoft 365 Exchange Online without the overhead of enrolling their devices. This limited access through Exchange Online for unenrolled devices can be accomplished using app-based Conditional Access policies.

To complete the necessary steps, confirm you have licenses for Microsoft 365, or Microsoft Entra ID P1 and Intune. Employees need to have a [supported iOS/iPadOS or Android device](../fundamentals/supported-devices-browsers.md).

If you decide to set up a device management system, you can as this type of app protection works independently of device management.

## Action plan

1. [Learn about Conditional Access](conditional-access.md).
2. [Learn about app-based Conditional Access](app-based-conditional-access-intune.md).
3. [Set up app-based Conditional Access policies for Exchange Online](app-based-conditional-access-intune-create.md).
4. [Block apps that can't be managed](app-modern-authentication-block.md). Specifically, block apps that don't use the Microsoft Authentication Library (MSAL).
5. (Optional) [Set up app-based Conditional Access policies for SharePoint Online](app-based-conditional-access-intune-create.md). These policies block access to your company data from apps that can't be managed and secured. The policies also limit access through SharePoint mobile.

## What to tell employees and students

- Ask your employees and students to download and install Microsoft Outlook or Microsoft SharePoint for iOS/iPadOS from the Apple App Store or for Android from the Google Play Store.
- If you block access to apps that don't use modern authentication, let the employees and students know of this restriction.

## Next steps

You have used app-based Conditional Access to increase the security of company data. As part of next steps, you can learn more about the other ways you can increase the protection of your company's data, including:

- Setting up app protection policies to help you protect your company data against intentional or unintentional data leaks.
- Use of Azure Information Protection to protect company data outside your network.

Want help with enabling this or other EMS or Microsoft 365 scenarios? If you have at least 150 licenses for Microsoft 365, Enterprise Mobility + Security, or Microsoft Entra ID P1, use your [FastTrack benefits](/enterprise-mobility-security/solutions/enterprise-mobility-fasttrack-program).
