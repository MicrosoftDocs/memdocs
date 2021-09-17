---
title: Plan for BitLocker management
titleSuffix: Configuration Manager
description: Plan for managing BitLocker Drive Encryption with Configuration Manager
ms.date: 04/14/2021
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a4d8cda2-bc9b-4fb4-aa0d-23c31b4fc60b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# Plan for BitLocker management

*Applies to: Configuration Manager (current branch)*

<!-- 3601034 -->

Use Configuration Manager to manage BitLocker Drive Encryption (BDE) for on-premises Windows clients, which are joined to Active Directory. It provides full BitLocker lifecycle management that can replace the use of Microsoft BitLocker Administration and Monitoring (MBAM).

> [!NOTE]
> Configuration Manager doesn't enable this optional feature by default. You must enable this feature before using it. For more information, see [Enable optional features from updates](../../core/servers/manage/optional-features.md).  

For more general information about BitLocker, see [BitLocker overview](/windows/security/information-protection/bitlocker/bitlocker-overview). For a comparison of BitLocker deployments and requirements, see the [BitLocker deployment comparison chart](/windows/security/information-protection/bitlocker/bitlocker-deployment-comparison).

> [!TIP]
> To manage encryption on co-managed Windows 10 devices using the Microsoft Endpoint Manager cloud service, switch the [**Endpoint Protection** workload](../../comanage/workloads.md#endpoint-protection) to Intune. For more information on using Intune, see [Windows Encryption](/intune/protect/endpoint-protection-windows-10#windows-encryption).

## Features

Configuration Manager provides the following management capabilities for BitLocker Drive Encryption:

### Client deployment

- Deploy the BitLocker client to managed Windows devices running Windows 10 or Windows 8.1

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

### User self-service portal

Let users help themselves with a single-use key for unlocking a BitLocker encrypted device. Once this key is used, it generates a new key for the device.

## Prerequisites

### General prerequisites

- To create a BitLocker management policy, you need the **Full Administrator** role in Configuration Manager.

- To use the BitLocker management reports, install the reporting services point site system role. For more information, see [Configure reporting](../../core/servers/manage/configuring-reporting.md).

    > [!NOTE]
    > For the **Recovery Audit Report** to work from the administration and monitoring website, only use a reporting services point at the primary site.

### Prerequisites for the recovery service

- The BitLocker recovery service requires HTTPS to encrypt the recovery keys across the network from the Configuration Manager client to the management point. Use one of the following options:

  - Enable the site for enhanced HTTP. This option applies to version 2103 or later.<!-- 9503186 -->

  - HTTPS-enable the IIS website on the management point that hosts the recovery service. This option applies to version 2002 or later.<!-- 5925660 -->

  - Configure the management point for HTTPS. This option applies to all supported Configuration Manager versions.

  For more information, see [Encrypt recovery data over the network](../deploy-use/bitlocker/encrypt-recovery-data-transit.md).

- In version 2010 and earlier, to use the recovery service, you need at least one management point not in a replica configuration. Although the BitLocker recovery service installs on a management point that uses a database replica, clients can't escrow recovery keys. Then BitLocker won't encrypt the drive. Disable the BitLocker recovery service on any management point with a database replica.<!-- 7813149 -->

  Starting in version 2103, the recovery service supports management points that use a database replica.<!-- 9503186 -->

### Prerequisites for BitLocker portals

- To use the self-service portal or the administration and monitoring website, you need a Windows server running IIS. You can reuse a Configuration Manager site system, or use a standalone web server that has connectivity to the site database server. Use a [supported OS version for site system servers](../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md).

    > [!NOTE]
    > Starting in version 2006, you can install the BitLocker self-service portal and the administration and monitoring website at the central administration site.<!-- 5925693 -->
    >
    > In version 2002 and earlier, only install the self-service portal and the administration and monitoring website with a primary site database. In a hierarchy, install these websites for each primary site.

- On the web server that will host the self-service portal, install [Microsoft ASP.NET MVC 4.0](/aspnet/mvc/mvc4) and .NET Framework 3.5 feature before staring the install process. Other required Windows server roles and features will be installed automatically during the portal installation process.

    > [!TIP]
    > You don't need to install any version of Visual Studio with ASP.NET MVC.<!-- MEMDocs#1463 -->

- The user account that runs the portal installer script needs SQL Server **sysadmin** rights on the site database server. During the setup process, the script sets login, user, and SQL Server role rights for the web server machine account. You can remove this user account from the sysadmin role after you complete setup of the self-service portal and the administration and monitoring website.

## Supported configurations

- BitLocker management isn't supported on virtual machines (VMs) or on server editions. For example, BitLocker management won't start the encryption on fixed drives of virtual machines. Additionally fixed drives in virtual machines may show as compliant even though they aren't encrypted.

- Azure Active Directory (Azure AD)-joined, workgroup clients, or clients in untrusted domains aren't supported. BitLocker management in Configuration Manager only supports devices that are joined to on-premises Active Directory. Hybrid Azure AD-joined devices are also supported. This configuration is to authenticate with the recovery service to escrow keys.

- Starting in version 2010, you can now manage BitLocker policies and escrow recovery keys over a [cloud management gateway (CMG)](../../core/clients/manage/cmg/overview.md). This change also provides support for BitLocker management via internet-based client management (IBCM). There's no change to the setup process for BitLocker management. This improvement supports domain-joined and hybrid domain-joined devices.<!--6979223--> For more information, see [Deploy management agent: Recovery service](../deploy-use/bitlocker/deploy-management-agent.md#recovery-service).

   -  If you have BitLocker management policies that you created before you updated to version 2010, to make them available to internet-based clients via CMG:
      1. In the Configuration Manager console, open the properties of the existing policy.
      1. Switch to the **Client Management** tab.
      1. Select **OK** or **Apply** to save the policy. This action revises the policy so that it's available to clients over the CMG.

- By default, the **Enable BitLocker** task sequence step only encrypts *used space* on the drive. BitLocker management uses *full disk* encryption. Configure this task sequence step to enable the option to **Use full disk encryption**. For more information, see [Task sequence steps - Enable BitLocker](../../osd/understand/task-sequence-steps.md#BKMK_EnableBitLocker).

> [!Important]
> The `Invoke-MbamClientDeployment.ps1` PowerShell script is for [stand-alone MBAM](/microsoft-desktop-optimization-pack/mbam-v25/) only. It should not be used with Configuration Manager BitLocker Management.

## Next steps

[Encrypt recovery data over the network](../deploy-use/bitlocker/encrypt-recovery-data-transit.md)
