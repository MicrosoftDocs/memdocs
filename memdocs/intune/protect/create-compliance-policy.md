---
# required metadata

title: Create device compliance policies in Microsoft Intune - Azure | Microsoft Docs
description: Create device compliance policies, overview of status and severity levels, using the InGracePeriod status, working with Conditional Access, handling devices without an assigned policy, and the differences in compliance in the Azure portal and classic portal in Microsoft Intune
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/18/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:
ms.reviewer: samyada

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Create a compliance policy in Microsoft Intune

Device compliance policies are a key feature when using Intune to protect your organization's resources. In Intune, you can create rules and settings that devices must meet to be considered compliant, such as a minimum OS version. If the device isn't compliant, you can then block access to data and resources using [Conditional Access](conditional-access.md).

You can also take actions for non-compliance, such as sending a notification email to the user. For an overview of what compliance policies do, and how they're used, see [get started with device compliance](device-compliance-get-started.md).

This article:

- Lists the prerequisites and steps to create a compliancy policy.
- Shows you how to assign the policy to your user and device groups.
- Describes additional features, including scope tags to "filter" your policies, and steps you can take on devices that aren't compliant.
- Lists the check-in refresh cycle times when devices receive policy updates.

## Before you begin

To use device compliance policies, be sure you:

- Use the following subscriptions:

  - Intune
  - If you use Conditional Access, then you need Azure Active Directory (AD) Premium edition. [Azure Active Directory pricing](https://azure.microsoft.com/pricing/details/active-directory/) lists what you get with the different editions. Intune compliance doesn't require Azure AD.

- Use a supported platform:

  - Android device administrator
  - Android Enterprise
  - iOS
  - macOS
  - Windows 10
  - Windows 8.1
  - Windows Phone 8.1

- Enroll devices in Intune (required to see the compliance status)

- Enroll devices to one user, or enroll without a primary user. Devices enrolled to multiple users aren't supported.

## Create the policy

1. Sign in to the [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **Compliance policies** > **Create Policy**.

3. Specify the following properties:

   - **Name**: Enter a descriptive name for the policy. Name your policies so you can easily identify them later. For example, a good policy name is **Mark iOS/iPadOS jailbroken devices as not compliant**.

   - **Description**: Enter a description for the policy. This setting is optional, but recommended.

   - **Platform**: Choose the platform of your devices. Your options:
     - **Android device administrator**
     - **Android Enterprise**
     - **iOS/iPadOS**
     - **macOS**
     - **Windows Phone 8.1**
     - **Windows 8.1 and later**
     - **Windows 10 and later**

     For *Android Enterprise*, you must then select a **Profile type**:
     - **Device owner**
     - **Work Profile**

   - **Settings**: The following articles list and describe the settings for each platform:
     - [Android device administrator](compliance-policy-create-android.md)
     - [Android Enterprise](compliance-policy-create-android-for-work.md)
     - [iOS/iPadOS](compliance-policy-create-ios.md)
     - [macOS](compliance-policy-create-mac-os.md)
     - [Windows Phone 8.1, Windows 8.1 and later](compliance-policy-create-windows-8-1.md)
     - [Windows 10 and later](compliance-policy-create-windows.md)  

   - **Locations** *(Android device administrator)*: In your policy, you can force compliance by the location of the device. Choose from existing locations. Don't have a location yet? [Use Locations (network fence)](use-network-locations.md) in Intune provides some guidance.  

   - **Actions for noncompliance**: For devices that don't meet your compliance policies, you can add a sequence of actions to apply automatically. You can change the schedule when the device is marked non-compliant, such as after one day. You can also configure a second action that sends an email to the user when the device isn't compliant.

     [Add actions for noncompliant devices](actions-for-noncompliance.md) provides more information, including creating a notification email to your users.

     For example, you're using the Locations feature, and add a location in a compliance policy. The default action for noncompliance applies when you select at least one location. If the device isn't connected to the selected locations, it's immediately considered not compliant. You can give your users a grace period, such as one day.

   - **Scope (Tags)**: Scope tags are a great way to filter policies to specific groups, such as `US-NC IT Team` or `JohnGlenn_ITDepartment`. After you add the settings, you can also add a scope tag to your compliance policies. [Use scope tags to filter policies](../fundamentals/scope-tags.md) is a good resource.

4. When finished, select **OK** > **Create** to save your changes. The policy is created, and shown in the list. Next, assign the policy to your groups.

## Assign the policy

Once a policy is created, the next step is to assign the policy to your groups:

1. Choose a policy you created. Existing policies are in **Devices** > **Compliance policies** > **Policies**.

2. Select the *policy* > **Assignments**. You can include or exclude Azure Active Directory (AD) security groups.

3. Choose **Selected groups** to see your Azure AD security groups. Select the groups you want this policy to apply > Choose **Save** to deploy the policy.

The users or devices targeted by your policy are evaluated for compliance when they check-in with Intune.

### Evaluate how many users are targeted

When you assign the policy, you can also **Evaluate** how many users are affected. This feature calculates users; it doesn't calculate devices.

1. In Intune, select **Devices** > **Compliance policies** > **Policies**.

2. Select a *policy* > **Assignments** > **Evaluate**. A message shows you how many users are targeted by this policy.

If the **Evaluate** button is grayed out, make sure the policy is assigned to one or more groups.

<!-- ## Actions for noncompliance

For devices that don't meet your compliance policies, you can add a sequence of actions to apply automatically. You can change the schedule when the device is marked non-compliant, such as after one day. You can also configure a second action that sends an email to the user when the device isn't compliant.

[Add actions for noncompliant devices](actions-for-noncompliance.md) provides more information, including creating a notification email to your users.

For example, you're using the Locations feature, and add a location in a compliance policy. The default action for noncompliance applies when you select at least one location. If the device isn't connected to the selected locations, it's immediately considered not compliant. You can give your users a grace period, such as one day.

## Scope tags

Scope tags are a great way to assign and filter policies to specific groups, such as Sales, HR, All US-NC employees, and so on. After you add the settings, you can also add a scope tag to your compliance policies. [Use scope tags to filter policies](../fundamentals/scope-tags.md) is a good resource.
-->

## Refresh cycle times

Intune uses different refresh cycles to check for updates to compliance policies. If the device recently enrolled, the check-in runs more frequently. [Policy and profile refresh cycles](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned) lists the estimated refresh times.

At any time, users can open the Company Portal app, and sync the device to immediately check for policy updates.

### Assign an InGracePeriod status

The InGracePeriod status for a compliance policy is a value. This value is determined by the combination of a device’s grace period, and a device’s actual status for that compliance policy.

Specifically, if a device has a NonCompliant status for an assigned compliance policy, and:

- The device has no grace period assigned to it, then the assigned value for the compliance policy is NonCompliant
- The device has a grace period that's expired, then the assigned value for the compliance policy is NonCompliant
- The device has a grace period that's in the future, then the assigned value for the compliance policy is InGracePeriod

The following table summarizes these points:

|Actual compliance status|Value of assigned grace period|Effective compliance status|
|---------|---------|---------|
|NonCompliant |No grace period assigned |NonCompliant |
|NonCompliant |Yesterday’s date|NonCompliant|
|NonCompliant |Tomorrow’s date|InGracePeriod|

For more information about monitoring device compliance policies, see [Monitor Intune Device compliance policies](compliance-policy-monitor.md).

### Assign a resulting compliance policy status

If a device has multiple compliance policies, and the device has different compliance statuses for two or more of the assigned compliance policies, then a single resulting compliance status is assigned. This assignment is based on a conceptual severity level assigned to each compliance status. Each compliance status has the following severity level:

|Status  |Severity  |
|---------|---------|
|Unknown     |1|
|NotApplicable     |2|
|Compliant|3|
|InGracePeriod|4|
|NonCompliant|5|
|Error|6|

When a device has multiple compliance policies, then the highest severity level of all the policies is assigned to that device.

For example, a device has three compliance policies assigned to it: one Unknown status (severity = 1), one Compliant status (severity = 3), and one InGracePeriod status (severity = 4). The InGracePeriod status has the highest severity level. So, all three policies have the InGracePeriod compliance status.

## Next steps

[Monitor your policies](compliance-policy-monitor.md).
