---
title: Use standalone media to deploy Windows
titleSuffix: Configuration Manager
description: Use standalone media in Configuration Manager to deploy Windows where bandwidth is limited as an option to refresh, install, or upgrade computers.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 58a0d2ae-de76-401f-b854-7a5243949033
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Use standalone media to deploy Windows without using the network

*Applies to: Configuration Manager (current branch)*

Standalone media in Configuration Manager contains everything required to deploy an OS on a computer. The media includes the boot image, OS image, task sequence policy, applications, drivers, and more. Standalone media deployments let you deploy operating systems in the following conditions:

- In environments where it isn't practical to copy an OS image or other large packages over the network.

- In environments without network connectivity or low-bandwidth network connectivity.

Use standalone media in the following OS deployment scenarios:

- [Refresh an existing computer with a new version of Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

- [Install a new version of Windows on a new computer (bare metal)](install-new-windows-version-new-computer-bare-metal.md)

- [Upgrade Windows to the latest version](upgrade-windows-to-the-latest-version.md)

Complete the steps in one of these OS deployment scenarios. Then use the following sections to prepare for and create the standalone media.

## Unsupported task sequence actions

When you use standalone media, Configuration Manager doesn't support the following actions in the task sequence:

- The [Auto Apply Drivers](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers) step. Automatic application of device drivers from the driver catalog isn't supported. To make a specific set of drivers available to Windows Setup, use the [Apply Driver Package](../understand/task-sequence-steps.md#BKMK_ApplyDriverPackage) step.

- Installing software updates.

- Installing software before deploying the OS.

- Associating users with the destination computer for user device affinity.

- Dynamic package installs with the [Install Package](../understand/task-sequence-steps.md#BKMK_InstallPackage) step.

- Dynamic application installs with the [Install Application](../understand/task-sequence-steps.md#BKMK_InstallApplication) step.

> [!NOTE]
> If your task sequence to deploy an OS includes the **Install Package** step, and you create the standalone media at a central administration site (CAS), an error might occur. The CAS doesn't have the necessary client configuration policies to enable the software distribution agent when the task sequence runs. The following error might appear in the **CreateTsMedia.log** file:
>
> `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`
>
> For standalone media that includes an **Install Package** step, create the standalone media at a primary site that has the software distribution agent enabled
>
> Alternatively, edit the task sequence to add a [Run Command Line](../understand/task-sequence-steps.md#BKMK_RunCommandLine) step after the [Setup Windows and ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) step. This **Run Command Line** step runs the following WMI command to enable the software distribution agent before the first **Install Package** step runs:
>
> ```command
> WMIC /namespace:\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE
> ```

## Configure deployment settings

When you use standalone media to start the OS deployment process, configure the deployment to make the OS available to media. On the **Deployment Settings** page of the deployment, for the **Make available to the following** setting, select one of the following options:

- Configuration Manager clients, media, and PXE

- Only media and PXE

- Only media and PXE (hidden)

## Create the standalone media

You can specify whether the standalone media is a USB flash drive or CD/DVD set. The computer that will start the media must support the option that you choose as a bootable drive. For more information, see [Create standalone media](create-stand-alone-media.md).

## Install the OS from standalone media

To install the OS, insert the standalone media to the computer, and then power it on.

## Next steps

[User experiences for OS deployment](../understand/user-experience.md#task-sequence-wizard)
