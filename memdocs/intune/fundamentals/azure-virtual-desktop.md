---
# required metadata

title: Using Azure Virtual Desktop single-session with Microsoft Intune
titleSuffix: 
description: Guidelines for using Azure Virtual Desktop single-session with Microsoft Intune. 
keywords:
author: Smritib17  
ms.author: smbhardwaj
manager: dougeby
ms.date: 02/13/2025
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: madakeva
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-classic; get-started
ms.collection:
- tier2
- M365-identity-device-management
---

# Using Azure Virtual Desktop with Intune

[Azure Virtual Desktop](/azure/virtual-desktop/) is a desktop and app virtualization service that runs on Microsoft Azure. It lets end users connect securely to a full desktop from any device. With Microsoft Intune, you can secure and manage your Azure Virtual Desktop VMs with policy and apps at scale, after they're enrolled.

## Prerequisites

Currently, for single-session, Intune supports Azure Virtual Desktop VMs that are:

- Running Windows 10 Enterprise, version 1809 or later, or running Windows 11.
- Set up as [personal remote desktops](/azure/virtual-desktop/configure-host-pool-personal-desktop-assignment-type) in Azure.
- [Microsoft Entra hybrid joined](/azure/active-directory/devices/hybrid-azuread-join-plan) and enrolled in Intune in one of the following methods:
  - Configure [Active Directory group policy](/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy) to automatically enroll devices that are Microsoft Entra hybrid joined.
  - [Configuration Manager co-management](/configmgr/comanage/overview).
  - [User self-enrollment via Microsoft Entra join](deployment-guide-enrollment-windows.md#byod-user-enrollment).
- Microsoft Entra joined and enrolled in Intune by enabling [Enroll the VM with Intune](/azure/virtual-desktop/deploy-azure-ad-joined-vm#deploy-azure-ad-joined-vms) in the Azure portal.
- Under the same tenant as Intune

For more information on Azure Virtual Desktop licensing requirements, see [What is Azure Virtual Desktop?](/azure/virtual-desktop/overview#requirements).

For information about working with multi-session remote desktops, see [Windows 10 or Windows 11 Enterprise multi-session remote desktops](azure-virtual-desktop-multi-session.md).

Intune treats Azure Virtual Desktop personal VMs the same as Windows 10 or Windows 11 Enterprise physical desktops. This treatment lets you use some of your existing configurations and secure the VMs with compliance policy and Conditional Access. Intune management doesn't depend on or interfere with Azure Virtual Desktop management of the same virtual machine.

## Limitations

There are some limitations to keep in mind when managing Windows 10 Enterprise remote desktops:

### Configuration

All VM limitations listed in [Using Windows 10 virtual machines](windows-10-virtual-machines.md) also apply to Azure Virtual Desktop VMs.

Also, the following profiles aren't currently supported:

- [Domain Join](../configuration/device-profiles.md#domain-join)
- [Wi-Fi](../configuration/device-profiles.md#wi-fi)

Make sure that the [RemoteDesktopServices/AllowUsersToConnectRemotely policy](/windows/client-management/mdm/policy-csp-remotedesktopservices#remotedesktopservices-allowuserstoconnectremotely) isn't disabled.

### Cloning physical and virtual devices

Intune does not support using a cloned image of a computer that is already enrolled. This includes both physical and virtual devices such as Azure Virtual Desktop (AVD). When device enrollment or identity tokens are replicated between devices, Intune device enrollment or synchronization failures will occur.

- For more information, see [Mobile device enrollment - Windows Client Management](/windows/client-management/mobile-device-enrollment) and [Certificate authentication device enrollment - Windows Client Management](/windows/client-management/certificate-authentication-device-enrollment).
- For information on disabling token roaming in AVD, see [Using Azure Virtual Desktop multi-session with Microsoft Intune](azure-virtual-desktop-multi-session.md#prerequisites).
- For information on troubleshooting issues related to image cloning, see [Error hr 0x8007064c: The machine is already enrolled](/troubleshoot/mem/intune/troubleshoot-windows-enrollment-errors#error-hr-0x8007064c-the-machine-is-already-enrolled).

### Remote actions

The following Windows 10 desktop device remote actions aren't supported/recommended for Azure Virtual Desktop VMs:

- Autopilot reset
- BitLocker key rotation
- Fresh Start
- Remote lock
- Reset password
- Wipe

### Retirement

Deleting VMs from Azure leaves orphaned device records in Intune. They'll be automatically [cleaned up](../remote-actions/devices-wipe.md#automatically-remove-devices-with-cleanup-rules) according to the cleanup rules configured for the tenant.

### Known issues

The following table provides a set of known issues along with more information about each issue.

| Issue | More   information |
|---|---|
| Can't auto-enroll if tenant has more than one MDM provider | This issue will be fixed in the future. |
| Modern apps, such as Universal Windows Platform (UWP) apps, aren't working correctly if [FSLogix](/fslogix/overview) is configured | Using FSLogix and Modern apps could cause compatibility issues. We recommend that you don't configure Modern apps when FSLogix is configured.|

## Next steps

* [Learn more about Azure Virtual Desktops](/azure/virtual-desktop/).
* [Use Azure Virtual Desktop multi-session with Intune](./azure-virtual-desktop-multi-session.md)
