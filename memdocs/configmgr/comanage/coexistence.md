---
title: Third-party MDM coexistence
titleSuffix: Configuration Manager
description: Learn about using a third-party MDM service with Configuration Manager
ms.date: 10/05/2021
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# Third-party MDM coexistence with Configuration Manager

When you concurrently manage Windows 10 or later devices with both Configuration Manager and Microsoft Intune, this functionality is called [co-management](overview.md). When you manage devices with Configuration Manager and enroll to a third-party MDM service, this functionality is called *coexistence*. Having two management authorities for a single device can be challenging if not properly orchestrated between the two. With co-management, Configuration Manager and Intune balance the [workloads](workloads.md) to make sure there are no conflicts. This interaction doesn't exist with third-party services, so there are limitations with the management capabilities of coexistence.

The Configuration Manager client can coexist with a third-party MDM service on a device running Windows 10 version 1709 or later, and that's joined to Azure Active Directory. The device can be either of the following types:

- [Azure AD-joined](/azure/active-directory/devices/azureadjoin-plan) only. (This type is sometimes referred to as "cloud domain-joined")  

- [Hybrid domain-joined](/azure/active-directory/devices/hybrid-azuread-join-plan), where the device is joined to your on-premises Active Directory and registered with your Azure Active Directory.  

> [!Note]  
> It doesn't support [personally-owned devices](/windows/client-management/mdm/mdm-enrollment-of-windows-devices#connecting-personally-owned-devices-bring-your-own-device).  

When the Configuration Manager client detects that a third-party MDM service is also managing the device, it automatically deactivates certain workloads in Configuration Manager. This behavior allows the MDM service to take over these functions. It also prevents conflicting settings on the client that could adversely impact the device and user experience. The following workloads in Configuration Manager are deactivated in this case:

- Resource access policies for VPN, Wi-Fi, email, and certificate settings
- Application management, including legacy packages
- Software update scanning and installation
- Endpoint protection, the Windows Defender suite of antimalware protection features
- Compliance policy for conditional access
- Device configuration
- Office Click-to-Run management

The Configuration Manager client avoids conflict with the third-party management authority by continuing the following read-only operations:

- Hardware and software inventory
- Asset Intelligence
- Software metering
- Power management reporting

For more information on the benefits of co-management with Configuration Manager and Intune, see [Co-management benefits](overview.md#benefits).