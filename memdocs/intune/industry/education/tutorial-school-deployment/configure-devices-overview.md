---
title: Configure devices with Microsoft Intune
description: Learn how to configure policies and applications in preparation for device deployment.
ms.date: 11/09/2023
ms.topic: tutorial
ms.collection: essentials-manage
author: scottbreenmsft
ms.author: scbree
ms.manager: dougeby
---

# Configure settings and applications with Microsoft Intune

Before distributing devices to your users, you must ensure that the devices will be configured with the required policies, settings, and applications as they get enrolled in Intune.

:::image type="content" source="./images/configure.png" alt-text="The device lifecycle for Intune-managed devices" border="false":::

Microsoft Intune uses Microsoft Entra groups to assign policies and applications to devices.

> [!div class="checklist"]
>In this section you will:
>
> - Create groups
> - Create and assign policies to groups
> - Create and assign applications to groups

## Create groups

✅ Organize devices and users

By organizing devices, students, classrooms, or learning curricula into groups, you can provide students with the resources and configurations they need.

Intune has two main targeting methods:

- **Groups** are created and managed in Entra and can contain users or devices.
  - **Virtual groups** are created by Intune and allow you to target *All devices* and *All users*.
  - **Assigned groups** are used when you want to manually add users or devices to a group.
  - **Dynamic groups** reference rules that you create to assign students or devices to groups, which automate the membership's maintenance of those groups.
- [**Filters**](/mem/intune/fundamentals/filters) allows you to narrow the assignment scope of a policy. For example, use filters to target devices with a specific OS version or a specific manufacturer, target only personal devices or only organization-owned devices, and more. Filters are evaluated dynamically during a device check-in and can therefore sometimes offer a faster dynamic grouping option than an Entra dynamic group.

> [!NOTE]
> Filters are not accessible in Intune for Education.

Two extra groups are precreated if you use **Microsoft School Data Sync (SDS)**: *All teachers* and *All students*. SDS can also be configured to automatically create and maintain groups of students and teachers for each school.

Beyond the defaults, groups can be customized to suit various needs. For example, if you have both *Windows 10* and *Windows 11* devices in your school, you can create groups, such as *Windows 10 devices* and *Windows 11 devices*, to assign different policies and applications to.

> [!TIP]
> **For Windows devices:**
> - If you target applications and policies to a *device dynamic group* based on [an Autopilot *Group Tag*](/autopilot/enrollment-autopilot), they will be applied to the devices as soon as they are enrolled in Intune, before users signs in. This can be useful in bulk enrollment scenarios, where devices are enrolled without requiring users to sign in. Devices can be configured and prepared in advance, before distribution.
> - Applications and policies to a *device dynamic group* based on other attributes, they will be applied to the devices after they are enrolled in Intune, after users gain access to the device.
> 
> **For iOS devices:**
> - If you target applications and policies to a *device dynamic group*, they will be applied to the devices after they are enrolled in Intune, after users gain access to the device.

### [Intune](#tab/intune)

- [Create groups in Entra](/entra/fundamentals/how-to-manage-groups)
- [Use filters when assigning your apps, policies, and profiles in Microsoft Intune](/mem/intune/fundamentals/filters)
- [Create or update a dynamic group in Microsoft Entra ID](/entra/fundamentals/concept-learn-about-groups)
- [Dynamic membership rules for groups in Microsoft Entra ID](/entra/fundamentals/concept-learn-about-groups)
- [Create simpler, more efficient rules for dynamic groups in Microsoft Entra ID](/entra/fundamentals/concept-learn-about-groups)

Here are examples of queries commonly used for dynamic security groups.

| Name | Type | Query |
| --- | --- | --- |
| All Windows devices | Dynamic membership rules | (device.deviceOSType -startsWith \"Windows\") |
| All Autopilot devices | Dynamic membership rules | (device.devicePhysicalIDs -any _ -startsWith \"[ZTDId]\") |
| All non-Autopilot devices | Dynamic membership rules | (device.deviceOSType -startsWith \"Windows\") -and (device.deviceOwnership -eq \"Company\") -and -not(device.devicePhysicalIds -any (_ -startsWith \"[ZTDId]\")) |

### [Intune for Education](#tab/intune-for-education)

- [Create groups in Intune for Education][EDU-1]
- [Manually add or remove users and devices to an existing assigned group][EDU-2]
- [Edit dynamic group rules to accommodate for new devices, locations, or school years][EDU-3]

---

For more information on grouping and targeting options, see [Performance recommendations for Grouping, Targeting, and Filtering in large Microsoft Intune environments](/mem/intune/fundamentals/filters-performance-recommendations).

________________________________________________________

## Next steps

With the groups created, you can configure policies and applications to deploy to your groups.

> [!div class="nextstepaction"]
> [Next: Configure policies >](configure-device-settings.md)

<!-- Reference links in article -->

[EDU-1]: /intune-education/create-groups
[EDU-2]: /intune-education/edit-groups-intune-for-edu
[EDU-3]: /intune-education/edit-groups-intune-for-edu#edit-dynamic-group-rules
