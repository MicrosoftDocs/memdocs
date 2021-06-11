---
# required metadata

title: Assign device profiles in Microsoft Intune - Azure | Microsoft Docs
description: Use the Microsoft Endpoint Manager admin center to assign device profiles and policies to users and devices. Learn how to exclude groups from a profile assignment in Microsoft Intune.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/19/2021
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:
ms.assetid: f6f5414d-0e41-42fc-b6cf-e7ad76e1e06d

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: scottduf
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

Profile settings applied to user groups always go with the user, and go with the user when signed in to their many devices. It's normal for users to have many devices, such as a Surface Pro for work, and a personal iOS/iPadOS device. And, it's normal for a person to access email and other organization resources from these devices. If a user has more than one device of the same platform, for example if they have a Personal and a Corporate iOS device, you can use [Filters](../fundamentals/) on the group assignment to ensure you are only targeting the Corporate device for that user.

Follow this general rule: If a feature belongs to a user, such as email or user certificates, then assign to user groups.

For example:

- You want to put a Help Desk icon for all users on all their devices. In this scenario, put these users in a users group, and assign your Help Desk icon profile to this users group.
- A user receives a new organization-owned device. The user signs in to the device with their domain account. The device is automatically registered in Azure AD, and automatically managed by Intune. This profile is a good scenario to assign to a users group.
- Whenever a user signs in to a device, you want to control features in apps, such as OneDrive or Office. In this scenario, assign your OneDrive or Office profile settings to a users group.

  For example, you want to block untrusted ActiveX controls in your Office apps. You can create an [Administrative Template in Intune](administrative-templates-windows.md), configure this setting, and then assign this profile to a users group.

To summarize, use user groups when you want your settings and rules to always go with the user, whatever device they use. 

## Exclude groups from a profile assignment

Intune device configuration profiles let you include and exclude groups from profile assignment.

As a best practice, create and assign profiles specifically for your user groups and use Filters to include or exclude devices of those users. Create and assign different profiles specifically for your device groups. For more information on groups, see [Add groups to organize users and devices](../fundamentals/groups-add.md).

When you assign your profiles, apply these general principals:
- Think of Include or Exclude groups as an initial starting point for deploying. The Azure AD group is the limiting group so use the smallest group scope possible. Refine targeting using Filters.
- Assigned (also known as static) Azure AD groups can be used for Included or Excluded groups, however it usually is not practical to statically assign devices into an AAD group unless they are pre-registered in AAD (eg: via autopilot) or if you want to collect them for a one-off, ad-hoc deployment.
- Dynamic Azure AD user groups can be used for Include or Exclude groups.
- Dynamic Azure AD device groups can be used for Include groups but there may be latency in populating group membership. In latency-sensitive scenarios where it is critical for targeting to occur instantly upon enrollment, consider using an assignment to User groups and then combine with filters to target the intended set of devices. If the scenario is userless, consider using the “All devices” group assignment in combination with filters.
- Avoid using Dynamic Azure AD device groups for Excluded groups. Latency in dynamic device group calculation at enrollment time can cause undesirable results such as unwanted apps and policy being delivered before the excluded group membership can be populated.

Use the follow matrix to understand support for and excluding groups. 
- ✔️: Supported
- ❌: Not supported
- ❕ : Partially supported

:::image type="content" source="./media/device-profile-assign/include-exclude-user-device-groups-matrix.png" alt-text="Supported options include or exclude groups from a profile assignment":::

| Scenario | Support| Support note |
| --- | --- |--- |
| 1 | ❕ Partially supported | Assigning policy to a dynamic device group while excluding another dynamic device group is supported but not recommended in scenarios that are sensitive to latency. Any delay in exclude group membership calculation can cause policy to be transiently offered to devices. We recommend using Filters instead of dynamic device groups for excluding devices in this scenario. For example, you have a device policy that's assigned to **All devices**. Later, you have a requirement that new marketing devices don't receive this policy. So, you create a dynamic device group called **Marketing devices** based on the `enrollmentProfilename` property (`device.enrollmentProfileName -eq "Marketing_devices"`). In the policy, you add the **Marketing devices** dynamic group as an excluded group. A new marketing device enrolls in Intune for the first time, and a new Azure AD device object is created. The dynamic grouping process puts the device into the **Marketing device**s group with a possible delayed calculation. In parallel, the device enrolls into Intune, and starts receiving all applicable policies. The Intune policy may be deployed before the device is put in the exclusion group. This behavior results in an unwanted policy (or app) being deployed to the **Marketing devices** group. As a result, it's not recommended to use dynamic device groups for exclusions in latency sensitive scenarios, use filters instead |
| 2 | ✔️ Supported | Assigning a policy to a dynamic device group while excluding a static device group is fully supported. |
| 3 | ❌ Not supported | Assigning a policy to a dynamic device group while excluding user groups (both dynamic and static) is not supported. Intune does not evaluate user-to-device group relationships and devices of the included users will not be excluded. |
| 4 | ❌ Not supported | Assigning a policy to a dynamic device group and excluding user groups (both dynamic and static) is not supported. Intune does not evaluate user-to-device group relationships and devices of the included users will not be excluded. |
| 5 | ❌ Not supported | Assigning policy to a static device group while excluding a dynamic device group is supported but not recommended in scenarios that are sensitive to latency. Any delay in exclude group membership calculation can cause policy to be transiently offered to devices. We recommend using Filters instead of dynamic device groups for excluding devices in this scenario.  |
| 6 | ✔️ Supported | Assigning a policy to a static device group and excluding a different static device group is supported. |
| 7 | ❌ Not supported | Assigning a policy to a static device group and excluding user groups (both dynamic and static) is not supported. Intune does not evaluate user-to-device group relationships and devices of the included users will not be excluded. |
| 8 | ❌ Not supported | Assigning a policy to a static device group and excluding user groups (both dynamic and static) is not supported. Intune does not evaluate user-to-device group relationships and devices of the included users will not be excluded. |
| 9 | ❌ Not supported | Assigning a policy to a dynamic user group and excluding device groups (both dynamic and static) is not supported. |
| 10 | ❌ Not supported | Assigning a policy to a dynamic user group and excluding device groups (both dynamic and static) is not supported. |
| 11 | ✔️ Supported | Assigning a policy to a dynamic user group while excluding other user groups (both dynamic and static) is fully supported. |
| 12 | ✔️ Supported | Assigning a policy to a dynamic user group while excluding other user groups (both dynamic and static) is fully supported. |
| 13 | ❌ Not supported | Assigning a policy to a static user group while excluding device groups (both dynamic and static) is not supported. |
| 14 | ❌ Not supported | Assigning a policy to a static user group while excluding device groups (both dynamic and static) is not supported. |
| 15 | ✔️ Supported | Assigning a policy to a static user group while excluding other user groups (both dynamic and static) is fully supported. |
| 16 | ✔️ Supported | Assigning a policy to a static user group while excluding other user groups (both dynamic and static) is fully supported. |

## Next steps

See [monitor device profiles](device-profile-monitor.md) for guidance on monitoring your profiles, and the devices running your profiles.
