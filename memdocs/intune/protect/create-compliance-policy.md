---
# required metadata

title: Create device compliance policies in Microsoft Intune
description: Create device compliance policies for Microsoft Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/20/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.reviewer: samyada

# optional metadata

#ROBOTS:
#audience:

ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: 
  - M365-identity-device-management
  - highpri
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
  - Android AOSP
  - Android Enterprise
  - iOS
  - macOS
  - Windows 10/11
  - Windows 8.1

- Enroll devices in Intune (required to see the compliance status)

- Enroll devices to one user, or enroll without a primary user. Single devices cannot be enrolled to multiple users.

If you plan to use custom settings for device compliance, you'll need prepare a custom JSON file and PowerShell script before you create a policy. For more information about custom compliance settings, including supported platforms, prerequisites, and how to configure the *Custom Compliance* category while creating a policy, see [Use custom compliance settings](../protect/compliance-use-custom-settings.md).
## Create the policy

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **Compliance policies** > **Policies** > **Create Policy**.

3. Select a **Platform** for this policy from the following options:
   - *Android device administrator*
   - *Android (AOSP)*
   - *Android Enterprise*
   - *iOS/iPadOS*
   - *macOS*
   - *Windows 8.1 and later*
   - *Windows 10 and later*

    For *Android Enterprise*, you also select a **Policy type**:
     - *Fully Managed*
     - *Dedicated*
     - *Corporate-Owned Work Profile*
     - *Personally-Owned Work Profile*

    Then, select **Create** to open the **Create policy** configuration window.

4. On the **Basics** tab, specify a **Name** that helps you identify them later. For example, a good policy name is **Mark iOS/iPadOS jailbroken devices as not compliant**.

   You can also choose to specify a **Description**.
  
5. On the **Compliance settings** tab, expand the available categories, and configure settings for your policy. The following articles describe the settings for each platform:
   - [Android device administrator](compliance-policy-create-android.md)
   - [Android (AOSP)](compliance-policy-create-android-aosp.md)
   - [Android Enterprise](compliance-policy-create-android-for-work.md)
   - [iOS/iPadOS](compliance-policy-create-ios.md)
   - [macOS](compliance-policy-create-mac-os.md)
   - [Windows 8.1 and later](compliance-policy-create-windows-8-1.md)
   - [Windows 10/11](compliance-policy-create-windows.md)  

   Before you use the category *Custom Compliance* to add custom compliance settings, you must preconfigure a JSON to define the custom settings you want to use, and upload a PowerShell script that runs discovery of those settings on supported devices.

   For more information about custom settings for device compliance, including supported platforms, prerequisites, and how to configure the *Custom Compliance* category while creating a policy, see [Use custom compliance settings](../protect/compliance-use-custom-settings.md).

6. On the **Actions for noncompliance** tab, specify a sequence of actions to apply automatically to devices that don't meet this compliance policy.

   You can add multiple actions and configure schedules and additional details for some actions. For example, you might change the schedule of the default action *Mark device noncompliant* to occur after one day. You can then add an action to send an email to the user when the device isn't compliant to warn them of that status. You can also add  actions that lock or retire devices that remain noncompliant.

   For information about the actions you can configure, see [Add actions for noncompliant devices](actions-for-noncompliance.md), including how to create notification emails to send to your users.

   Another example includes the use of Locations where you add at least one location to a compliance policy. In this case, the default action for noncompliance applies when you select at least one location. If the device isn't connected to any of the selected locations, it's considered not compliant. You can configure the schedule to give your users a grace period, such as one day.

7. On the **Scope tags** tab, select tags to help filter policies to specific groups, such as `US-NC IT Team` or `JohnGlenn_ITDepartment`. After you add the settings, you can also add a scope tag to your compliance policies. 

   For information on using scope tags, see [Use scope tags to filter policies](../fundamentals/scope-tags.md).

8. On the **Assignments** tab, assign the policy to your groups.  

   Select **+ Select groups to include** and then assign the policy to one or more groups. The policy will apply to these groups when you save the policy after the next step. 

9. On the **Review + create** tab, review the settings and select **Create** when ready to save the compliance policy.  

   The users or devices targeted by your policy are evaluated for compliance when they check in with Intune.

## Refresh cycle times

Intune uses different refresh cycles to check for updates to compliance policies. If the device recently enrolled, the check-in runs more frequently. [Policy and profile refresh cycles](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned) lists the estimated refresh times.

At any time, users can open the Company Portal app, and sync the device to immediately check for policy updates.

### Assign an InGracePeriod status

The InGracePeriod status for a compliance policy is a value. This value is determined by the combination of a device's grace period, and a device's actual status for that compliance policy.

Specifically, if a device has a NonCompliant status for an assigned compliance policy, and:

- The device has no grace period assigned to it, then the assigned value for the compliance policy is NonCompliant
- The device has a grace period that's expired, then the assigned value for the compliance policy is NonCompliant
- The device has a grace period that's in the future, then the assigned value for the compliance policy is InGracePeriod

The following table summarizes these points:

|Actual compliance status|Value of assigned grace period|Effective compliance status|
|---------|---------|---------|
|NonCompliant |No grace period assigned |NonCompliant |
|NonCompliant |Yesterday's date|NonCompliant|
|NonCompliant |Tomorrow's date|InGracePeriod|

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
