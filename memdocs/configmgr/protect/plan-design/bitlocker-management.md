---
title: Plan for BitLocker management
titleSuffix: Configuration Manager
description: Plan for managing BitLocker Drive Encryption with Configuration Manager
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a4d8cda2-bc9b-4fb4-aa0d-23c31b4fc60b
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Plan for BitLocker management

*Applies to: Configuration Manager (current branch)*

<!-- 3601034 -->

Starting in version 1910, use Configuration Manager to manage BitLocker Drive Encryption (BDE) for on-premises Windows clients. It provides full BitLocker lifecycle management that can replace the use of Microsoft BitLocker Administration and Monitoring (MBAM).

> [!Note]  
> Configuration Manager doesn't enable this optional feature by default. You must enable this feature before using it. For more information, see [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).  

For more information, see [BitLocker overview](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-overview).

> [!TIP]
> To manage encryption on co-managed Windows 10 devices using the Microsoft Endpoint Manager cloud service, switch the [**Endpoint Protection** workload](../../comanage/workloads.md#endpoint-protection) to Intune. For more information on using Intune, see [Windows Encryption](/intune/protect/endpoint-protection-windows-10#windows-encryption).

## Features

Configuration Manager provides the following management capabilities for BitLocker Drive Encryption:

### Client deployment

Deploy the BitLocker client to managed Windows devices running Windows 10 or Windows 8.1

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

- To create a BitLocker management policy, you need the **Full Administrator** role in Configuration Manager.

- The BitLocker recovery service requires HTTPS to encrypt the recovery keys across the network from the Configuration Manage client to the management point. There are two options:

  - HTTPS-enable the IIS website on the management point that hosts the recovery service. This option only applies to Configuration Manager version 2002.<!-- 5925660 -->

  - Configure the management point for HTTPS. This option applies to Configuration Manager versions 1910 or 2002.

  For more information, see [Encrypt recovery data](../deploy-use/bitlocker/encrypt-recovery-data.md).

- To use the BitLocker management reports, install the reporting services point site system role. For more information, see [Configure reporting](../../core/servers/manage/configuring-reporting.md).

    > [!NOTE]
    > For the **Recovery Audit Report** to work from the administration and monitoring website, only use a reporting services point at the primary site.

- To use the self-service portal or the administration and monitoring website, you need a Windows server running IIS. You can reuse a Configuration Manager site system, or use a standalone web server that has connectivity to the site database server. Use a [supported OS version for site system servers](../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md).

    > [!NOTE]
    > Only install the self-service portal and the administration and monitoring website with a primary site database. In a hierarchy, install these websites for each primary site.

- On the web server that will host the self-service portal, install [Microsoft ASP.NET MVC 4.0](https://docs.microsoft.com/aspnet/mvc/mvc4).

- The user account that runs the portal installer script needs SQL **sysadmin** rights on the site database server. During the setup process, the script sets login, user, and SQL role rights for the web server machine account. You can remove this user account from the sysadmin role after you complete setup of the self-service portal and the administration and monitoring website.

- BitLocker Management is not supported on virtual machines (VMs). For this reason some features may not work as expected on virtual machines. For example BitLocker Management will not start the encryption on fixed drives of virtual machines. Additional fixed drives in virtual machines may show as compliant even though they are not encrypted.

> [!TIP]
> By default, the **Enable BitLocker** task sequence step only encrypts *used space* on the drive. BitLocker management uses *full disk* encryption. Configure this task sequence step to enable the option to **Use full disk encryption**. For more information, see [Task sequence steps - Enable BitLocker](../../osd/understand/task-sequence-steps.md#BKMK_EnableBitLocker).

## Next steps

[Encrypt recovery data](../deploy-use/bitlocker/encrypt-recovery-data.md) (an optional prerequisite before deploying policy for the first time)

[Deploy BitLocker management client](../deploy-use/bitlocker/deploy-management-agent.md)
