---
# required metadata

title: Assign device profiles in Microsoft Intune - Azure | Microsoft Docs
description: Use the Microsoft Endpoint Manager admin center to assign device profiles and policies to users and devices. Learn how to exclude groups from a profile assignment in Microsoft Intune.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/01/2021
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:
ms.assetid: f6f5414d-0e41-42fc-b6cf-e7ad76e1e06d

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: altsou
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure, contperf-fy21q1
ms.collection: M365-identity-device-management
---

# Assign user and device profiles in Microsoft Intune

You create a profile, and it includes all the settings you entered. The next step is to deploy or "assign" the profile to your user or device groups. When it's assigned, the users and devices receive your profile, and the settings you entered are applied.

This article shows you how to assign a profile, and includes some information on using scope tags on your profiles.

> [!NOTE]  
> When a profile is removed or no longer assigned to a device, different things can happen, depending on the settings in the profile. The settings are based on CSPs, and each CSP can handle the profile removal differently. For example, a setting might keep the existing value, and not revert back to a default value. The behavior is controlled by each CSP in the operating system. For a list of Windows CSPs, see [configuration service provider (CSP) reference](/windows/client-management/mdm/configuration-service-provider-reference).
>
> To change a setting to a different value, create a new profile, configure the setting to **Not configured**, and assign the profile. Once applied to the device, users should have control to change the setting to their preferred value.
>
> When configuring these settings, we suggest deploying to a pilot group. For more Intune rollout advice, see [create a rollout plan](../fundamentals/intune-planning-guide.md).

## Before you begin

Be sure you have the correct role to assign profiles. For more information, see [Role-based access control (RBAC) with Microsoft Intune](../fundamentals/role-based-access-control.md).

## Assign a device profile

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration profiles**. All the profiles are listed.
3. Select the profile you want to assign > **Properties** > **Assignments** > **Edit**:

    :::image type="content" source="./media/device-profile-assign/properties-select-assignments.png" alt-text="Select assignments to deploy the profile to users and groups in Microsoft Intune and Endpoint Manager":::

4. Select **Included groups** or **Excluded groups**, and then choose **Select groups to include**. When you select your groups, you're choosing an Azure AD group. To select multiple groups, hold down the **Ctrl** key, and select your groups.

    :::image type="content" source="./media/device-profile-assign/select-included-excluded-groups-profile-assignment.png" alt-text="Include or exclude users and groups when assigning or deploying a profile in Microsoft Intune and Endpoint Manager.":::

5. Select **Review + Save**. This step doesn't assign your profile.
6. Select **Save**. When you save, your profile is assigned. Your groups will receive your profile settings when the devices check in with the Intune service.

## Use scope tags or applicability rules

When you create or update a profile, you can also add scope tags and applicability rules to the profile.

**Scope tags** are a great way to filter profiles to specific groups, such as `US-NC IT Team` or `JohnGlenn_ITDepartment`. [Use RBAC and scope tags for distributed IT](../fundamentals/scope-tags.md) has more information.

