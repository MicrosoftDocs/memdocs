---
# required metadata

title: Manage and secure apps in Endpoint Manager
titleSuffix: Microsoft Endpoint Manager
description: Learn more about the concepts and features you should know when managing apps that access organization resources in Microsoft Intune and Endpoint Manager. You can manage new and existing devices, including BYOD personal devices, check health compliance and view reports, configure device features, and secure devices using mobile threat solutions.
keywords:
author: MandiOhlinger
  
ms.author: mandia
manager: dougeby
ms.date: 08/18/2022
ms.topic: conceptual
ms.service: mem
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 
# optional metadata
 
#audience:
#ms.devlang:
ms.reviewer:
ms.suite: ems
search.appverid:
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
  - M365-identity-device-management
---

# Manage your apps and app data in Microsoft Endpoint Manager

> [!NOTE]
> This is a draft of an idea. It's meant to be 100-level with an introduction to some concepts that decision makers need to be aware.

app protect policies require Azure AD

## Deploy apps your organization uses

Update already deployed apps

## Configure apps before they're installed


## Protect apps on organization owned and personal devices

## Update apps to the latest version

app protection policies

different levels of app protection

[App protection policies overview and benefits](./intune/apps/app-protection-policy.md)

mobile application management (MAM) defines policies on apps, not devices or users. When users are within an app, you can create policies that block features, such as copy-and-paste.

Android uses Google Mobile Services for apps

Intune marks all data in the app as either "corporate" or "personal." Data is considered "corporate" when it originates from a business location. For the Office apps, Intune considers the following as business locations: email (Exchange) or cloud storage (OneDrive app with a OneDrive for Business account).

Selective wipe for MAM simply removes company app data from an app

Add store apps, line-of-business apps, web apps, built-in Intune apps

Use CP app to add more apps

MDM or MAM or both

license apps from the platform stores, such 

Selective wipe for MAM simply removes company app data from an app

## Next steps

- [Manage identities](manage-identities.md)
- [Manage devices](manage-devices.md)
