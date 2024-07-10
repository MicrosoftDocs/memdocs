---
title: Plan Education device grouping and targeting
description: Plan how you'll group devices and users and target policies and applications.
ms.date: 5/2/2024
ms.topic: tutorial
ms.author: scbree
author: scottbreenmsft
zone_pivot_groups: platforms-windows-ios
---

# Plan Education device grouping and targeting

✅ Organize devices and users

By organizing devices, students, classrooms, or learning curricula into groups, you can provide students with the resources and configurations they need.

## Grouping and targeting overview

Intune has four targeting methods:

| Grouping type | Description | Benefits | Disadvantages |
| --- | --- | --- | --- |
| Virtual groups | Created by Intune and allow you to target *All devices* and *All users* | Always up to date automatically | Can only be scoped using filters |
| Assigned groups | Used when you want to manually add users or devices to a group. | Easily manage unique group membership | Membership are manually maintained |
| Dynamic groups | Groups based on rules that you create to assign students or devices to groups. | Automates the membership maintenance of those groups | Can take between several minutes to 24 hours to update |
| Filters | Allows you to further narrow the assignment scope of a policy or app when targeting a group. | Intune quickly evaluates filters on each check-in | Needs to be applied to virtual, assigned, or dynamic groups |

Organizations typically use a combination of these targeting methods.

> [!NOTE]
> Filters aren't accessible in the Intune for Education admin console but are accessible in the Intune admin console.

Two extra groups are precreated if you use **Microsoft School Data Sync (SDS)**: *All teachers* and *All students*. SDS can also be configured to automatically create and maintain groups of students and teachers for each school.

Beyond the defaults, groups can be customized to suit various needs. For example, if you have both *Windows 10* and *Windows 11* devices in your school, you can create groups, such as *Windows 10 devices* and *Windows 11 devices*, to assign different policies and applications to them.

> [!TIP]
> For more information on grouping and targeting options, see [Performance recommendations for Grouping, Targeting, and Filtering in large Microsoft Intune environments](/mem/intune/fundamentals/filters-performance-recommendations).

## Choose grouping methods

✅ Select the best option for grouping

The way you target configuration and apps may depend on many factors and the enrollment type.

::: zone pivot="windows"

The following table provides guidance about which Windows device grouping options to use based on the enrollment method and desired behavior.

| Enrollment type | Behavior | Best grouping options |
| --- | --- | --- |
| Autopilot user driven | Fastest application during enrollment | ✔️ *Device dynamic group* based on [an Autopilot *Group Tag*](/autopilot/enrollment-autopilot), manufacturer or model <br/>✔️ *User dynamic group*✔️ Assigned groups |
| Autopilot self-deploying mode | Fastest application during enrollment | ✔️ *Device dynamic group* based on [an Autopilot *Group Tag*](/autopilot/enrollment-autopilot), manufacturer or model <br/>✔️ Assigned groups |
| All enrollment types | Fastest application during enrollment | ✔️ *All devices* group</br>✔️ *All devices* group with a filter |
| All enrollment types | Applies after enrollment | ✔️ *Device dynamic group* based on other attributes |

::: zone-end

::: zone pivot="ios"

The following table provides guidance about which iOS device grouping options to use based on the enrollment method and desired behavior.

| Enrollment type | Behavior | Best grouping options |
| --- | --- | --- |
| Automated device enrollment | Fastest application during enrollment | ✔️ *All devices* group</br>✔️ *All devices* group with a filter |
| Automated device enrollment with user affinity | Fastest application during enrollment | ✔️ Assigned or dynamic user groups |
| Company portal | Fastest application during enrollment | ✔️ Assigned or dynamic user groups |
| All enrollment types | Applies after enrollment | ✔️ Device dynamic group</br>✔️ Assigned device groups |

::: zone-end

> [!TIP]
> For more information on grouping and targeting options, see [Performance recommendations for Grouping, Targeting, and Filtering in large Microsoft Intune environments](/mem/intune/fundamentals/filters-performance-recommendations).

## Create groups and filters

✅ Create your organization groups

With your enrollment and grouping plan in place, you can create your groups.

### [Intune](#tab/intune)

- [Create groups in Entra](/entra/fundamentals/how-to-manage-groups)
- [Use filters when assigning your apps, policies, and profiles in Microsoft Intune](/mem/intune/fundamentals/filters)
- [Create or update a dynamic group in Microsoft Entra ID](/entra/fundamentals/concept-learn-about-groups)
- [Dynamic membership rules for groups in Microsoft Entra ID](/entra/fundamentals/concept-learn-about-groups)
- [Create simpler, more efficient rules for dynamic groups in Microsoft Entra ID](/entra/fundamentals/concept-learn-about-groups)

