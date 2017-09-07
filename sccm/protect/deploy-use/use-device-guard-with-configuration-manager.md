---
title: "How to manage Windows Device Guard | Microsoft Docs"
description: "Learn how to use System Center Configuration Manager to manage Windows Device Guard."
ms.custom: na
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.reviewer: dudeso
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5e5d854c-9cc1-4dd8-b33f-0fcac675b395
caps.latest.revision: 13
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe

---


# Device Guard management with Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

## Introduction
Device Guard is a group of Windows 10 features that are designed to protect PCs against malware and other untrusted software. It prevents malicious code from running by ensuring that only approved code, that you know, can be run.

Device Guard encompasses both software and hardware-based security functionality. Configurable code integrity is a software-based security layer that enforces an explicit list of software that is allowed to run on a PC. On its own, configurable code integrity does not have any hardware or firmware prerequisites. Device Guard policies deployed with Configuration Manager enable a configurable code integrity policy on PCs in targeted collections that meet the minimum Windows version and SKU requirements outlined in this topic. Optionally, hypervisor-based protection of code integrity policies deployed through Configuration Manager can be enabled through Group Policy on capable hardware.

To learn more about Device Guard, read the [Device Guard deployment guide](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-deployment-guide).

## Using Device Guard with Configuration Manager

You can use Configuration Manager to deploy a Device Guard policy that lets you configure the mode in which Device Guard runs on PCs in a collection. 

You can configure one of the following modes:

1.	**Enforcement enabled** - Only trusted executables are allowed to run.
2.	**Audit only** - Allow all executables to run, but log untrusted executables that run in the local client event log.

>[!TIP]
>In this version of Configuration Manager, Device Guard is a pre-release feature. To enable it, see [Pre-release features in System Center Configuration Manager](/sccm/core/servers/manage/pre-release-features).

## What can run when you deploy a Device Guard policy?

Windows Device Guard lets you strongly control what can run on PCs you manage. This feature can be useful for PCs in high-security departments, where it's vital that unwanted software cannot run.

When you deploy a policy, typically, the following executables can run:

- Windows operating system components
- Hardware Dev Center drivers (that have Windows Hardware Quality Labs signatures)
- Windows Store apps
- The Configuration Manager client 
- All software deployed through Configuration Manager that PCs install after the Device Guard policy is processed. 
- Updates to windows components from:
	- Windows Update
	- Windows Update for Business
	- Windows Server Update Services
	- Configuration Manager

>[!IMPORTANT]
>These items do not include any software that is *not* built-into Windows that automatically updates from the internet or third-party software updates whether they are installed via any of the update mechanisms mentioned previously, or from the internet. Only software changes that are deployed though the Configuration Manager client can run.

## Before you start

Before you configure or deploy Device Guard policies, read the following information:

- Device Guard management is a pre-release feature for Configuration Manager, and is subject to change.
- To use Device Guard with Configuration Manager, PCs you manage must be running the Windows 10 Enterprise version 1703, or later.
- Once a policy is successfully processed on a client PC, Configuration Manager is configured as a Managed Installer on that client, and software deployed through SCCM after the policy processes is automatically trusted. Software installed by Configuration Managed before the Device Guard policy processes is not automatically trusted.
- Client PCs must have connectivity to their Domain Controller in order for a Device Guard policy to be processed successfully.
- The default compliance evaluation schedule for Device Guard policies, configurable during deployment, is every 1 day. If issues in policy processing are observed, it may be beneficial to configure the compliance evaluation schedule to be shorter, for example every hour. This schedule dictates how often clients reattempt to process a Device Guard policy when a failure.
- Regardless of the enforcement mode you select, when you deploy a Device Guard policy, client PCs cannot run HTML applications with the extension .hta.

## How to create a Device Guard policy
1.	In the Configuration Manager console, click **Assets and Compliance**.
2.	In the **Assets and Compliance** workspace, expand **Endpoint Protection**, and then click **Device Guard Policies**.
3.	On the **Home** tab, in the **Create** group, click **Create Device Guard Policy**.
4.	On the **General** page of the **Create Device Guard Policy Wizard**, specify the following settings:
	- **Name** - Enter a unique name for this Device Guard policy. 
	- **Description** - Optionally, enter a description for the policy that helps you identify it in the Configuration Manager console.
	- **Enforcement Mode** - Choose one of the following enforcement methods for Device Guard on the client PC.
		- **Enforcement Enabled** - Only allow trusted executables are allowed to run.
		- **Audit Only** - Allow all executables to run, but log untrusted executables that run in the local client event log.
