---
title: Plan Education device grouping and targeting
description: Plan how you will group devices and users and target policies and applications.
ms.date: 01/16/2024
ms.topic: tutorial
appliesto:
ms.author: scbree
author: scottbreenmsft
zone_pivot_groups: platforms-windows-ios
---

# Plan Education device grouping and targeting

✅ Organize devices and users

By organizing devices, students, classrooms, or learning curricula into groups, you can provide students with the resources and configurations they need.

## Grouping and targeting overview

Intune has three main targeting methods:

- **Virtual groups** are created by Intune and allow you to target *All devices* and *All users*.

- **Groups** are created and managed in Entra and can contain users or devices.
  - **Assigned groups** are used when you want to manually add users or devices to a group.

  - **Dynamic groups** reference rules that you create to assign students or devices to groups, which automate the membership's maintenance of those groups.

- [**Filters**](/mem/intune/fundamentals/filters) allows you to narrow the assignment scope of a policy. <br><br>For example, use filters to target devices with a specific OS version or a specific manufacturer, target only personal devices or only organization-owned devices, and more. Filters are evaluated dynamically during a device check-in and can therefore sometimes offer a faster dynamic grouping option than an Entra dynamic group.

 > **alternative display option below**

Intune has four main targeting methods:

| Grouping type | Description | Benefits | Disadvantages |
| --- | --- | --- | --- |
| Virtual groups | Created by Intune and allow you to target *All devices* and *All users* | Always up to date automatically | Can only be scoped using filters |
| Assigned groups | Used when you want to manually add users or devices to a group. | Easily manage unique group memeberships | Membership are manually maintained |
| Dynamic groups | Groups based on rules that you create to assign students or devices to groups. | Automates the membership maintenance of those groups | Can take between several minutes to 24 hours to update |
| Filters | Allows you to further narrow the assignment scope of a policy or app when targeting a group. | Intune quickly evaluates filters on each check-in | Needs to be applied to virtual, assigned or dynamic groups |

Organizations typically use a combination of these grouping types in their envrironments.

> [!NOTE]
> Filters aren't accessible in the Intune for Education admin console but are accessible in the Intune admin console.

Two extra groups are precreated if you use **Microsoft School Data Sync (SDS)**: *All teachers* and *All students*. SDS can also be configured to automatically create and maintain groups of students and teachers for each school.

Beyond the defaults, groups can be customized to suit various needs. For example, if you have both *Windows 10* and *Windows 11* devices in your school, you can create groups, such as *Windows 10 devices* and *Windows 11 devices*, to assign different policies and applications to.

> [!TIP]
> For more information on grouping and targeting options, see [Performance recommendations for Grouping, Targeting, and Filtering in large Microsoft Intune environments](/mem/intune/fundamentals/filters-performance-recommendations).

## Choose grouping methods

✅ Check out tips and tricks for grouping

::: zone pivot="windows"

For Windows devices:
- Applications and policies targeted to a *device dynamic group* based on [an Autopilot *Group Tag*](/autopilot/enrollment-autopilot) will be applied to the devices as soon as they are enrolled in Intune, before users signs in.
  This can be useful in bulk enrollment scenarios, where devices are enrolled without requiring users to sign in. Devices can be configured and prepared in advance, before distribution.

- Applications and policies targeted to a *device dynamic group* based on other attributes will be applied to the devices after they are enrolled in Intune, after users gain access to the device.

 > **alternative display option below**

The following table provides guidance about which Windows device grouping options to use based on the enrollment method and desired behavior.

| Enrollment type | Behavior | Best grouping options |
| --- | --- | --- |
| Autopilot | Fastest application during enrollment | ✔️ *Device dynamic group* based on [an Autopilot *Group Tag*](/autopilot/enrollment-autopilot), manufacturer or model <br/>✔️ Assigned groups |
| Autopilot userdriven | Fastest application during enrollment | ✔️ Assigned or dynamic user groups |
| All enrollment types | Fastest application during enrollment | ✔️ All devices group</br>✔️ All devices group with a filter |
| All enrollment types | Applies after enrollment | ✔️ *Device dynamic group* based on other attributes |

