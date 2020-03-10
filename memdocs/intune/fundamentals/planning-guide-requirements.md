---
# required metadata

title: Determine use-case scenario requirements
titleSuffix: Microsoft Intune
description: This article helps you determine Intune use-case, and sub-use-case scenario requirements for an Microsoft Intune cloud-only implementation.
keywords:
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 01/02/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology:
ms.assetid: fd8cb5f7-19f0-4d80-8825-2bafa49624af

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: jeffbu, cgerth
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-classic
ms.collection: M365-identity-device-management
---

# Determine use-case scenario requirements

In this section, you determine the requirements for each organizational group within each use-case scenario. This process helps you prepare for the other Intune deployment planning areas like architecture and design, onboarding, and rollout. It can also help identify potential gaps and challenges related to your Intune deployment project.

You might have different sets of requirements for each of your use-case and sub-use-case scenarios, and their associated organizational groups and mobile device platforms. For example, your corporate use-case scenario requirements might require devices to enroll into Intune with a more restrictive set of device settings, like a PIN of 6 characters or disabled cloud backup. Your "bring your own device" (BYOD) use-case scenario, may be less restrictive and allow a 4-character PIN and cloud backup.

You may also have organizational groups for the corporate use-case scenario that have different sets of requirements (for example, PIN settings, Wi-Fi or VPN profile, apps deployed). Your requirements may also be determined by the capabilities of the mobile device platform (for example, finger print reader, email profile).

Here are a few examples of an organization’s use-case requirements showing different sets of requirements for each use-case and sub-use-case scenario, organizational group, and mobile device platform. You can also use the following table to enter your organization’s use-case requirements:

| **Use cases** | **Sub-use cases** | **Groups** | **Device platforms** | **Requirements** |
|:---:|:---:|:---:|:---:|:---:|
| Corporate | Information worker | HR, Finance | iOS/iPadOS | Secure e-mail, device settings, profiles, apps |                                                          
| Corporate | Executives | HR, Finance | iOS/iPadOS | Secure e-mail, device settings, profiles, apps |                                                         
| Corporate | Kiosk | Retail | Android | Device settings, profiles, apps |
| BYOD | Information worker | Marketing, Sales | iOS/iPadOS | Secure e-mail, device settings, profiles, apps |                                                         
| BYOD | Executives | Marketing, Sales | iOS/iPadOS | Secure e-mail, device settings, profiles, apps |

You can [download a template of the above table](https://gallery.technet.microsoft.com/Intune-deployment-planning-fae156c2?redir=0) to enter your organization’s use-case and sub-use-case requirements.


## Examples of requirements

Here are a few more examples that can be used in the "Requirements" column:

- **Secure e-mail**
  - Conditional Access for Exchange Online / on-premises
  - Outlook app protection policies

- **Device settings**
  - PIN setting with four, six characters
  - Restrict cloud backup

- **Profiles**
  - Wi-Fi
  - VPN
  - Email (Windows 10 mobile)

- **Apps**
  - Office 365 with app protection policies
  - Line of business (LOB) with app protection policies

## Next steps

The next section provides guidance on [how to develop an Intune rollout plan](planning-guide-rollout-plan.md).