### [Intune for Education](#tab/intune-for-education)

- [Create groups in Intune for Education][EDU-1]
- [Manually add or remove users and devices to an existing assigned group][EDU-2]
- [Edit dynamic group rules to accommodate for new devices, locations, or school years][EDU-3]
- [Create Filters](/mem/intune/fundamentals/filters)

---

## Avoiding policy conflicts

✅ Ensure policies apply effectively to devices

> [!NOTE]
> If you only use Intune for Education to manage your devices, you can easily update the settings or apps that you have deployed to existing groups or create new groups to apply new policies or apps. You don't need to do anything extra to prevent conflicts if the members of the new groups are different from the members of the existing groups.

### Considerations when creating new policies in the Microsoft Intune Admin Center

Devices and users targeted with the same setting from different policies cause conflicts. When conflicts occur, Intune generates an error and don't apply eihter setting. As a result, it is important to avoid or resolve conflicts to ensure the correct configuration is applied.

Use these steps to avoid policy conflicts:

1. Determine which users or devices need the new policy.
1. Identify and review potentials sources of conflict.
1. Assign the policy to target group.
1. Monitoring for policy conflicts.

#### Determine which users or devices need the new policy

Review the existing Entra ID groups and determine if they are applicable for the new policy. Otherwise, create a new group and add users or devices.

#### Identify and review potentials sources of conflict

The key to avoiding policy conflicts is to understand if existing policies targeted at the same set of users or devices contain the same settings. If you're creating a new policy that has overlapping settings targeted to the same user or device, exclude those users or devices from existing policies or remove any of the overlapping settings.

You can exclude groups of devices or users using the "exclude group" option or by excluding devices using [filters](/mem/intune/fundamentals/filters).

If you are using an Education tenant, these are the potential policies that may lead to policy conflicts. They should be reviewed for overlapping settings to determine if exclusions are required when targeting the same set of users or devices.

> [!NOTE]
> If you're only using Intune for Education, you can confirm current assignments by navigating to **Groups** and select the group **All Devices** or **All Users** – **Settings** – **Windows device settings** or **iOS device settings**.

##### Default Intune for Education policies

When Intune licenses are added to an Education tenant for the first time, a set of default policies are created and can be viewed in the Configuration policies list in the Intune admin center. These are the policies created:

- **Devices** – **Windows** – **Configuration**
  - Default Policies for EDU
  - Default Admx policy for EDU
  - Edition Upgrade
  - Shared PC Policy
- **Devices** – **Windows** – **Windows 10 and later updates** – **Update rings**
  - Windows Update Policy

##### Policies created on Intune for Education console

When you configure settings in Intune for Education, corresponding policies are created in the Intune service that can be viewed and edited from the Intune admin console. Configuration profiles created by Intune for Education have a recognizable naming template that always starts with the name of the group followed by a suffix based on the template type.

This list provides examples of configuration profiles created by Intune for Education. **GROUP NAME** represents the group that was selected in Intune for Education when the settings were configured.

- **Devices** – **Windows** – **Configuration**
  - **GROUP NAME** Windows10General
  - **GROUP NAME** GroupPolicyConfiguration
  - **GROUP NAME** Windows10EndpointProtection
  - **GROUP NAME** Windows10CustomDenyAdministrativeApps
  - **GROUP NAME** Windows10CustomDenyStore
  - **GROUP NAME** Windows10SharedPC
  - **GROUP NAME** Windows10EnterpriseModernAppManagement
  - **GROUP NAME** ConfigurationPolicy
- **Devices** – **Windows** – **Enrollment** – **Windows Autopilot/Deployment Profiles**
  - **GROUP NAME** Windows10AutopilotProfile
- **Devices** – **Windows** – **Windows 10 and later updates** – **Update rings**
  - **GROUP NAME** Windows10UpdatesForBusiness
- **Devices** – **Windows** – **Windows 10 and later updates** – **Feature Updates**
  - **GROUP NAME** WindowsFeatureUpdates
- **Endpoint security** – **Account protection**
  - **GROUP NAME**_LocalUsersAndGroupsConfig_EDU

#### Add new policy assignment to target group(s)

Once all the potential sources of conflict have been reviewed and required exclusions are configured for any of the existing policies, you can assign the new policy to the user or device group(s). Assign the policy using "Included groups" and optionally use assignment filters for additional targeting options.

#### Monitoring for policy conflicts

##### [Intune](#tab/intune)

 **Devices** – **Monitor** – **Configuration policy assignment failure**. Find the new policy and review any conflicts in the report. The report can also be exported to CSV.

