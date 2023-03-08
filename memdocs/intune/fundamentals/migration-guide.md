---
# required metadata

title: Intune mobile device management migration guide
titleSuffix: Microsoft Intune
description: This overview includes a summary of the planning and deployment guides for Microsoft Intune.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 11/30/2022
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
#ms.custom:
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Deploy or move to Microsoft Intune

A successful adoption or migration to Microsoft Intune starts with a plan. This plan depends on your current mobile device management (MDM) environment, business goals, and technical requirements. Additionally, you need to include the key stakeholders who will support and collaborate with your plan.

We created some deployment guides to help plan your adoption or move to Intune.

## Before you begin

- Your Intune deployment might be different from a previous MDM deployment. Intune uses identity-driven access control. It doesn't require a network proxy to access organization data from devices outside your network.

  Review the [common ways to use Intune](common-scenarios.md).

- These guides assume you've evaluated Intune in a proof of concept (PoC) environment, and decided to use it as the MDM solution in your organization. You're familiar with Intune and its features.

## Deployment guides

- **Deployment plans and guides**: These guides cover several areas:

  - [Set up Intune](deployment-guide-intune-setup.md) and [drive end-user adoption with conditional access](migration-guide-drive-adoption.md): See your options when moving to Intune, or adopting Intune. Learn more about the advantages of using conditional access, and see a task list.

  - [Enroll devices](deployment-guide-enrollment.md): Use these guides to determine the best enrollment method for your devices. Get an overview of the admin tasks, and the end user tasks. The deployment enrollment guides cover the following areas:

    - [Mobile Application Management (MAM)](deployment-guide-enrollment-mamwe.md)
    - [Android](deployment-guide-enrollment-android.md)
    - [iOS/iPadOS](deployment-guide-enrollment-ios-ipados.md)
    - [macOS](deployment-guide-enrollment-macos.md)
    - [Windows](deployment-guide-enrollment-windows.md)

  - [Device and app management](migration-guide-configure-policies.md): Deploy a basic set of device configuration and compliance policies for users and devices. You can also deploy a specific set of apps used by your organization.
  - [App protection](../apps/app-protection-policies.md): For business line of business (LOB) apps that need an extra layer of protection, you can use app protection policies.

- **[Educate your users](end-user-educate.md)**: Get guidance on communicating with users about Company Portal app messages, getting apps, and the information Apple and Google send to Intune.

## Next steps

Start planning your Intune adoption using the [planning guide](intune-planning-guide.md).

Find the right [Intune setup](deployment-guide-intune-setup.md) for your organization.
