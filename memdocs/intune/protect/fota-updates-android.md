---
# required metadata

title: Android FOTA Updates
description: Use Microsoft Intune to manage firmware updates on Android devices. A FOTA update can include software and security patches, feature updates, and other changes to the device's firmware. 
keywords:
author: Smritib17 
ms.author: smbhardwaj
manager: dougeby
ms.date: 05/10/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: Jessica Yang
#ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
#ms.custom:
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---
# Android FOTA Updates

You can use Microsoft Intune to manage software updates on the following Android Enterprise devices:

- Fully Managed
- Dedicated  
- Corporate-Owned Work Profile devices

You have two ways to manage software updates on android:  

- Use Firmware Over-the-Air (FOTA), which works for some OEMs.

- If FOTA isn't available you can use Device restrictions profiles, which work for all OEMs.

    1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
    2. Navigate to **Devices** > **Android** > **Configuration profiles** > **Device restrictions**.  
    3. Device restrictions profiles offer control over how the device handles over-the-air updates and allow you to set a freeze period for these updates.  
    > [!NOTE]
    > Not all device manufacturers support over-the-air updates. For more information, see [Corporate-owned Android Enterprise device restriction settings in Microsoft Intune](../configuration/device-restrictions-android-for-work.md)

Firmware Over-the-Air (FOTA) updates allow remotely updating the firmware of devices using a wireless connection, rather than requiring the devices to be physically connected to a computer or network.  

A FOTA update can include software and security patches, feature updates, and other changes to the device's firmware. This method is more efficient, convenient, and more secure than manual updates and can be performed on a scheduled or on-demand basis.  

In the context of FOTA, a deployment is an update policy that includes instructions about the firmware update to be deployed to devices and other update-related settings. For example, Schedule type, and charging requirements.

In addition, Microsoft Intune supports FOTA update management for supported devices from the following manufacturers. Manufacturer-specific FOTA support may offer more controls beyond what Device restrictions profiles offer.  

- **Zebra**: Go to [Zebra LifeGuard Over-the-Air Integration with Microsoft Intune](zebra-lifegaurd-ota-integration.md). This feature is in public preview. For more information, see [Public preview in Microsoft Intune](../fundamentals/public-preview.md).  
- **Samsung**: Go to [Samsung E-FOTA Update Management with Microsoft Endpoint Manager](https://techcommunity.microsoft.com/t5/intune-customer-success/samsung-e-fota-update-management-with-microsoft-endpoint-manager/ba-p/2002552)