##### [Intune for Education](#tab/intune-for-education)

You can check for potential policy conflicts by going to **Reports** – **Settings error**.

---

If a conflict is found, remove the overlapping settings from the new policy or exclude the targeted users or devices from existing policies.

## Example groups

✅ See examples of common grouping by enrollment type

This section includes targeting methods commonly seen in Education organizations.

::: zone pivot="windows"

### Autopilot

When devices are imported into Autopilot, they include the manufacturer and model of the device. A group tag can also be added to each device imported. The group tag can be used to create groups for targeting. Some customers use group tags to create groups for different autopilot profiles, to target different apps or profiles and also for assigning scope tags for role-based access control.

This table contains common groups used for devices that are enrolled using Autopilot.

| Name | Type | Query |
| --- | --- | --- |
| All Windows devices | Dynamic membership rules | (device.deviceOSType -startsWith \"Windows\") |
| All Autopilot devices | Dynamic membership rules | (device.devicePhysicalIDs -any _ -startsWith \"[ZTDId]\") |
| All non-Autopilot devices | Dynamic membership rules | (device.deviceOSType -startsWith \"Windows\") -and (device.deviceOwnership -eq \"Company\") -and -not(device.devicePhysicalIds -any (_ -startsWith \"[ZTDId]\")) |
| All Autopilot Student devices | Dynamic membership rules | (device.devicePhysicalIds -any (_ -eq \"[OrderID]:*`Student`*\")) |

> [!NOTE]
> The "All Autopilot Student devices" group example is assuming the Autopilot Group Tag is set to "Student". You could use another Group Tag and update the membership rule accordingly.

> [!NOTE]
>
> - If you plan to create groups or filters based on enrollmentProfileName make sure you create the enrollment profile with the name that matches the rules.
> - If you use Autopilot group tags to group devices, make sure the group tags added to device objects match the dynamic group rules.
> - On Windows, apps and policies can also be targeted at user groups. However, the majority of apps and policies on Windows devices are device-based. As a result, each user of a Windows device receives device-based apps and policies assigned to any previous user of the device - unless the new user has different configurations for settings previously applied.

### Provisioning packages

This table contains common groups used for devices that are enrolled using provisioning packages.

| Name | Type | Query |
| --- | --- | --- |
| All Windows devices | Dynamic membership rules | (device.deviceOSType -startsWith \"Windows\") |
| All Student devices | Dynamic membership rules | (device.displayName -startsWith \"*`STU-`*\")|

> [!NOTE]
> The "All Student devices" group example is assuming the device name prefix in the provisioning package is set to "STU-". You could use another prefix and update the membership rule accordingly.

### All enrollment types

Filters can be used to further include or exclude devices from groups. For example:

- Devices running Windows 10 (osVersion *starts with* 10.0.1)
- Devices running Windows 11 (osVersion *starts with* 10.0.2)

::: zone-end

::: zone pivot="ios"

### Automated Device Enrollment

When devices are enrolled with Automated Device Enrollment, the devices are stamped with the enrollment profile name used during enrollment. Devices can be associated with different enrollment profiles in the Automated Device Enrollment token section under enrollment. Some customers use enrollment profile names to create groups or filters for different enrollment settings, to target different apps or profiles and also for assigning scope tags for role-based access control.

Here are examples of queries commonly used for dynamic security groups.

| Name | Type | Query |
| --- | --- | --- |
| All iOS devices | Dynamic membership rules | (device.deviceOSType -startsWith \"iOS\") |
| All *'use case'* devices | Dynamic membership rules | (device.enrollmentProfileName -eq \"'*use case*'\") |

To apply settings as quickly as possible during enrollment without waiting for dynamic group updates, some customers use a filter based on enrollmentProfileName and target configuration at the *All Devices* virtual group.

- Devices with a specific enrollmentProfileName (enrollmentProfileName *equals* *'use case*')

> [!NOTE]
> If you plan to create groups or filters based on enrollmentProfileName make sure you create the enrollment profile with the name that matches the rules.

> [!WARNING]
> Each time an iOS device enrolls it creates a new Entra device object, so *assigned group* memberships aren't maintained afer a device is reset.

::: zone-end

________________________________________________________

> [!div class="nextstepaction"]
> [Next: Set up Microsoft Entra ID >](set-up-microsoft-entra-id.md)

<!-- Reference links in article -->

[EDU-1]: /intune-education/create-groups
[EDU-2]: /intune-education/edit-groups-intune-for-edu
[EDU-3]: /intune-education/edit-groups-intune-for-edu#edit-dynamic-group-rules