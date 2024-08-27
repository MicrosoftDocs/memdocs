---
# required metadata

title: Create Mobile Threat Defense (MTD) app protection policy with Intune
titleSuffix: Microsoft Intune
description: Create Mobile Threat Defense (MTD) app protection policy with Microsoft Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 01/23/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: 
ms.collection:
- tier3
- M365-identity-device-management
- sub-mtd-apps
---

# Create Mobile Threat Defense app protection policy with Intune

Intune with Mobile Threat Defense (MTD) helps you detect threats and assess risk on mobile and Windows devices. You can create an Intune app protection policy that assesses risk to determine if the application is allowed to access corporate data or not.

> [!NOTE]
> This article applies to all Mobile Threat Defense partners that support app protection policies:
>
> - Better Mobile (Android, iOS/iPadOS)
> - BlackBerry Mobile (Android, iOS/iPadOS)
> - Check Point Harmony Mobile (Android, iOS/iPadOS)
> - Jamf (Android, iOS/iPadOS)
> - Microsoft Defender for Endpoint (Android, iOS/iPadOS)
> - Lookout for Work (Android, iOS/iPadOS)
> - Trellix Mobile Security (Android, iOS/iPadOS)
> - SentinelOne (Android, iOS/iPadOS)
> - Symantec Endpoint Security (Android, iOS/iPadOS)
> - Windows Security Center (Windows)
> - Zimperium (Android, iOS/iPadOS)
 
## Before you begin

As part of the MTD setup, in the MTD partner console, you created a policy that classifies various threats as high, medium, and low. You now need to set the Mobile Threat Defense level in the Intune app protection policy.

Prerequisites for app protection policy with MTD:

- Set up MTD integration with Intune. Without this integration, the MTD app protection policy has no effect.

## To create an MTD app protection policy for mobile

Use the procedure to [create an Application protection policy for either iOS/iPadOS or Android](../apps/app-protection-policies.md#app-protection-policies-for-iosipados-and-android-apps), and use the following information on the *Apps*, *Conditional launch*, and *Assignments* pages:

- **Apps**: Select the apps you wish to target with app protection policies. For this feature set, these apps are blocked or selectively wiped based on device risk assessment from your chosen Mobile Threat Defense vendor.
- **Conditional launch**: Below *Device conditions*, use the drop-down box to select **Max allowed device threat level**.

  Options for the threat level **Value**:

  - **Secured**: This level is the most secure. The device can't have any threats present and still access company resources. If any threats are found, the device is evaluated as noncompliant.
  - **Low**: The device is compliant if only low-level threats are present. Anything higher puts the device in a noncompliant status.
  - **Medium**: The device is compliant if the threats found on the device are low or medium level. If high-level threats are detected, the device is determined as noncompliant.
  - **High**: This level is the least secure and allows all threat levels, using Mobile Threat Defense for reporting purposes only. Devices are required to have the MTD app activated with this setting.

  Options for **Action**:

  - **Block access**
  - **Wipe data**

- **Assignments**: Assign the policy to groups of users. The devices used by the group's members are evaluated for access to corporate data on targeted apps via Intune app protection.

## To create an MTD app protection policy for Windows

Use the procedure to [create an Application protection policy for Windows](../apps/app-protection-policy-settings-windows.md), and use the following information on the *Apps*, *Health Checks*, and *Assignments* pages:

- **Apps**: Select the apps you want to target app protection policies. For this feature set, these apps are blocked or selectively wiped based on device risk assessment from your chosen Mobile Threat Defense vendor.
- **Health Checks**: Below *Device conditions*, use the drop-down box to select **Max allowed device threat level**.

  Options for the threat level **Value**:

  - **Secured**: This level is the most secure. The device can't have any threats present and still access company resources. If any threats are found, the device is evaluated as noncompliant.
  - **Low**: The device is compliant if only low-level threats are present. Anything higher puts the device in a noncompliant status.
  - **Medium**: The device is compliant if the threats found on the device are low or medium level. If high-level threats are detected, the device is determined as noncompliant.
  - **High**: This level is the least secure and allows all threat levels, using Mobile Threat Defense for reporting purposes only. Devices are required to have the MTD app activated with this setting.

  Options for **Action**:

  - **Block access**
  - **Wipe data**
    
- **Assignments**: Assign the policy to groups of users. The devices used by the group's members are evaluated for access to corporate data on targeted apps via Intune app protection.

> [!IMPORTANT]
>
> If you create an app protection policy for any protected app, the device's threat level is assessed. Depending on the configuration, devices that don’t meet an acceptable level are either blocked or selectively wiped through conditional launch. If blocked, they are prevented from accessing corporate resources until the threat on the device is resolved and reported to Intune by the chosen MTD vendor.

## Next steps

- Learn more about [Mobile Threat Defense](mobile-threat-defense.md) in Microsoft Intune.