On Windows 10 devices, you can add **applicability rules** so the profile only applies to a specific OS version or a specific Windows edition. [Applicability rules](device-profile-create.md#applicability-rules) has more information.

## User groups vs. device groups

Many users ask when to use user groups and when to use device groups. The answer depends on your goal. Here's some guidance to get you started.

### Device groups

If you want to apply settings on a device, regardless of who's signed in, then assign your profiles to a devices group. Settings applied to device groups always go with the device, not the user.

For example:

- Device groups are useful for managing devices that don't have a dedicated user. For example, you have devices that print tickets, scan inventory, are shared by shift workers, are assigned to a specific warehouse, and so on. Put these devices in a devices group, and assign your profiles to this devices group.

- You create a [Device Firmware Configuration Interface (DFCI) Intune profile](device-firmware-configuration-interface-windows.md) that updates settings in the BIOS. For example, you configure this profile to disable the device camera, or lock down the boot options to prevent users from booting up another OS. This profile is a good scenario to assign to a devices group.

- On some specific Windows devices, you always want to control some Microsoft Edge settings, regardless of who's using the device. For example, you want to block all downloads, limit all cookies to the current browsing session, and delete the browsing history. For this scenario, put these specific Windows devices in a devices group. Then, create an [Administrative Template in Intune](administrative-templates-windows.md), add these device settings, and then assign this profile to the devices group.

To summarize, use device groups when you don't care who's signed in on the device, or if anyone signs in. You want your settings to always be on the device.

### User groups

Profile settings applied to user groups always go with the user, and go with the user when signed in to their many devices. It's normal for users to have many devices, such as a Surface Pro for work, and a personal iOS/iPadOS device. And, it's normal for a person to access email and other organization resources from these devices.

Follow this general rule: If a feature belongs to a user, such as email or user certificates, then assign to user groups.

For example:

- You want to put a Help Desk icon for all users on all their devices. In this scenario, put these users in a users group, and assign your Help Desk icon profile to this users group.
- A user receives a new organization-owned device. The user signs in to the device with their domain account. The device is automatically registered in Azure AD, and automatically managed by Intune. This profile is a good scenario to assign to a users group.
- Whenever a user signs in to a device, you want to control features in apps, such as OneDrive or Office. In this scenario, assign your OneDrive or Office profile settings to a users group.

  For example, you want to block untrusted ActiveX controls in your Office apps. You can create an [Administrative Template in Intune](administrative-templates-windows.md), configure this setting, and then assign this profile to a users group.

To summarize, use user groups when you want your settings and rules to always go with the user, whatever device they use.

## Exclude groups from a profile assignment

Intune device configuration profiles let you include and exclude groups from profile assignment.

As a best practice, create and assign profiles specifically for your user groups. And, create and assign different profiles specifically for your device groups. For more information on groups, see [Add groups to organize users and devices](../fundamentals/groups-add.md).

When you assign your profiles, use the following table when including and excluding groups. A checkmark means that assignment is supported:

:::image type="content" source="./media/device-profile-assign/include-exclude-user-device-groups.png" alt-text="Supported options include or exclude groups from a profile assignment":::

### What you should know

- Exclusion takes precedence over inclusion in the following same group type scenarios:

  - Including user groups and excluding user groups
  - Including device groups and excluding device group

  For example, you assign a device profile to the **All corporate users** user group, but exclude members in the **Senior Management Staff** user group. Since both groups are user groups, **All corporate users** except the **Senior Management staff** get the profile.

- Intune doesn't evaluate user-to-device group relationships. If you assign profiles to mixed groups, the results may not be what you want or expect.

  For example, you assign a device profile to the **All Users** user group, but exclude an **All personal devices** device group. In this mixed group profile assignment, **All users** get the profile. The exclusion does not apply.

  As a result, it's not recommended to assign profiles to mixed groups.

> [!NOTE]
> Use caution when excluding dynamic device groups from any policy assignment. Consider the latency associated with an Azure AD dynamic device group calculation.  
> 
> For example, you have a device policy that's assigned to **All devices**. Later, you have a requirement that new marketing devices don't receive this policy. So, you create a dynamic device group called **Marketing devices** based on the `enrollmentProfilename` property (`device.enrollmentProfileName -eq "Marketing_devices"`). In the policy, you add the **Marketing devices** dynamic group as an excluded group.
> 
> A new marketing device enrolls in Intune for the first time, and a new Azure AD device object is created. The dynamic grouping process puts the device into the **Marketing device**s group with a possible delayed calculation. In parallel, the device enrolls into Intune, and starts receiving all applicable policies. The Intune policy may be deployed before the device is put in the exclusion group. This behavior results in an unwanted policy (or app) being deployed to the **Marketing devices** group.
> 
> As a result, it's not recommended to use dynamic device groups for exclusions in latency sensitive scenarios.

## Next steps

See [monitor device profiles](device-profile-monitor.md) for guidance on monitoring your profiles, and the devices running your profiles.
