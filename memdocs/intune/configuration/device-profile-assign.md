---
# required metadata

title: Assign device profiles in Microsoft Intune
description: Use the Microsoft Intune admin center to assign device configuration profiles and policies to users and devices. Learn how to exclude groups from a profile assignment in Microsoft Intune.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/13/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.assetid: f6f5414d-0e41-42fc-b6cf-e7ad76e1e06d

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: gokarthi
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
- magic-ai-copilot
---

# Assign policies in Microsoft Intune

When you create an Intune policy, it includes all the settings you added and configured within the policy. When the policy is ready to be deployed, the next step is to "assign" the policy to your user or device groups. When you assign the policy, the users and devices receive your policy, and the settings you entered are applied.

In Intune, you can create and assign the following policies:

- App protection policies
- App configuration policies
- Compliance policies
- Conditional Access policies
- Device configuration profiles
- Enrollment policies

This article shows you how to assign a policy, includes some information on using scope tags, describes when to assign policies to user groups or device groups, and more.

This feature applies to:

- Android
- iOS/iPadOS
- macOS
- Linux
- Windows

## Before you begin

- Be sure you have the correct role that can assign policies and profiles. For more information, go to [Role-based access control (RBAC) with Microsoft Intune](../fundamentals/role-based-access-control.md).
- Consider using Microsoft Copilot in Intune. Some benefits include:

  - When you create a policy and configure settings, Copilot provides more information on each setting, can recommend a value, and find potential conflicts.
  - When you assign a policy, Copilot can tell you the groups the policy is assigned to and help you understand the effect of the policy.

  For more information, go to [Microsoft Copilot in Intune](../copilot/copilot-intune-overview.md).

## Assign a policy to users or groups

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Manage devices** > **Configuration**. All the profiles are listed.
3. Select the profile you want to assign > **Properties** > **Assignments** > **Edit**:

    For example, to assign a device configuration profile:

    1. Go to **Devices** > **Manage devices** > **Configuration**. All the profiles are listed.
    2. Select the policy you want to assign > **Properties** > **Assignments** > **Edit**:

       :::image type="content" source="./media/device-profile-assign/properties-select-assignments.png" alt-text="Screenshot that shows how to select assignments to deploy the profile to users and groups in Microsoft Intune.":::

4. Under **Included groups** or **Excluded groups**, choose **Add groups** to select one or more Microsoft Entra groups. If you intend to deploy the policy broadly to all applicable devices, select **Add all users** or **Add all devices**.

    > [!NOTE]
    > If you select "All Devices" and "All Users", the option to add additional Microsoft Entra groups disables. 

5. Select **Review + Save**. This step doesn't assign your policy.
6. Select **Save**. When you save, your policy is assigned. Your groups will receive your policy settings when the devices check in with the Intune service.

## Assignment features you should know and use

- Use **[Filters](../fundamentals/filters.md)** to assign a policy based on rules you create. You can create filters for:

  - App configuration policies
  - App protection policies
  - App assignments
  - Compliance policies
  - Device configuration profiles

  For more information, go to:
  
  - [Use filters when assigning your apps, policies, and profiles in Microsoft Intune](../fundamentals/filters.md)
  - [Platforms, policies, and app types supported by filters in Microsoft Intune](../fundamentals/filters-supported-workloads.md)

- **[Policy sets](../fundamentals/policy-sets.md)** create a group or collection of existing apps and policies. When the policy set is created, you can assign the policy set from a single place in the Microsoft Intune admin center.

  For more information, go to [Use policy sets to group collections of management objects in Microsoft Intune](../fundamentals/policy-sets.md).

- **[Scope tags](../fundamentals/scope-tags.md)** are a great way to filter policies to specific groups, such as `US-NC IT Team` or `JohnGlenn_ITDepartment`. For more information, go to [Use RBAC and scope tags for distributed IT](../fundamentals/scope-tags.md).

