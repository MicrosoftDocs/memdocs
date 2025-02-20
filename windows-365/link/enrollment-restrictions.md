---
# required metadata
title: Optimize enrollment restrictions for Windows 365 Link devices
titleSuffix:
description: Learn how to optimize enrollment restrictions for Windows 365 Link devices.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 11/19/2024
ms.topic: overview
ms.service: windows-365-link
ms.subservice:
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: sajelaci
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started; intro-hub-or-landing
ms.collection:
- M365-identity-device-management
- tier2
---

# Configure enrollment restrictions

While [setting up your organization's environment to support Windows 365 Link](deployment-overview.md), you should make sure that your environment's enrollment restrictions don't block Windows 365 Link devices from enrolling in Intune.

The first time a user signs in to their Windows 365 Link, the Out of Box Experience (OOBE) joins the device to Microsoft Entra and enrolls it in Microsoft Intune for management. This is the first time the device is introduced to Intune, and thus it's an Unknown device. Because the device is Microsoft Entra joined, Intune sets the ownership to Corporate owned after the Intune enrollment process completes.

If a [device platform restriction]() blocks personally owned devices, Windows 365 Link devices are prevented from completing Intune enrollment. To avoid this prevention, make sure to allow Windows 365 Link devices to enroll in Intune using one of the following methods:

- [Use a Device Enrollment Manager to bypass all restrictions](/mem/intune-service/enrollment/device-enrollment-manager-enroll).
- [Use an operating system SKU filter to let Windows 365 Link devices enroll](#use-an-operating-system-sku-filter-to-let-windows-365-link-devices-enroll-in-intune).
- [Preregister Windows 365 Link devices using corporate identifiers](/mem/intune-service/enrollment/corporate-identifiers-add#add-windows-corporate-identifiers).

Windows 365 Link devices don't currently support Autopilot.

## Use an operating system SKU filter to let Windows 365 Link devices enroll in Intune

If there's a policy that blocks personally owned Windows devices from enrolling in Intune it also blocks Windows 365 Link devices. You can create another policy with higher priority to allow Windows 365 Link devices to enroll in Intune while still blocking other personally owned Windows devices.

Follow these steps to create a policy to allow users to enroll Windows 365 Link devices in Intune:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Enrollment** > **Windows** > **Device platform restriction** > **Windows restrictions**.
2. Under **Windows restrictions**, select **Create restriction**.
3. On the **Basics** page, type a **Name** (like *Allow enrollment of Windows 365 Link devices*) and an optional **Description** > **Next**.
4. On the **Platform settings** page, set the following options:
    - **MDM**: *Allow*
    - **Personally owned devices**: *Allow*
5. Select **Next**.
6. On **Scope tags** page, select **Next**.
7. On **Assignments** page, select **Add all users** > **Edit filter**.
8. On the **Filters** pane, select **Include filtered devices in assignment** > **Windows 365 Link** > **Select**.
9. Select **Next**.
10. On the **Review + create** page, select **Create**.
11. On the **Enrollment restrictions** > **Windows restrictions** page, make sure the new policy is above any block policy in priority order.

For more information about Intune platform enrollment restrictions, see [Create device platform restrictions](/mem/intune-service/enrollment/create-device-platform-restrictions).

<!-- ########################## -->
## Next steps

[Suppress single sign-on consent prompt](single-sign-on-suppress.md).