::: zone-end

::: zone pivot="ios"

For iOS devices:
- If you target applications and policies to a *device dynamic group*, they will be applied to the devices after they are enrolled in Intune, after users gain access to the device.

 > **alternative display option below**

The following table provides guidance about which iOS device grouping options to use based on the enrollment method and desired behavior.

| Enrollment type | Behavior | Best grouping options |
| --- | --- | --- |
| Automated device enrollment | Fastest application during enrollment | ✔️ All devices group</br>✔️ All devices group with a filter |
| Automated device enrollment with user affinity | Fastest application during enrollment | ✔️ Assigned or dynamic user groups |
| All enrollment types | Applies after enrollment | ✔️ *Device dynamic group* based on other attributes</br>✔️ Assigned device groups |

::: zone-end

> [!TIP]
> For more information on grouping and targeting options, see [Performance recommendations for Grouping, Targeting, and Filtering in large Microsoft Intune environments](/mem/intune/fundamentals/filters-performance-recommendations).


## Create groups and filters

✅ Create your organization groups

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

## Example groups

✅ See examples of common grouping by enrollment type

The way you target configuration and apps may depend on many factors and the enrollment type. This section includes targeting methods commonly seen amongst Education organizations.

::: zone pivot="windows"

### Autopilot
When devices are imported into Autopilot they include the manufacturer and model of the device. A group tag can also be added to each device imported. The group tag can be used to create groups for targeting. Some customers use this to create groups for different autopilot profiles, to target different apps or profiles and also for assigning scope tags for role-based access control.
These are the common groups used for devices that are enrolled using Autopilot.

| Name | Type | Query |
| --- | --- | --- |
| All Windows devices | Dynamic membership rules | (device.deviceOSType -startsWith \"Windows\") |
| All Autopilot devices | Dynamic membership rules | (device.devicePhysicalIDs -any _ -startsWith \"[ZTDId]\") |
| All non-Autopilot devices | Dynamic membership rules | (device.deviceOSType -startsWith \"Windows\") -and (device.deviceOwnership -eq \"Company\") -and -not(device.devicePhysicalIds -any (_ -startsWith \"[ZTDId]\")) |
| All *use case* devices | Dynamic membership rules | (device.devicePhysicalIds -any (_ -eq \"[OrderID]:*use case*\")) |

### Provisioning packages
These are the common groups used for devices that are enrolled using provisioning packages.

| Name | Type | Query |
| --- | --- | --- |
| All Windows devices | Dynamic membership rules | (device.deviceOSType -startsWith \"Windows\") |
| All *use case* devices | Dynamic membership rules | (device.displayName -startsWith \"*use case*\") |

### All enrollment types
Filters can be used to further include or exclude devices from groups. For example:

- Devices running Windows 10 (osVersion *starts with* 10.0.1)
- Devices running Windows 11 (osVersion *starts with* 10.0.2)

On Windows apps and policies can also be targeted at user groups. Many apps and policies on Windows are "device" targeted, so even if targeted at a user group, will apply to all subsequent users of that device.

::: zone-end

::: zone pivot="ios"

### Automated Device Enrollment
When devices are enrolled with Automated Device Enrollment, the devices are stamped with the enrollment profile name used during enrollment. Devices can be associated with different enrollment profiles in the Automated Device Enrollment token section under enrollment. Some customers use this to create groups or filters for different enrollment settings, to target different apps or profiles and also for assigning scope tags for role-based access control.

Here are examples of queries commonly used for dynamic security groups.

| Name | Type | Query |
| --- | --- | --- |
| All iOS devices | Dynamic membership rules | (device.deviceOSType -startsWith \"iOS\") |
| All *'use case'* devices | Dynamic membership rules | (device.enrollmentProfileName -eq \"'*use case*'\") |

To apply settings as quickly as possible during enrollment without waiting for dynamic group updates, some customers use a filter based on enrollmentProfileName and target configuration at the *All Devices* virutal group.

- Devices with a specific enrollmentProfileName (enrollmentProfileName *equals* *'use case*')

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