---
# required metadata

title: Policies for Office apps
titleSuffix: Microsoft Intune
description: Understand the policies available for Office apps.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/31/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: manchen
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: 
ms.collection:
- tier2
- M365-identity-device-management
---

# Policies for Office apps

Intune provides policies specifically for Microsoft Office apps. You can select specific options to create mobile app management policies for Office mobile apps that connect to Microsoft 365 services. There are many policies for Office apps that you can add to Microsoft Intune and apply to groups of end users.

Examples of just a few of the Office app policies include the following:
- Microsoft Word: *Turn off Protected View for attachments opened from Outlook*
- Microsoft Visio: *Block macros from running in Office files from the Internet*
- Microsoft Project: *Allow Trusted Locations on the network*
- Microsoft Publisher: *Publisher Automation Security Level*
- Microsoft PowerPoint: *Turn off Protected View for attachments opened from Outlook*

> [!NOTE]
> When you select to configure each specific app policy, additional policy details are provided. You can filter the Office policy list to quickly select the recommended **Security Baseline** policies.

You can also protect access to Exchange on-premises mailboxes by creating Intune app protection policies for Outlook for iOS/iPadOS and Android enabled with hybrid Modern Authentication. Before using this feature, you must meet the requirements for using the Office cloud policy service. App protection policies are not supported for other apps that connect to on-premises Exchange or SharePoint services. For related information, see [Overview of the Office cloud policy service for Microsoft 365 Apps for enterprise](/deployoffice/overview-office-cloud-policy-service).

## Prerequisites

You must meet the requirements to use policies for Office apps. For more information, see [Requirements for using the Office cloud policy service](/deployoffice/overview-office-cloud-policy-service#requirements-for-using-the-office-cloud-policy-service).

## To add an Office app policy

After you set up Intune for your organization, you can create an Office app policy.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Apps** > **Policies for Office apps** > **Create**.
3. Add the following values:
    - **Name:** Type a name (required) for your new policy.
    - **Description:** (Optional) Type a description.
    - **Select type:** Select how this policy configuration will be applied.
    - **Select group:** Select the group for this policy configuration.
    - **Configure policies:** Select the Office policy that you want to apply. You can sort the provided list based on policy, platform, application, recommendation, and status.
4. Select **Create**. The policy is created and appears in the table on the **Policy configurations** pane.

   > [!TIP]
   > The **Policy configurations** pane provides the **Health status** for each policy.

## Additional information

- [Overview of the Office cloud policy service for Microsoft 365 Apps for enterprise](/deployoffice/overview-office-cloud-policy-service)
- [Use policy settings to manage privacy controls for Microsoft 365 Apps for enterprise](/deployoffice/privacy/manage-privacy-controls)
- [Use preferences to manage privacy controls for Office for Mac](/deployoffice/privacy/mac-privacy-preferences)
- [Use preferences to manage privacy controls for Office on iOS devices](/deployoffice/privacy/ios-privacy-preferences)
- [Use policy settings to manage privacy controls for Office on Android devices](/deployoffice/privacy/android-privacy-controls)

## Next steps

- [Monitor app information and assignments with Microsoft Intune](apps-monitor.md)
