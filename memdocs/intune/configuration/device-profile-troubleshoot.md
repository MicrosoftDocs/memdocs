---
# required metadata

title: Troubleshoot device profiles in Microsoft Intune
description: Common questions and answers with device policies and profiles, including profile changes not applied to users or devices, how long it takes for new policies to deploy to devices, which settings apply when there are multiple policies, what happens when a profile is deleted or removed, and more with Microsoft Intune.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/16/2022
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:
ms.assetid: 

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

# Common questions and answers with device policies and profiles in Microsoft Intune

Get answers to common questions when working with device profiles and policies in Intune. This article also lists the check-in time intervals, provides more detains on conflicts, and more.

## How long does it take for devices to get a policy, profile, or app after they are assigned?

Intune notifies the device to check in with the Intune service. The notification times vary, including immediately up to a few hours. These notification times also vary between platforms.

If a device doesn't check in to get the policy or profile after the first notification, Intune makes three more attempts. An offline device, such as turned off, or not connected to a network, may not receive the notifications. In this case, the device gets the policy or profile on its next scheduled check-in with the Intune service. The same applies to checks for non-compliance, including devices that move from a compliant to a non-compliant state.

**Estimated** frequencies:

| Platform | Refresh cycle|
| --- | --- |
| iOS/iPadOS | About every 8 hours |
| macOS | About every 8 hours |
| Android | About every 8 hours |
| Windows 10/11 PCs enrolled as devices | About every 8 hours |
| Windows 8.1 | About every 8 hours |

If devices recently enroll, then the compliance, non-compliance, and configuration check-in runs more frequently. The check-ins are **estimated** at:

| Platform | Frequency |
| --- | --- |
| iOS/iPadOS | Every 15 minutes for 1 hour, and then around every 8 hours |  
| macOS | Every 15 minutes for 1 hour, and then around every 8 hours | 
| Android | Every 3 minutes for 15 minutes, then every 15 minutes for 2 hours, and then around every 8 hours | 
| Windows 10/11 PCs enrolled as devices | Every 3 minutes for 15 minutes, then every 15 minutes for 2 hours, and then around every 8 hours | 
| Windows 8.1 | Every 5 minutes for 15 minutes, then every 15 minutes for 2 hours, and then around every 8 hours | 

At any time, users can open the Company Portal app, **Settings** > **Sync** to immediately check for policy or profile updates. For related information about the Intune Management Extension agent or Win32 apps, see [Win32 app management in Microsoft Intune](../apps/apps-win32-app-management.md).

## What actions cause Intune to immediately send a notification to a device?

There are different actions that trigger a notification. For example, when a policy, profile, or app is assigned (or unassigned), updated, deleted, and so on. These action times vary between platforms.

Devices check in with Intune when they receive a notification to check in, or during the scheduled check-in. When you target a device or user with an action, then Intune immediately notifies the device to check in to receive these updates. For example, when a lock, passcode reset, app, or policy assignment action runs.

Other changes, such as revising the contact information in the Company Portal app, don't cause an immediate notification to devices.

The settings in the policy or profile are applied at every check-in. A [Windows 10 MDM policy refresh customer blog post](https://www.petervanderwoude.nl/post/windows-10-mdm-policy-refresh/) may be a good resource.

## If multiple policies are assigned to the same user or device, how do I know which settings gets applied?

When two or more policies are assigned to the same user or device, then the setting that's applied happens at the individual setting level:

- Compliance policy settings always have precedence over configuration profile settings.

- If a compliance policy evaluates against the same setting in another compliance policy, then the most restrictive compliance policy setting applies.

- If a configuration policy setting conflicts with a setting in another configuration policy, this conflict is shown in Intune. Manually resolve these conflicts.

In the Endpoint Manager admin center, there are few places you can create configuration policies, including Group Policy analytics, Endpoint Security, Security Baselines, and more. If there's a conflict and you have multiple policies, then check all the places you've configured policies. Also, the built-in reporting features can help with conflicts. For more information on the available reports, go to [Intune reports](../fundamentals/reports.md).

## What happens when app protection policies conflict with each other? Which one is applied to the app?

Conflict values are the most restrictive settings available in an app protection policy. The exception is numeric entry fields, such as PIN attempts before reset. Numeric entry fields are set the same as the values, as if you created a MAM policy using the recommended settings option.

Conflicts happen when two profile settings are the same. For example, you configured two MAM policies that are identical except for the copy/paste setting. In this scenario, the copy/paste setting is set to the most restrictive value. The rest of the settings apply as configured.

A policy is deployed to the app and takes effect. A second policy is deployed. In this scenario, the first policy takes precedence, and stays applied. The second policy shows a conflict. If both are applied at the same time, meaning that there isn't preceding policy, then both are in conflict. Any conflicting settings are set to the most restrictive values.

## What happens when iOS/iPadOS or macOS custom policies conflict?

Intune doesn't evaluate the payload of Apple Configuration files or a custom Open Mobile Alliance Uniform Resource Identifier (OMA-URI) policy. It merely serves as the delivery mechanism.

When you assign a custom policy, confirm that the configured settings don't conflict with compliance, configuration, or other custom policies. If a custom policy and its settings conflict, then the settings are applied randomly by Apple.

The built-in reporting features can help with conflicts. For more information on the available reports, go to [Intune reports](../fundamentals/reports.md).

## What happens when a profile is deleted or no longer applicable?

When you delete a profile, or remove a device from a group that's assigned the profile, then the profile and settings are removed from the device. Specifically, they're removed as described in the following list:

- Wi-Fi, VPN, certificate, and email profiles: These profiles are removed from all supported enrolled devices.
- All other profile types:

  - **Android devices**: Settings aren't removed from the device
  - **iOS/iPadOS**: All settings are removed, except:

    - Allow voice roaming
    - Allow data roaming
    - Allow automatic synchronization while roaming

  - **Windows devices**: After you remove or unassign the profile, have the Azure AD user sign in to the device, and [sync with the Intune service](../user-help/sync-your-device-manually-windows.md).

    Intune settings are based on the Windows configuration service provider (CSPs). The behavior depends on the CSP. Some CSPs remove the setting, and some CSPs keep the setting, also called tattooing.

- A profile applies to a user group. Later, a user is removed from the group. For the settings to be removed from that user, it can take up to 7 hours or more for:

  - The profile to be removed from the policy assignment in the Endpoint Manager admin center
  - The device to sync with the Intune object using the [platform-specific policy refresh cycle](#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned) (in this article)

## I changed a device restriction profile, but the changes haven't taken effect

To apply a less restrictive profile, some devices may need to be retired and re-enrolled in to Intune. For example, you may have to retire and re-enroll Android, iOS/iPadOS, and Windows client devices.

## Some settings in a Windows 10/11 profile return "Not Applicable"

Some settings on Windows client devices may show as "Not Applicable". When this situation happens, that specific setting isn't supported on the Windows version or edition running on the device. This message can occur for the following reasons:

- The setting is only available for newer versions of Windows, and not the current operating system (OS) version on the device.
- The setting is only available for specific Windows editions or specific SKUs, such as Home, Professional, Enterprise, and Education.

To learn more about the version and SKU requirements for the different settings, see the [Configuration Service Provider (CSP) reference](/windows/client-management/mdm/configuration-service-provider-reference).

## Next steps

Need extra help? See [How to get support in Microsoft Endpoint Manager](../../get-support.md).
