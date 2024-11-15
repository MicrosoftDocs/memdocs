---
# required metadata
title: Optimize enrollment restrictions for NXT devices
titleSuffix:
description: Learn how to optimize enrollment restrictions for NXT devices.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 11/19/2024
ms.topic: overview
ms.service: windows-365
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

# Optimize enrollment restrictions

[!INCLUDE [MS confidential, draft docs](../includes/draft-doc.md)]

While [setting up your organization's environment to support NXT devices](deployment-overview.md), you should make sure that your environment's enrollment restrictions don't block NXT devices from enrolling in Intune.

The first time a user signs in to their NXT, the Out of Box Experience (OOBE) joins the device to Microsoft Entra and enrolls it in Microsoft Intune for management. This is the first time the device is introduced to the tenant, and thus it's an Unknown device. After joining Microsoft Entra, it becomes a Corporate-owned device.

If a [device platform restriction]() blocks personal Windows devices, the transition from unknown to corporate-owned device is prevented and Intune enrollment fails. To avoid this, make sure to allow NXT devices to enroll in Intune using one of the following methods:

- [Use a Device Enrollment Manager to bypass all restrictions](mem/intune/enrollment/device-enrollment-manager-enroll).
- [Use an operating system SKU filter to let NXT devices enroll](#use-an-operating-system-sku-filter-to-let-nxt-devices-enroll-in-intune).
- [Preregister NXT devices using corporate identifiers](mem/intune/enrollment/corporate-identifiers-add#add-windows-corporate-identifiers).

Autopilot can't be used to pre-register NXT as corporate devices.

## Use an operating system SKU filter to let NXT devices enroll in Intune

If there's a policy that blocks personally-owned Windows devices from enrolling in Intune it will also block NXT devices. You can create another policy to allow NXT devices to enroll in Intune while still blocking other personally-owned Windows devices.

Follow these steps to create a policy to allow NXT devices to enroll in Intune:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Enrollment** > **Windows** > **Device platform restriction** > **Windows restrictions**.
2. Under **Windows restrictions**, select **Create restriction**.
3. On the **Basics** page, type a **Name** (like *Allowed NXT devices to enroll*) and an optional **Description** > **Next**.
4. On the **Platform settings** page, set the following options:
    - **MDM**: *Allow*
    - **Personally owned devices**: *Allow*
5. Select **Next**.
6. On **Scope tags** page, select **Next**.
7. On **Assignments** page, select **Add all users** > **Edit filter**.
8. On the **Filters** pane, select **Include filtered devices in assignment** > **??NXT devices??” > **Select**.
9. Select **Next**.
10. On the **Review + create** page, select **Create**.
11. On the **Enrollment restrictions** > **Windows restrictions** page, make sure the new policy is above any block policy in priority order.

<!-- ########################## -->
## Next steps

