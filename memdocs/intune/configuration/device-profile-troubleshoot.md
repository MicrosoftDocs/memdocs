---
# required metadata

title: Questions with policies and profiles in Microsoft Intune
description: Common questions, answers, and scenarios with device policies and profiles in Microsoft Intune. Learn more about profile changes not applying to users or devices, how long it takes for new policies to deploy, which settings apply when there are conflicts, what happens when you delete or remove a profile, and more.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 11/25/2024
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:

ms.reviewer:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
- magic-ai-copilot
---

# Common questions, answers, and scenarios with policies and profiles in Microsoft Intune

[!INCLUDE [windows-phone-81-windows-10-mobile-support](../includes/windows-phone-81-windows-10-mobile-support.md)]

Get answers to common questions when working with policies in Intune. This article also lists the check-in time intervals, provides more detains on conflicts, and more.

This article applies to the following policies:

- App protection policies
- App configuration policies
- Compliance policies
- Conditional Access policies
- Device configuration profiles
- Enrollment policies

## Policy refresh intervals

When a device checks-in, it immediately checks for compliance, non-compliance and configuration for the current user/device context, receiving any pending actions, policies and apps assigned to it.

There are 4 main types of check-ins:

**Scheduled check-ins** - These check-ins happen at predetermined intervals and can be initiated by the client or service depending on the platform. The check-ins are estimated as follows:

| Platform | Estimated refresh cycle|
| --- | --- |
| Android, AOSP | About every 8 hours |
| iOS/iPadOS | About every 8 hours |
| macOS | About every 8 hours |
| Windows 10/11 PCs enrolled as devices | About every 8 hours |

**End user driven check-ins** – These check-ins are driven by end users when they perform certain actions in the Company Portal app like going into  **Devices** > **Check Status** or **Settings** > **Sync** to check for policy or profile updates or selecting an app for download.

**Admin check-ins** - These check-ins are driven by admins when they perform certain actions on a single device from the Intune portal, like [device sync](../remote-actions/device-sync.md), [remote lock](../remote-actions/device-remote-lock.md) or [reset passcode](../remote-actions/device-passcode-reset.md). Other actions like [remotely assist users](../fundamentals/remote-help.md) do not cause a device check-in.

**Notification-based check-ins** - These check-ins happen through different actions that trigger a notification. For example, when a policy, profile, or app is assigned (or unassigned), updated, deleted, or when certain behind the scenes changes like Microsoft Entra group membership updates are made. Other changes don't cause an immediate notification to devices, like adding an app as available to your users.

Intune notifies online devices to check-in with the Intune service. The notification times vary from immediately up to a few hours.
These notification times also vary between platforms.