- On Windows devices, you can add **[applicability rules](device-profile-create.md#applicability-rules)** so the policy only applies to a specific OS version or a specific Windows edition. For more information, go to [Applicability rules](device-profile-create.md#applicability-rules).

## User groups vs. device groups

Many users ask when to use user groups and when to use device groups. The answer depends on your goal. Here's some guidance to get you started.

### Device groups

If you want to apply settings on a device, regardless of who's signed in, then assign your policies to a devices group. Settings applied to device groups always go with the device, not the user.

For example:

- Device groups are useful for managing devices that don't have a dedicated user. For example, you have devices that print tickets, scan inventory, are shared by shift workers, are assigned to a specific warehouse, and so on. Put these devices in a devices group, and assign your policies to this devices group.

- You create a [Device Firmware Configuration Interface (DFCI) Intune profile](device-firmware-configuration-interface-windows.md) that updates settings in the BIOS. For example, you configure this policy to disable the device camera, or lock down the boot options to prevent users from booting up another OS. This policy is a good scenario to assign to a devices group.

- On some specific Windows devices, you always want to control some Microsoft Edge settings, regardless of who's using the device. For example, you want to block all downloads, limit all cookies to the current browsing session, and delete the browsing history. For this scenario, put these specific Windows devices in a devices group. Then, create an [Administrative Template in Intune](administrative-templates-windows.md), add these device settings, and then assign this policy to the devices group.

To summarize, use device groups when you don't care who's signed in on the device, or if anyone signs in. You want your settings to always be on the device.

### User groups

Policy settings applied to user groups always go with the user, and go with the user when signed in to their many devices. It's normal for users to have many devices, such as a Surface Pro for work, and a personal iOS/iPadOS device. And, it's normal for a person to access email and other organization resources from these devices.

If a user has multiple devices on the same platform, then you can use [filters](../fundamentals/filters.md) on the group assignment. For example, a user has a personal iOS/iPadOS device, and an organization-owned iOS/iPadOS. When you assign a policy for that user, you can use [filters](../fundamentals/filters.md) to target only the organization-owned device.

Follow this general rule: If a feature belongs to a user, such as email or user certificates, then assign to user groups.

For example:

- You want to put a Help Desk icon for all users on all their devices. In this scenario, put these users in a users group, and assign your Help Desk icon policy to this users group.
- A user receives a new organization-owned device. The user signs in to the device with their domain account. The device is automatically registered in Microsoft Entra ID, and automatically managed by Intune. This policy is a good scenario to assign to a users group.
- Whenever a user signs in to a device, you want to control features in apps, such as OneDrive or Office. In this scenario, assign your OneDrive or Office policy settings to a users group.

  For example, you want to block untrusted ActiveX controls in your Office apps. You can create an [Administrative Template in Intune](administrative-templates-windows.md), configure this setting, and then assign this policy to a users group.

To summarize, use user groups when you want your settings and rules to always go with the user, whatever device they use. 

### Azure Virtual Desktop multi-session

You can use Intune to manage Windows multi-session remote desktops created with Azure Virtual Desktop, just like you manage any other shared Windows client device. When you assign policies to user groups or devices, Azure Virtual Desktop multi-session is a special scenario. With virtual machines, device CSPs must target device groups. User CSPs must target user groups.

For more information, go to [Use Azure Virtual Desktop multi-session with Microsoft Intune](../fundamentals/azure-virtual-desktop-multi-session.md).

### Windows CSPs and their behavior

The policy settings for Windows devices are based on the [configuration service providers (CSPs)](/windows/client-management/mdm/configuration-service-provider-reference). These settings map to registry keys or files on the devices.

Here's what you need to know about Windows CSPs:

- Intune exposes these CSPs so you can configure these settings and assign them to your Windows devices. These settings are configurable using the built-in templates and using the [settings catalog](settings-catalog.md). In the settings catalog, you see that some settings apply to the user scope and some settings apply to the device scope.

  For information on how user scoped and device scoped settings are applied to Windows devices, go to [Settings catalog: Device scope vs. user scope settings](settings-catalog.md#device-scope-vs-user-scope-settings).

- When a policy is removed or no longer assigned to a device, different things can happen, depending on the settings in the policy. Each CSP can handle the policy removal differently.

  For example, a setting might keep the existing value, and not revert back to a default value. Each CSP controls the behavior. For a list of Windows CSPs, see [configuration service provider (CSP) reference](/windows/client-management/mdm/configuration-service-provider-reference).

  To change a setting to a different value, create a new policy, configure the setting to **Not configured**, and assign the policy. When the policy applies to the device, users should have control to change the setting to their preferred value.

- When configuring these settings, we suggest deploying to a pilot group. For more Intune rollout advice, see [create a rollout plan](../fundamentals/intune-planning-guide.md).

## Exclude groups from a policy assignment

Intune device configuration policies let you include and exclude groups from policy assignment.

As a best practice:

- Create and assign policies specifically for your user groups. Use [filters](../fundamentals/filters.md) to include or exclude devices of those users.
- Create and assign different policies specifically for your device groups.

For more information on groups, see [Add groups to organize users and devices](../fundamentals/groups-add.md).

### Principles of including and excluding groups

When you assign your policies and policies, apply the following general principles:

- Think of **Included groups** or **Excluded groups** as a starting point for the users and devices that will receive your policies. The Microsoft Entra group is the limiting group, so use the smallest group scope possible. Use [filters](../fundamentals/filters.md) to limit or refine your policy assignment.
- Assigned Microsoft Entra groups, also known as static groups, can be added to Included groups or Excluded groups.

  Typically, you statically assign devices into a Microsoft Entra group if they're pre-registered in Microsoft Entra ID, like with Windows Autopilot. Or, if you want to combine devices for a one-off, ad-hoc deployment. Otherwise, it might not be practical to statically assign devices into a Microsoft Entra group.

- Dynamic Microsoft Entra user groups can be added to Included groups or Excluded groups.

- Excluded groups can be groups with users or groups with devices.

- Dynamic Microsoft Entra device groups can be added to Included groups. But, there can be latency when populating the dynamic group membership. In latency-sensitive scenarios, use [filters](../fundamentals/filters.md) to target specific devices, and assign your policies to user groups.

  For example, you want policies assigned to devices as soon as they enroll. In this latency-sensitive situation, create a [filter](../fundamentals/filters.md) to target the devices you want, and assign the policy with this filter to user groups. Don't assign to device groups.

  In a userless scenario, create a [filter](../fundamentals/filters.md) to target the devices you want, and assign the policy with the filter to the "All devices" group.

- Avoid adding dynamic Microsoft Entra device groups to Excluded groups. Latency in dynamic device group calculation at enrollment can cause undesirable results. For example, unwanted apps and policies might be deployed before the excluded group membership is populated.

### Support matrix

Use the following matrix to understand support for excluding groups:

- ✅: Supported
- ❌: Not supported
- ❕ : Partially supported

:::image type="content" source="./media/device-profile-assign/include-exclude-user-device-groups-matrix.png" alt-text="Screenshot that shows the supported options to include or exclude groups from a policy assignment.":::

| Scenario | Support|
| --- | --- |
| 1 | ❕ Partially supported </br></br> Assigning policies to a dynamic device group while excluding another dynamic device group is supported. But, it's not recommended in scenarios that are sensitive to latency. Any delay in exclude group membership calculation can cause policies to be offered to devices. In this scenario, we recommend using [filters](../fundamentals/filters.md) instead of dynamic device groups for excluding devices. </br></br> For example, you have a device policy that's assigned to **All devices**. Later, you have a requirement that new marketing devices don't receive this policy. So, you create a dynamic device group called **Marketing devices** based on the `enrollmentProfilename` property (`device.enrollmentProfileName -eq "Marketing_devices"`). In the policy, you add the **Marketing devices** dynamic group as an excluded group.  </br></br> A new marketing device enrolls in Intune for the first time, and a new Microsoft Entra device object is created. The dynamic grouping process puts the device into the **Marketing devices** group with a possible delayed calculation. At the same time, the device enrolls into Intune, and starts receiving all applicable policies. The Intune policy can be deployed before the device is put in the exclusion group. This behavior results in an unwanted policy (or app) being deployed to the **Marketing devices** group.  </br></br> As a result, it's not recommended to use dynamic device groups for exclusions in latency sensitive scenarios. Instead, use [filters](../fundamentals/filters.md). |
| 2 | ✅ Supported </br></br> Assigning a policy to a dynamic device group while excluding a static device group is supported. |
| 3 | ❌ Not supported </br></br> Assigning a policy to a dynamic device group while excluding user groups (both dynamic and static) isn't supported. Intune doesn't evaluate user-to-device group relationships, and devices of the included users aren't excluded. |
| 4 | ❌ Not supported </br></br> Assigning a policy to a dynamic device group and excluding user groups (both dynamic and static) isn't supported. Intune doesn't evaluate user-to-device group relationships, and devices of the included users aren't excluded. |
| 5 | ❕ Partially supported </br></br> Assigning a policy to a static device group while excluding a dynamic device group is supported. But, it's not recommended in scenarios that are sensitive to latency. Any delay in exclude group membership calculation can cause policies to be offered to devices. In this scenario, we recommend using [filters](../fundamentals/filters.md) instead of dynamic device groups for excluding devices. |
| 6 | ✅ Supported </br></br> Assigning a policy to a static device group and excluding a different static device group is supported. |
| 7 | ❌ Not supported </br></br> Assigning a policy to a static device group and excluding user groups (both dynamic and static) isn't supported. Intune doesn't evaluate user-to-device group relationships, and devices of the included users aren't excluded. |
| 8 | ❌ Not supported </br></br> Assigning a policy to a static device group and excluding user groups (both dynamic and static) isn't supported. Intune doesn't evaluate user-to-device group relationships, and devices of the included users aren't excluded. |
| 9 | ❌ Not supported </br></br> Assigning a policy to a dynamic user group and excluding device groups (both dynamic and static) isn't supported. |
| 10 | ❌ Not supported </br></br> Assigning a policy to a dynamic user group and excluding device groups (both dynamic and static) isn't supported. |
| 11 | ✅ Supported </br></br> Assigning a policy to a dynamic user group while excluding other user groups (both dynamic and static) is supported. |
| 12 | ✅ Supported </br></br> Assigning a policy to a dynamic user group while excluding other user groups (both dynamic and static) is supported. |
| 13 | ❌ Not supported </br></br> Assigning a policy to a static user group while excluding device groups (both dynamic and static) isn't supported. |
| 14 | ❌ Not supported </br></br> Assigning a policy to a static user group while excluding device groups (both dynamic and static) isn't supported. |
| 15 | ✅ Supported </br></br> Assigning a policy to a static user group while excluding other user groups (both dynamic and static) is supported. |
| 16 | ✅ Supported </br></br> Assigning a policy to a static user group while excluding other user groups (both dynamic and static) is supported. |

## Related articles

See [monitor device profiles](device-profile-monitor.md) for guidance on monitoring your policies, and the devices running your policies.
