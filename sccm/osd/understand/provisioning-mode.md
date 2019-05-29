---
title: Provisioning mode
titleSuffix: Configuration Manager
description: Learn about client provisioning mode during the Configuration Manager task sequence.
ms.date: 05/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 3e3ff3a4-7a75-41bb-bdf9-33ede9c0e3a3
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Provisioning mode

*Applies to: System Center Configuration Manager (Current Branch)*

During an OS deployment task sequence, Configuration Manager places the client in provisioning mode. (An OS deployment task sequence includes in-place upgrade to Windows 10.) In this state, the client doesn't process policy from the site. This behavior allows the task sequence to run without risk of additional deployments running on the client. When the task sequence completes, either success or handled failure, it exits client provisioning mode.

If the task sequence unexpectedly fails, the client can be left in provisioning mode. For example, if the device restarts in the middle of task sequence processing, and it's unable to recover. An administrator must manually identify and fix clients in this state.


## Client provisioning mode timeout

Starting in version 1902, the task sequence sets a timestamp when it puts the client in provisioning mode. Every 60 minutes, a client in provisioning mode checks the duration of time since the timestamp. If it's been in provisioning mode for more than 48 hours, the client automatically exits provisioning mode and restarts its process.

48 hours is the default provisioning mode timeout value. You can adjust this timer on a device by setting the **ProvisioningMaxMinutes** value in the following registry key: `HKLM\Software\Microsoft\CCM\CcmExec`. If this value doesn't exist or is `0`, the client uses the default 48 hours.


## Process flow diagrams

These diagrams show the process flow for the task sequence and the client.

### Task sequence

The following diagram shows how the task sequence sets provisioning mode:

![Flow diagram of task sequence setting provisioning mode](media/3197824-ts-flow.png)

### Client remediation

The following diagram shows how the client exits provisioning mode:

![Flow diagram of client exiting provisioning mode](media/3197824-client-flow.png)


## See also

[Setup Windows and ConfigMgr](/sccm/osd/understand/task-sequence-steps#BKMK_SetupWindowsandConfigMgr)

[Upgrade Operating System](/sccm/osd/understand/task-sequence-steps#BKMK_UpgradeOS)
