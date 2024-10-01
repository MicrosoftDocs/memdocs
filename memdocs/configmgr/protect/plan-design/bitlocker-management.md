---
title: Plan for BitLocker management
titleSuffix: Configuration Manager
description: Plan for managing BitLocker Drive Encryption with Configuration Manager.
ms.date: 04/08/2022
ms.service: configuration-manager
ms.subservice: protect
ms.topic: conceptual
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# Plan for BitLocker management

*Applies to: Configuration Manager (current branch)*

<!-- 3601034 -->

Use Configuration Manager to manage BitLocker Drive Encryption (BDE) for on-premises Windows clients, which are joined to Active Directory. It provides full BitLocker lifecycle management that can replace the use of Microsoft BitLocker Administration and Monitoring (MBAM).

> [!NOTE]
> Configuration Manager doesn't enable this optional feature by default. You must enable this feature before using it. For more information, see [Enable optional features from updates](../../core/servers/manage/optional-features.md).  

For more general information about BitLocker, see [BitLocker overview](/windows/security/information-protection/bitlocker/bitlocker-overview). For a comparison of BitLocker deployments and requirements, see the [BitLocker deployment comparison chart](/windows/security/information-protection/bitlocker/bitlocker-deployment-comparison).

> [!TIP]
> To manage encryption on co-managed Windows 10 or later devices using the Microsoft Intune cloud service, switch the [**Endpoint Protection** workload](../../comanage/workloads.md#endpoint-protection) to Intune. For more information on using Intune, see [Windows Encryption](/mem/intune/protect/endpoint-protection-windows-10#windows-encryption).

## Features

Configuration Manager provides the following management capabilities for BitLocker Drive Encryption:

### Client deployment

- Deploy the BitLocker client to managed Windows devices running Windows 8.1, Windows 10 or Windows 11.

- Manage BitLocker policies and escrow recovery keys for on-premises and internet-based clients

### Manage encryption policies

- For example: choose drive encryption and cipher strength, configure user exemption policy, fixed data drive encryption settings.

- Determine the algorithms with which to encrypt the device, and the disks that you target for encryption.

- Force users to get compliant with new security policies before using the device.

- Customize your organization's security profile on a per device basis.

- When a user unlocks the OS drive, specify whether to unlock only an OS drive or all attached drives.

### Compliance reports

Built-in reports for:

- Encryption status per volume or per device
- The primary user of the device
- Compliance status
- Reasons for non-compliance

### Administration and monitoring website

Allow other personas in your organization outside of the Configuration Manager console to help with key recovery, including key rotation and other BitLocker-related support. For example, help desk administrators can help users with key recovery.

> [!TIP]
> Starting in version 2107, you can also get BitLocker recovery keys for a tenant-attached device from the Microsoft Intune admin center.<!--6979225--> For more information, see [Tenant attach: BitLocker recovery keys](../../tenant-attach/bitlocker-recovery-keys.md).

### User self-service portal

Let users help themselves with a single-use key for unlocking a BitLocker encrypted device. Once this key is used, it generates a new key for the device.

## Prerequisites

### General prerequisites

- To create a BitLocker management policy, you need the **Full Administrator** role in Configuration Manager.

- To use the BitLocker management reports, install the reporting services point site system role. For more information, see [Configure reporting](../../core/servers/manage/configuring-reporting.md).

    > [!NOTE]
    > For the **Recovery Audit Report** to work from the administration and monitoring website, only use a reporting services point at the primary site.

### Prerequisites for clients

<!-- memdocs#2098 -->

- The device requires a TPM chip that's enabled in the BIOS and is resettable from Windows.

    Microsoft recommends devices with TPM version 2.0 or later. Devices with TPM version 1.2 may not properly support all BitLocker functionality.

- The computer's hard disk requires a BIOS that's compatible with TPM and that supports USB devices during computer startup.

> [!NOTE]
> Uploading of the TPM password hash mainly pertains to versions of Windows before Windows 10. Windows 10 or later by default doesn't save the TPM password hash, so these devices don't normally upload it. For more information, see [About the TPM owner password](/windows/security/information-protection/tpm/change-the-tpm-owner-password#about-the-tpm-owner-password).

BitLocker management doesn't support all client types that are supported by Configuration Manager. For more information, see [Supported configurations](#supported-configurations).

### Prerequisites for the recovery service

- In version 2010 and earlier, the BitLocker recovery service requires HTTPS to encrypt the recovery keys across the network from the Configuration Manager client to the management point. Use one of the following options:

  - HTTPS-enable the IIS website on the management point that hosts the recovery service.<!-- 5925660 -->

  - Configure the management point for HTTPS.

  For more information, see [Encrypt recovery data over the network](../deploy-use/bitlocker/encrypt-recovery-data-transit.md).

  > [!NOTE]
  > When both the site and clients are running Configuration Manager version 2103 or later, clients send their recovery keys to the management point over the secure client notification channel. If any clients are on version 2010 or earlier, they need an HTTPS-enabled recovery service on the management point to escrow their keys.
  >
  > Starting in version 2103, since clients use the secure client notification channel to escrow keys, you can enable the Configuration Manager site for enhanced HTTP. This configuration doesn't affect the functionality of BitLocker management in Configuration Manager.<!-- 11108795 -->

- In version 2010 and earlier, to use the recovery service, you need at least one management point not in a replica configuration. Although the BitLocker recovery service installs on a management point that uses a database replica, clients can't escrow recovery keys. Then BitLocker won't encrypt the drive. Disable the BitLocker recovery service on any management point with a database replica.<!-- 7813149 -->

  Starting in version 2103, the recovery service supports management points that use a database replica.<!-- 9503186 -->

### Prerequisites for BitLocker portals

- To use the self-service portal or the administration and monitoring website, you need a Windows server running IIS. You can reuse a Configuration Manager site system, or use a standalone web server that has connectivity to the site database server. Use a [supported OS version for site system servers](../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md).

- On the web server that will host the self-service portal, install [Microsoft ASP.NET MVC 4.0](/aspnet/mvc/mvc4) and .NET Framework 3.5 feature before staring the install process. Other required Windows server roles and features will be installed automatically during the portal installation process.

    > [!TIP]
    > You don't need to install any version of Visual Studio with ASP.NET MVC.<!-- MEMDocs#1463 -->

- The user account that runs the portal installer script needs SQL Server **sysadmin** rights on the site database server. During the setup process, the script sets login, user, and SQL Server role rights for the web server machine account. You can remove this user account from the sysadmin role after you complete setup of the self-service portal and the administration and monitoring website.

## Supported configurations

- BitLocker management isn't supported on virtual machines (VMs) or on server editions. For example, BitLocker management won't start the encryption on fixed drives of virtual machines. Additionally fixed drives in virtual machines may show as compliant even though they aren't encrypted.

- In version 2010 and earlier, Microsoft Entra joined, workgroup clients, or clients in untrusted domains aren't supported. In these earlier versions of Configuration Manager, BitLocker management only supports devices that are joined to on-premises Active Directory including Microsoft Entra hybrid joined devices. This configuration is to authenticate with the recovery service to escrow keys.

  Starting in version 2103, Configuration Manager supports all client join types for BitLocker management. However, the client-side BitLocker user interface component is still only supported on Active Directory-joined and Microsoft Entra hybrid joined devices.

- Starting in version 2010, you can now manage BitLocker policies and escrow recovery keys over a [cloud management gateway (CMG)](../../core/clients/manage/cmg/overview.md). This change also provides support for BitLocker management via internet-based client management (IBCM). There's no change to the setup process for BitLocker management. This improvement supports domain-joined and hybrid domain-joined devices.<!--6979223--> For more information, see [Deploy management agent: Recovery service](../deploy-use/bitlocker/recovery-service.md).

   - If you have BitLocker management policies that you created before you updated to version 2010, to make them available to internet-based clients via CMG:
      1. In the Configuration Manager console, open the properties of the existing policy.
      1. Switch to the **Client Management** tab.
      1. Select **OK** or **Apply** to save the policy. This action revises the policy so that it's available to clients over the CMG.

- By default, the **Enable BitLocker** task sequence step only encrypts *used space* on the drive. BitLocker management uses *full disk* encryption. Configure this task sequence step to enable the option to **Use full disk encryption**.

  Starting in version 2203, you can configure this task sequence step to escrow the BitLocker recovery information for the OS volume to Configuration Manager.<!--10454717-->

  For more information, see [Task sequence steps - Enable BitLocker](../../osd/understand/task-sequence-steps.md#enable-bitlocker).

> [!IMPORTANT]
> The `Invoke-MbamClientDeployment.ps1` PowerShell script is for [stand-alone MBAM](/microsoft-desktop-optimization-pack/mbam-v25/) only. It should not be used with Configuration Manager BitLocker Management.

## Next steps

[Encrypt recovery data over the network](../deploy-use/bitlocker/encrypt-recovery-data-transit.md)
