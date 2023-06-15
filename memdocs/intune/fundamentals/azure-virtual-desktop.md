---
# required metadata

title: Using Azure Virtual Desktop single-session with Microsoft Endpoint Manager
titleSuffix: 
description: Guidelines for using Azure Virtual Desktop single-session with Microsoft Endpoint Manager. 
keywords:
author: Smritib17  
ms.author: smbhardwaj
manager: dougeby
ms.date: 9/02/2021
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
- [Hybrid Azure AD-joined](/azure/active-directory/devices/hybrid-azuread-join-plan) and enrolled in Intune in one of the following methods: 
    - Configure [Active Directory group policy](/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy) to automatically enroll devices that are hybrid Azure AD joined.
    - [Configuration Manager co-management](/configmgr/comanage/overview).
    - [User self-enrollment via Azure AD Join](/mem/intune/fundamentals/deployment-guide-enroll#user-self-enrollment-in-intune).
- Azure AD-joined and enrolled in Intune by enabling [Enroll the VM with Intune](/azure/virtual-desktop/deploy-azure-ad-joined-vm#deploy-azure-ad-joined-vms) in the Azure portal.

For more information on Azure Virtual Desktop licensing requirements, see [What is Azure Virtual Desktop?](/azure/virtual-desktop/overview#requirements).

For information about working with multi-session remote desktops, see [Windows 10 or Windows 11 Enterprise multi-session remote desktops](azure-virtual-desktop-multi-session.md).

Intune treats Azure Virtual Desktop personal VMs the same as Windows 10 or Windows 11 Enterprise physical desktops. This treatment lets you use some of your existing configurations and secure the VMs with compliance policy and conditional access. Intune management doesn't depend on or interfere with Azure Virtual Desktop management of the same virtual machine. 

## Limitations

There are some limitations to keep in mind when managing Windows 10 Enterprise remote desktops: 

### Configuration

All VM limitations listed in [Using Windows 10 virtual machines](windows-10-virtual-machines.md) also apply to Azure Virtual Desktop VMs.

Also, the following profiles aren't currently supported:
- [Domain Join](../configuration/device-profiles.md#domain-join)
- [Wi-Fi](../configuration/device-profiles.md#wi-fi)

Make sure that the [RemoteDesktopServices/AllowUsersToConnectRemotely policy](/windows/client-management/mdm/policy-csp-remotedesktopservices#remotedesktopservices-allowuserstoconnectremotely) isn't disabled.

> [!NOTE]
> Configuration and compliance policies for Secure Boot and features leveraging vTPM (Virtual Trusted Platform Module) are not supported at this time for Azure Virtual Desktop VMs.

### Remote actions

The following Windows 10 desktop device remote actions aren't supported/recommended for Azure Virtual Desktop VMs:

- Autopilot reset
- BitLocker key rotation
- Fresh Start
- Remote lock
- Reset password
- Wipe

### Retirement

Deleting VMs from Azure leaves orphaned device records in Intune. They'll be automatically [cleaned up](../remote-actions/devices-wipe.md#automatically-delete-devices-with-cleanup-rules) according to the cleanup rules configured for the tenant.

### Known issues

The following table provides a set of known issues along with more information about each issue.

| Issue | More   information |
|---|---|
| Cannot auto-enroll if tenant has more than one MDM provider | This issue will be fixed in the future. |
| Modern apps, such as Universal Windows Platform (UWP) apps, are not working correctly if [FSLogix](/fslogix/overview) is configured | Using FSLogix and Modern apps could cause compatibility issues. We recommend that you don’t configure Modern apps when FSLogix is configured.|

## Next steps

* [Learn more about Azure Virtual Desktops](/azure/virtual-desktop/).
* [Use Azure Virtual Desktop multi-session with Intune](./azure-virtual-desktop-multi-session.md)
