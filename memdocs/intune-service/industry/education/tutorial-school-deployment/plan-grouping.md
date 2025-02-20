---
title: Plan Education device grouping and targeting
description: Plan how you'll group devices and users and target policies and applications.
ms.date: 5/2/2024
ms.topic: tutorial
ms.author: scbree
author: scottbreenmsft
zone_pivot_groups: platforms-windows-ios
ms.service: microsoft-intune
ms.subservice: education
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
> For more information on grouping and targeting options, see [Performance recommendations for Grouping, Targeting, and Filtering in large Microsoft Intune environments](/mem/intune-service/fundamentals/filters-performance-recommendations).
>
> For tips on avoiding policy conflicts, see [Avoid policy conflicts](manage-avoid-policy-conflicts.md).

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
> For more information on grouping and targeting options, see [Performance recommendations for Grouping, Targeting, and Filtering in large Microsoft Intune environments](/mem/intune-service/fundamentals/filters-performance-recommendations).

## Create groups and filters

✅ Create your organization groups

With your enrollment and grouping plan in place, you can create your groups.

### [Intune](#tab/intune)

- [Create groups in Entra](/entra/fundamentals/how-to-manage-groups)
- [Use filters when assigning your apps, policies, and profiles in Microsoft Intune](/mem/intune-service/fundamentals/filters)
- [Create or update a dynamic group in Microsoft Entra ID](/entra/fundamentals/concept-learn-about-groups)
- [Dynamic membership rules for groups in Microsoft Entra ID](/entra/fundamentals/concept-learn-about-groups)
- [Create simpler, more efficient rules for dynamic groups in Microsoft Entra ID](/entra/fundamentals/concept-learn-about-groups)

### [Intune for Education](#tab/intune-for-education)

- [Create groups in Intune for Education][EDU-1]
- [Manually add or remove users and devices to an existing assigned group][EDU-2]
- [Edit dynamic group rules to accommodate for new devices, locations, or school years][EDU-3]
- [Create Filters](/mem/intune-service/fundamentals/filters)

---

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