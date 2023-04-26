---
title: Admin checklist for software updates on BYOD in Microsoft Intune
description: Guidance and advice for administrators that create and manage software updated for BYOD and personally owned devices using Microsoft Intune. See tasks and settings that can manage updates on personal devices on Android and iOS/iPadOS platforms.
ms.author: mandia
author: MandiOhlinger
manager: dougeby
ms.date: 04/26/2023
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

# Software updates admin checklist for BYOD and personal devices in Microsoft Intune

As organizations embrace a hybrid and remote workforce, admins are challenged with controlling and managing software updates on devices owned by users. These devices are often called BYOD (bring your own device) or personally owned devices. When devices are organization owned, software updates are managed by IT admins. On personal devices, IT admins typically don't have any control of software updates.

When devices aren't enrolled in Intune, they're considered unmanaged.

By default, when a new update is available for unmanaged devices, users receive notifications and/or see the latest updates available on their devices (Settings > Software Updates). The timing of these updates varies depending on the carrier, OEM, and the device itself. At any time, users can check for updates themselves.

To help manage the software updates on unmanaged devices, there are Intune policies and features that can help. This section lists the Microsoft-recommended policies to install software updates on unmanaged devices.

This article applies to:

- Android Enterprise
- iOS/iPadOS

> [!TIP]
> If your devices are organization owned, then go to software updates admin checklist for [managed Android devices](software-updates-guide-android.md) or [supervised iOS/iPadOS devices](software-updates-guide-ios-ipados.md).

## ✔️ **Create enrollment restrictions**

Users can enroll their personal devices in Microsoft Intune.

- When users enroll their personal Android devices, these devices automatically get a work profile. Any policies you create apply to the work profile, not the personal profile. For information on the Android enrollment option for personal devices, go to [Android enrollment guide](../fundamentals/deployment-guide-enrollment-android.md).

- When they enroll iOS/iPadOS devices, the behavior depends on the enrollment option you use. For information on the different iOS/iPadOS enrollment options for personal devices, go to [iOS/iPadOS enrollment guide](../fundamentals/deployment-guide-enrollment-ios-ipados.md).

It's recommended to create an enrollment restrictions policy that requires a minimum and maximum operating system version. This policy helps create a good baseline for new enrollments.

The following example shows an enrollment device platform restrictions policy for Android Enterprise devices:

:::image type="content" source="./media/software-updates-guide-android/android-enrollment-restrictions-policy.png" alt-text="Screenshot that shows enrollment restrictions policy for Android devices in the Microsoft Intune admin center.":::

When users enroll their personal devices, this policy checks the version info. If the devices are outside the versions you enter, then they're prevented from enrolling. ??Is this true? Not sure if CA (?) is built in to enrollment restrictions policies??

For more information on this feature, go to [Device platform restrictions in Intune](../enrollment/create-device-platform-restrictions.md).

## ✔️ **Create compliance policies**

Compliance policies are a great tool to help keep devices up-to-date. If a device isn't using a version you define, then the device is marked as noncompliant. Noncompliant devices are shown in the Microsoft Intune admin center.

It's recommended to create compliance policies, and use the built-in reporting to see noncompliant devices & the individual settings that aren't compliant.

In your compliance policy, you can:

- Notify the user that the OS version doesn't meet your requirements
- Allow a grace period before the device is marked noncompliant, to allow them time to upgrade

:::image type="content" source="./media/software-updates-guide-android/compliance-policy-actions-noncompliance.png" alt-text="Screenshot that shows a compliance policy with actions for noncompliance in the Microsoft Intune admin center.":::

If you combine your compliance policies with Conditional Access (CA), then you can block users from resource access until they meet the OS version requirements.

For more information on compliance policies, go to:

- [Create a compliance policy in Microsoft Intune](create-compliance-policy.md)
- [Configure actions for noncompliant devices in Intune](actions-for-noncompliance.md)
- [Monitor results of your compliance policies](compliance-policy-monitor.md)

## ✔️ **Use app protection policies**

On unmanaged personal devices that access organization resources, it's recommended to use app protection policies.

At the app level, you can use app protection policies to determine the minimum OS and patch versions.

When users open or resume an app that's managed by you, the app protection policy can prompt users to upgrade the OS. In the policy, if the version they're running doesn't meet your requirements, then you can warn users that a new OS version is required, or block access:

:::image type="content" source="./media/software-updates-guide-android/app-protection-policy-device-conditions.png" alt-text="Screenshot that shows device-based conditions in an app protection policy in the Microsoft Intune admin center.":::

## ✔️ **Use custom notifications**

You can create a custom notification to alert users of upcoming OS version requirements. Use this feature to proactively communicate to users to update their devices so they don't lose access:

:::image type="content" source="./media/software-updates-guide-android/custom-notification.png" alt-text="Screenshot that shows a custom notification message in the Microsoft Intune admin center.":::

Remember, if the OS updates can't be forced or controlled, which is common on personal devices, then end users need to update their own devices.

For more information on these features, go to:

- [Conditional launch actions with app protection policies in Intune](../apps/app-protection-policies-access-actions.md)
- [Using custom notifications in Intune](../remote-actions/custom-notifications.md#considerations-for-using-custom-notifications)

## Next steps

- [Software updates admin checklist for managed Android devices](software-updates-guide-android.md)
- [Software updates admin checklist and scenarios for supervised iOS/iPadOS devices](software-updates-guide-ios-ipados.md)