- On Android devices, [Google Mobile Services (GMS) can affect policy refresh intervals](../apps/manage-without-gms.md#some-tasks-can-be-delayed).

- On iOS devices, [Specific conditions can affect policy refresh intervals](/troubleshoot/mem/intune/device-configuration/2016341112-ios-device-is-currently-busy).

An offline device, such as a powered off, or a disconnected device, might not receive the notifications. In this case, the device gets the policy or profile on its next scheduled check-in with Intune.

> [!NOTE]
> It might take additional time for Intune reports to reflect the latest status of the policy on the device in the Intune portal.  

Additionally, when devices first enroll, configuration check-ins run more frequently to perform configuration, compliance and non-compliance checks. The check-ins are estimated as follows:

| Platform | Estimated refresh cycle|
| --- | --- |
| Android, AOSP | Every 3 minutes for 15 minutes, then every 15 minutes for 2 hours, and then around every 8 hours |
| iOS/iPadOS | Every 15 minutes for 1 hour, and then around every 8 hours |
| macOS | Every 15 minutes for 1 hour, and then around every 8 hours |
| Windows 10/11 PCs enrolled as devices | Every 3 minutes for 15 minutes, then every 15 minutes for 2 hours, and then around every 8 hours |

For app protection policy refresh intervals, go to [App Protection Policy delivery timing](../apps/app-protection-policy-delivery.md).

## Company portal

At any time, users can open the Company Portal app and navigate to **Devices** > **Check Status** to evaluate your device's settings and verify access to work or school resources or navigate to **Settings** > **Sync** to get the latest updates, requirements, and communications from your organization.

For related information about the Intune Management Extension agent or Win32 apps, see [Win32 app management in Microsoft Intune](../apps/apps-win32-app-management.md).

For related information, see  [Sync enrolled device for Windows](../user-help/sync-your-device-manually-windows.md) and [Check device access in Company Portal for Windows](../user-help/check-device-access-windows-cpapp.md).

## Conflicts

Conflicts can happen when different policies update the same setting to different values. For example, you have two policies that update the copy/paste setting to different values. The conflict is handled differently depending on the type of policy.

If you use Microsoft Copilot in Intune, then Copilot can help you resolve conflicts. For more information, go to [Policy and setting management in Copilot in Intune](../copilot/copilot-intune-overview.md#policy-and-setting-management).

You can also use Microsoft Copilot in Intune to get more information about your policies and the settings configured in your policies.

### App protection policies that conflict

Conflict values are the most restrictive settings available in an app protection policy. The exception is numeric entry fields, such as PIN attempts before reset. Numeric entry fields are set the same as the values, as if you created a MAM policy using the recommended settings option.

Conflicts happen when two profile settings are the same. For example, you configured two MAM policies that are identical except for the copy/paste setting. In this scenario, the copy/paste setting is set to the most restrictive value. The rest of the settings apply as configured.

A policy is deployed to the app and takes effect. A second policy is deployed. In this scenario, the first policy takes precedence, and stays applied. The second policy shows a conflict. If both are applied at the same time, meaning that there isn't preceding policy, then both are in conflict. Any conflicting settings are set to the most restrictive values.

### Compliance and device configuration policies that conflict

When two or more policies are assigned to the same user or device, then the setting that applies happens at the individual setting level:

- If you use compliance policies to evaluate device settings, then the settings within the compliance policy take precedence over the same setting within device configuration policies. Compliance policy settings always have precedence over configuration profile settings.

- If a compliance policy evaluates against the same setting in another compliance policy, then the most restrictive compliance policy setting applies.

- If a configuration policy setting conflicts with a setting in another configuration policy, this conflict is shown in Intune. Manually resolve these conflicts.

In the Intune admin center, there are a few places you can create configuration policies, including Group Policy analytics, endpoint security, security baselines, and more. If there's a conflict and you have multiple policies, then check all the places you configured policies. Also, the built-in reporting features can help with conflicts. For more information on the available reports, go to [Intune reports](../fundamentals/reports.md).

### Custom iOS/iPadOS or macOS policies that conflict

Intune doesn't evaluate the payload of Apple Configuration files or a custom Open Mobile Alliance Uniform Resource Identifier (OMA-URI) policy. It merely serves as the delivery mechanism.

When you assign a custom policy, confirm that the configured settings don't conflict with compliance, configuration, or other custom policies. If a custom policy and its settings conflict, then Apple randomly applies the settings.

The built-in reporting features can help with conflicts. For more information on the available reports, go to [Intune reports](../fundamentals/reports.md).

## A profile is deleted or no longer applicable

When you delete a profile, or remove a device from a group that's assigned the profile, then the profile and settings are removed from the device. Specifically, they're removed as described in the following list:

- Wi-Fi, VPN, certificate, and email profiles: These profiles are removed from all supported enrolled devices.
- All other profile types:

  - **Android devices**: Settings aren't removed from the device.
  - **iOS/iPadOS**: All settings are removed, except:

    - Allow voice roaming
    - Allow data roaming
    - Allow automatic synchronization while roaming

  - **Windows devices**: After you remove or unassign the profile, have the Microsoft Entra user sign in to the device, and [sync with the Intune service](../user-help/sync-your-device-manually-windows.md).

    Intune settings are based on the Windows configuration service provider (CSPs). The behavior depends on the CSP. Some CSPs remove the setting, and some CSPs keep the setting, also called tattooing.

- A profile applies to a user group. Later, a user is removed from the group. For the settings to be removed from that user, it can take up to 7 hours or more for:

  - The profile to be removed from the policy assignment in the Intune admin center
  - The device to sync with the Intune object using the [platform-specific policy refresh cycle](#policy-refresh-intervals) (in this article)

## I changed a device restriction profile, but the changes haven't taken effect

To apply a less restrictive profile, some devices might need to be retired and re-enrolled in to Intune. For example, you might have to retire and re-enroll Android, iOS/iPadOS, and Windows client devices.

## Some settings in a Windows 10/11 profile return "Not Applicable"

Some settings on Windows client devices can show as **Not Applicable**. When this situation happens, that specific setting isn't supported on the Windows version or edition running on the device. This message can occur for the following reasons:

- The setting is only available for newer versions of Windows, and not the current operating system (OS) version on the device.
- The setting is only available for specific Windows editions or specific SKUs, such as Home, Professional, Enterprise, and Education.

To learn more about the version and edition requirements for the different settings, see the [Configuration Service Provider (CSP) reference](/windows/client-management/mdm/configuration-service-provider-reference).

## When devices enroll, there's a delay in applying apps and policies assigned to dynamic device groups

During enrollment, you can use Microsoft Entra dynamic device groups. For example, you can create a dynamic device group based on a device's name or enrollment profile.

The enrollment profile is applied to the device record during initial device setup. Microsoft Entra dynamic grouping isn't instant. The device might not be in the dynamic group for some time, possibly minutes to hours depending on other changes being made in your tenant.

If the device isn't added to the group, then your apps and policies aren't assigned to the device during the initial Intune check-in. The policies might not apply until the next scheduled check-in.

If fast delivery of apps and policies is important to your setup/enrollment scenario, then assign your apps and policies to user groups, not dynamic device groups. User groups are pre-populated with members before device setup and don't have this delay.

For more information on dynamic groups, go to:

- [Add groups to organize users and devices in Intune](../fundamentals/groups-add.md)
- [Performance recommendations when using Intune to group, target, and filter](../fundamentals/filters-performance-recommendations.md)
- [Dynamic membership rules for groups in Microsoft Entra ID](/azure/active-directory/enterprise-users/groups-dynamic-membership)

## "The sync could not be initiated (0x80072f9a)" error

On Windows devices, when trying to sync in the **Settings** app > **Accounts** > **Access work or school**, you might see a `The sync could not be initiated (0x80072f9a)` error.

If the Trusted Platform Module (TPM) was reset to factory settings, then the device must reenrolled to resume syncing. The device's Microsoft Entra identity is stored in the TPM. So, if the ID is removed, then reenrollment is the only way to reestablish the Microsoft Entra identity. 

## Related articles

- [Troubleshoot policies and profiles](/troubleshoot/mem/intune/troubleshoot-policies-in-microsoft-intune).
- Need extra help? See [How to get support in Microsoft Intune](../../get-support.md).
