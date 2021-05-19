---
# required metadata

title: Using Windows Virtual Desktop with Microsoft Intune
titleSuffix: 
description: Guidelines for using Windows Virtual Desktop with Microsoft Intune
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 9/22/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: madakeva
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
---

# Using Windows Virtual Desktop with Intune

[Windows Virtual Desktop](/azure/virtual-desktop/) is a desktop and app virtualization service that runs on Microsoft Azure. It lets end users connect securely to a full desktop from any device. With Microsoft Intune, you can secure and manage your Windows Virtual Desktop VMs with policy and apps at scale, after they're enrolled. 

## Prerequisites 

Currently, Intune supports Windows Virtual Desktop VMs that are: 

- Running Windows 10 Enterprise, version 1809 or later.
- [Hybrid Azure AD-joined](/azure/active-directory/devices/hybrid-azuread-join-plan).
- Set up as [personal remote desktops](/azure/virtual-desktop/configure-host-pool-personal-desktop-assignment-type) in Azure. 
- Enrolled in Intune in one of the following methods: 
    - Configure [Active Directory group policy](/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy) to automatically enroll devices that are hybrid Azure AD joined.
    - [Configuration Manager co-management](/configmgr/comanage/overview).
    - [User self-enrollment via Azure AD Join](../enrollment/windows-enrollment-methods.md#user-self-enrollment-in-intune).

For more information on Windows Virtual Desktop licensing requirements, see [What is Windows Virtual Desktop?](/azure/virtual-desktop/overview#requirements).

Intune treats Windows Virtual Desktop personal VMs the same as Windows 10 Enterprise physical desktops. This treatment lets you use some of your existing configurations and secure the VMs with compliance policy and conditional access. Intune management doesn't depend on or interfere with Windows Virtual Desktop management of the same virtual machine. 

## Limitations

There are some limitations to keep in mind when managing Windows 10 Enterprise remote desktops: 

### Configuration

All VM limitations listed in [Using Windows 10 virtual machines](windows-10-virtual-machines.md) also apply to Windows Virtual Desktop VMs.

Also, the following profiles aren't currently supported:
- [Domain Join](../configuration/device-profiles.md#domain-join)
- [Wi-Fi](../configuration/device-profiles.md#wi-fi)

Make sure that the [RemoteDesktopServices/AllowUsersToConnectRemotely policy](/windows/client-management/mdm/policy-csp-remotedesktopservices#remotedesktopservices-allowuserstoconnectremotely) isn't disabled.

### Remote actions

The following Windows 10 desktop device remote actions aren't supported/recommended for Windows Virtual Desktop VMs:

- Autopilot reset
- BitLocker key rotation
- Fresh Start
- Remote lock
- Reset password
- Wipe

### Retirement

Deleting VMs from Azure leaves orphaned device records in Intune. They'll be automatically [cleaned up](../remote-actions/devices-wipe.md#automatically-delete-devices-with-cleanup-rules) according to the cleanup rules configured for the tenant.

## Next steps

* [Learn more about Windows Virtual Desktops](/azure/virtual-desktop/).
* [Use Windows Virtual Desktop multi-session with Intune](windows-virtual-desktop-multi-session.md)
