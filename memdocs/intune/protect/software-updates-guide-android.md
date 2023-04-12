---
title: Admin checklist for Android software updates in Microsoft Intune
description: Guidance and advice for administrators that create and manage software updated for Android devices using Microsoft Intune. See sample policy for different industry scenarios, including shared devices, kiosk, manufacturing, and information worker.
ms.author: mandia
author: MandiOhlinger
manager: dougeby
ms.date: 04/12/2023
audience: ITPro
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high

# optional metadata

#ROBOTS:

ms.reviewer: ahamil, talima, brenduns
ms.suite: ems
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
---

# Software updates admin checklist and scenarios for Android devices in Microsoft Intune

In today's rapid pace of modern device management, patches, major and minor updates, and new operating system versions are released frequently. Keeping your devices up to date is incredibly important for many reasons, namely security, compatibility, and new functionality. Microsoft Intune helps you structure and plan your update management strategy for Android. Android GMS (Google Mobile Services) devices include all the Google Apps and services on top of the OEMs own firmware set of features and flavor. These devices receive different type of updates more or less frequently depending on a series of factors and players, including Google, OEM, and Carriers/Telcos. This article will help you better understand how Android GMS devices updates work, how important it is to plan and roll out updates, and how Microsoft Endpoint Manager can help with that. 

This article applies to:

- Android devices

## Scenarios

Most Android use cases in organizations fall into one of the following scenarios:  

- Personal/BYOD (Android Enterprise Personally Enabled, Mobile Application Management)
- Android Enterprise Corporate (Dedicated, Fully Managed, Fully Managed with a Work Profile)

  - **1:1**: Devices are used by only one person.
  - **Shared**: Devices are used by more than one person.
  - **Dedicated**: Devices are used for a specific business purpose, like a kiosk or digital signage. Not assigned to a specific user.

Typically, organizations also have devices that require the following: 

- OEM Config
- Over-the-air (OTA) updates

We'll get into details for each of scenarios mentioned throughout this article.

## BYOD and personally-owned devices

Users can enroll their personal Android devices in Microsoft Intune. When they enroll, these personal or bring-your-own-devices (BYOD) get a work profile. You create policies that apply to the work profile.

✔️ **Create enrollment restrictions**

You can create an enrollment restrictions policy that requires a minimum and maximum operating system version:

:::image type="content" source="./media/software-updates-guide-android/android-enrollment-restrictions-policy.png" alt-text="Screenshot that shows enrollment restrictions policy for Android devices in the Microsoft Intune admin center.":::

When users enroll their personal devices, the policy requires users update their OS versions to the versions you want. When you require a minimum and maximum OS version, you also have version consistency and up-to-date devices.

✔️ **Create compliance policies**

While MDM enrolment restrictions are helpful for when the device first enrolls, Compliance policies are a great resource to help with keeping those devices up to date. You can mark a device as non-complaint if it has not been upgraded to a version you defined. When devices are non-compliant, users lose access to corporate resources until they upgrade. You can notify the user and allow a grace period before you mark the device as non-complaint, to allow them some time to perform the upgrade. In addition, you can leverage Conditional Access in conjunction with the Compliance status to determine access. 

:::image type="content" source="./media/software-updates-guide-android/compliance-policy-actions-noncompliance.png" alt-text="Screenshot that shows compliance policy and actions for noncompliance in the Microsoft Intune admin center.":::

✔️ **Use app protection policies**

If you are leveraging App Protection Policies (MAM) in your environment, you can also take advantage of its capabilities to determine the minimum operating system and patch versions at the app level. When you do so, users are prompted to upgrade the operating system when they launch or resume a managed app. You can either simply warn the user, or block access entirely, if the version they are running does not met your criteria.  

:::image type="content" source="./media/software-updates-guide-android/app-protection-policy-device-conditions.png" alt-text="Screenshot that shows device-based conditions in an app protection policy in the Microsoft Intune admin center.":::

In scenarios where OS update cannot be forced or controlled, such as personal devices, you may need to rely on the end users to perform the upgrade. You should leverage any existing communications team/process you may have, and in addition, you can leverage Intune Custom Notifications to alert the users to an upcoming OS version requirement and guide them to proactively update so they don't lose access.  

:::image type="content" source="./media/software-updates-guide-android/custom-notification.png" alt-text="Screenshot that shows a custom notification message in the Microsoft Intune admin center.":::


