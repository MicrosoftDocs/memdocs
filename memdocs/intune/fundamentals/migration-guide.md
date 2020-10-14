---
# required metadata

title: Intune mobile device management migration guide - Azure | Microsoft Docs
titleSuffix: Microsoft Intune
description: This guide walks you through the various details involved in migrating from a third-party MDM provider to Microsoft Intune.
keywords:
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 10/13/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology:
ms.assetid: dcfc21f9-1bcd-4371-a46d-f2e18154ec50

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
#ms.custom:
ms.collection: M365-identity-device-management
---

# Deploy or move to Microsoft Intune

![Microsoft Intune MDM migration guide art](./media/migration-guide/MDM-migration-guide-art.PNG)

A successful migration to Microsoft Intune starts with a solid plan that factors in your current mobile device management (MDM) environment, business goals, and technical requirements. Additionally, you need to include the key stakeholders who will support and collaborate with your migration plan.

This guide walks you through the various details involved in migrating from a third-party MDM provider to Intune.

We created some deployment guides to help plan your adoption or move to Intune. These guides are living things. So, be sure to add tips and guidance you've found helpful. 

## Before you begin

- Your Intune deployment might be different from a previous MDM deployment. Unlike traditional MDM services, Intune centers on identity-driven access control. It doesn't require a network proxy appliance to control access to corporate data from mobile devices outside the organization's network perimeter. Microsoft offers solutions to secure data services within the cloud through a suite of tightly integrated cloud services, collectively referred to as the Enterprise Client + Security offering.

  Review the [common ways to use Intune](common-scenarios.md).

- These guides assume you've evaluated Intune in a proof of concept (PoC) environment, and decided to use it as the MDM solution in your organization. You're familiar with Intune and its features.

## What's included in these guides?

These guide breaks down the migration into two phases. Both include tasks, strategies, and guidance.

- **[Planning guide](intune-planning-guide.md)**: This guide includes recommendations, suggestions, and guidance on the different tasks associated with MDM solutions. For example, get guidance on:

  - Common objectives
  - Managing personal devices and desktop computers
  - Costs and licensing
  - Existing policies and group structures
  - Creating a rollout plan
  - Communicating changes with your users
  - Supporting your help desk

- **Deployment plans and guides**: These guides cover several areas:

  - [Set up Intune](deployment-guide-intune-setup.md): Get an overview of setting up Intune. Also see some recommendations if using a third party or partner MDM solution.
  - [Enroll devices](deployment-guide-enrollment.md): Use these guides to determine the best enrollment method for your devices. Get an overview of the admin tasks, and the end user tasks. There are deployment enrollment guides for [MAM-WE](deployment-guide-enrollment-mamwe.md), [Android](deployment-guide-enrollment-android.md), [iOS/iPadOS](deployment-guide-enrollment-ios-ipados.md), [macOS](deployment-guide-enrollment-macos.md), and [Windows](deployment-guide-enrollment-windows.md).
  - [Device and app management](migration-guide-configure-policies.md)
  - [App protection](../apps/app-protection-policies.md)
  - [Phase 2: Migration campaign](migration-guide-campaign.md)
    - [Communication plan](migration-guide-communication-plan.md)
    - [Drive end-user adoption with Conditional Access](migration-guide-drive-adoption.md)

- **[Educate your users](end-user-educate.md)**: Get guidance on communicating with users about Company Portal app messages, getting apps, and the information Apple and Google send to Intune.

## Next steps

[Setup Intune](deployment-guide-intune-setup.md)