5.	On the **Inclusions** tab of the **Create Device Guard Policy Wizard**, click **Add** if you want to optionally add trust for specific files or folders on PCs. 
6.	In the **Add Trusted File or Folder** dialog box, specify information about the file or folder that you want to trust. You can either specify a local file or folder path or connect to a remote device to which you have permission to connect and specify a file or folder path on that device.
When you add trust for specific files for folders in a Device Guard policy you can:
	- Overcome issues with managed installer behaviors
	- Trust line-of-business apps that cannot be deployed with Configuration Manager
	- Trust apps that are included in an operating system deployment image. 
7.	Click **Next**, then complete the wizard.

>[!IMPORTANT]
>The inclusion of trusted files or folders is only supported on client PCs running version 1706 or later of the Configuration Manager client. If any inclusion rules are included in a Device Guard policy and the policy is then deployed to a client PC running an earlier version on the Configuration Manager client, the policy will fail to be applied. Upgrading these older clients will resolve this issue. Policies that do not include any inclusion rules may still be applied on older versions of the Configuration Manager client.

## How to deploy a Device Guard policy
1.	In the Configuration Manager console, click **Assets and Compliance**.
2.	In the **Assets and Compliance** workspace, expand **Endpoint Protection**, and then click **Device Guard Policies**.
3.	From the list of policies, select the one you want to deploy, and then, on the **Home** tab, in the **Deployment** group, click **Deploy**.
4.	In the **Deploy Device Guard Policy** dialog box, select the collection to which you want to deploy the policy. Then, configure a schedule for when clients evaluate the policy. Finally, select whether the client can evaluate the policy outside of any configured maintenance windows.
5.	When you are finished, click **OK** to deploy the policy. 

Once the policy is processed on a client PC, a restart is scheduled on that client according to the **Client Settings** for **Computer Restart**.
Until you restart the client PC, the policy does not take effect.

## How to monitor a Device Guard policy

Use the information in the [Monitor compliance settings](/sccm/compliance/deploy-use/monitor-compliance-settings) topic to help you monitor that the deployed policy has been applied to all PCs correctly.

To monitor the processing of a Device Guard policy, use the following log file on client PCs:

**%WINDIR%\CCM\Logs\DeviceGuardHandler.log**

To verify the specific software being blocked or audited, see the following local client event logs:

1.	For blocking and auditing of executable files, use **Applications and Services Logs** > **Microsoft** > **Windows** > **Code Integrity** > **Operational**.
2.	For blocking and auditing of Windows Installer and script files, use **Applications and Services Logs** > **Microsoft** > **Windows** > **AppLocker** > **MSI and Script**.

## Security and privacy information for Device Guard

- In this pre-release version, do not deploy Device Guard policies with the enforcement mode **Audit Only** in a production environment. This mode is intended to help you test the capability in a lab setting only.
- Devices that have a policy deployed to them in **Audit Only** or **Enforcement Enabled** mode, that have not been restarted to enforce the policy are vulnerable to untrusted software being installed.
In this situation, the software might continue to be allowed to run even if the device restarts, or receives a policy in **Enforcement Enabled** mode.
- To ensure that the Device Guard policy is effective, prepare the device in a lab environment. Then, deploy the **Enforcement Enabled** policy, and finally, restart the device before you give the device to an end user.
- Do not deploy a policy with **Enforcement Enabled**, and then later deploy a policy with **Audit Only** to the same device. This configuration might result in untrusted software being allowed to run.
- When you use Configuration Manager to enable configurable code integrity on client PCs with Device Guard policies, the policy does not prevent users with local administrator rights from circumventing the Device Guard policy or otherwise executing untrusted software. 
- The only way to prevent users with local administrator rights from disabling configurable code integrity is to deploy a signed binary policy. This deployment is possible through Group Policy but not currently supported in Configuration Manager.
- Setting up Configuration Manager as a Managed Installer on client PCs uses AppLocker policy. AppLocker is only used to identify Managed Installers and all enforcement happens with configurable code integrity. 




