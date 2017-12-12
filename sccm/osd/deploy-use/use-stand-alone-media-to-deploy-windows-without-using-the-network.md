---
title: Use stand-alone media to deploy Windows without using the network
titleSuffix: "Configuration Manager"
description: "Use stand-alone media in Configuration Manager to deploy operating systems where bandwidth is limited or as an option to refresh, install, or upgrade computers."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 58a0d2ae-de76-401f-b854-7a5243949033
caps.latest.revision: 16
author: aczechowski
ms.author: aaroncz
manager: angrobe

---
# Use stand-alone media to deploy Windows without using the network in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Stand-alone media in System Center Configuration Manager contains everything that is required to deploy an  operating system on a computer. This includes the boot image, operating system image, and task sequence to install the operating system, including applications, drivers, and so on. Stand-alone media deployments let you deploy operating systems in the following conditions:  

-   In environments where it is not practical to copy an operating system image or other large packages over the network.  

-   In environments without network connectivity or low bandwidth network connectivity.  

You can use stand-alone media in the following operating system deployment scenarios:  

-   [Refresh an existing computer with a new version of Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Install a new version of Windows on a new computer (bare metal)](install-new-windows-version-new-computer-bare-metal.md)  

-   [Upgrade Windows to the latest version](upgrade-windows-to-the-latest-version.md)  

 Complete the steps in one of the operating system deployment scenarios and then use the following sections to prepare for and create the stand-alone media.  

## Task sequence actions not supported when using stand-alone media  
 If  you have completed the steps in one of the supported operating system deployment scenarios, the task sequence to deploy, or upgrade, the operating system has been created and  all associated content has been distributed to a distribution point. When you use stand-alone media, the following actions are not supported in the task sequence:  

-   The Auto Apply Drivers step in the task sequence. Automatic application of device drivers from the driver catalog is not supported, but you can choose the Apply Driver Package step to make a specified set of drivers available to Windows Setup.  

-   Installing software updates.  

-   Installing software before deploying the  operating system.  

-   Associating users with the destination computer to support user device affinity.  

-   Dynamic package installs via the Install Packages task.  

-   Dynamic application installs via the Install Application task.  

> [!NOTE]  
>  If your task sequence to deploy an operating system includes  the [Install Package](../understand/task-sequence-steps.md#BKMK_InstallPackage) step and you create the stand-alone media at a central administration site, an error might occur. The central administration site does not have the necessary client configuration policies that are required to enable the software distribution agent during the execution of the task sequence. The following error might appear in the CreateTsMedia.log file:  
>   
>  `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`
>   
>  For stand-alone media that includes an **Install Package** step, you must create the stand-alone media at a primary site that has the software distribution agent enabled or add a [Run Command Line](../understand/task-sequence-steps.md#BKMK_RunCommandLine) step after the [Setup Windows and ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) step and before the first **Install Package** step in the task sequence. The **Run Command Line** step runs a WMIC command to enable the software distribution agent before the first Install package step runs. You can use the following in your **Run Command Line** task sequence step:  
>   
>  **Command Line**: **WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE**  

## Configure deployment settings  
 When you use stand-alone media to start the operating system deployment process, you must configure the deployment to make the operating system available to media. You can configure this on the **Deployment Settings** page of the Deploy Software Wizard or the **Deployment Settings** tab in the properties for the deployment.  For the **Make available to the following** setting, configure one of the following:  

-   **Configuration Manager clients, media and PXE**  

-   **Only media and PXE**  

-   **Only media and PXE (hidden)**  

## Create the stand-alone media  
 You can specify whether the  stand-alone media is a USB flash drive or CD/DVD set. The computer that will start the media must support the option that you choose as  a bootable drive. For more information, see [Create stand-alone media](create-stand-alone-media.md).  

## Install the operating system from stand-alone media  
 Insert the stand-alone media in a bootable drive on the computer, and then power it on to install the operating system.  
