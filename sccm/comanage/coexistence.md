---
title: Third-party MDM coexistence
titleSuffix: Configuration Manager
description: Learn about using a third-party MDM service with Configuration Manager 
ms.date: 04/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: ed4dc65e-e5d5-4f75-88ac-f4849ec8fc10
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Third-party MDM coexistence with Configuration Manager

When you concurrently manage Windows 10 devices with both Configuration Manager and Microsoft Intune, this functionality is called [co-management](/sccm/comanage/overview). When you manage devices with Configuration Manager and enroll to a third-party MDM service, this functionality is called *coexistence*. Having two management authorities for a single device can be challenging if not properly orchestrated between the two. With co-management, Configuration Manager and Intune balance the [workloads](/sccm/comanage/workloads) to make sure there are no conflicts. This interaction doesn't exist with third-party services, so there are limitations with the management capabilities of coexistence.

The Configuration Manager client can coexist with a third-party MDM service on a device that's joined to Azure Active Directory. The device can be either of the following types:

- [Azure AD-joined](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan) only. (This type is sometimes referred to as "cloud domain-joined")  

- [Hybrid domain-joined](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan), where the device is joined to your on-premises Active Directory and registered with your Azure Active Directory.  

> [!Note]  
> It doesn't support [personally-owned devices](https://docs.microsoft.com/windows/client-management/mdm/mdm-enrollment-of-windows-devices#connecting-personally-owned-devices-bring-your-own-device).  

When the Configuration Manager client detects that a third-party MDM service is also managing the device, it automatically transitions the following workloads to the coexistence service:

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
