---
title: "How to manage Windows Device Guard | Microsoft Docs"
description: "Learn how to use System Center Configuration Manager to manage Windows Device Guard."
ms.custom: na
ms.date: 04/13/2017
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
Windows Device Guard is a group of Windows 10 features that are designed to protect PCs against malware and other untrusted software. It prevents malicious code from running by ensuring that only approved code, that you know, can be run.

To learn more about Device Guard, read [Device Guard deployment guide](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-deployment-guide).

You can use Configuration Manager to deploy a Device Guard policy that lets you configure the mode in which Device Guard will run on PCs in a collection. 

You can configure one of the following modes:

1.	**Enforcement enabled** - Only trusted executables are allowed to run.
2.	**Audit only** - Allow all executables to run, but log untrusted executables that run in the local client event log.

>[!TIP]
>In this version of Configuration Manager, Device Guard is a pre-release feature. To enable it, see [Pre-release features in System Center Configuration Manager](/sccm/core/servers/manage/pre-release-features).

### What can run when you deploy a Device Guard policy?

Windows Device Guard lets you strongly control what can run on PCs you manage. This can be particularly useful for PCs in high-security departments, where it's vital that unwanted software is not allowed to be run.

When you deploy a policy, typically, the following executables will be allowed to run:

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
>These do not include any software that is **not** built-into Windows that automatically updates from the internet or third party software updates whether they are installed via any of the update mechanisms mentioned above, or from the internet. Only software changes that are deployed though the Configuration Manager client will be allowed to run.

## Before you start

Before you configure or deploy Device Guard policies, read the following information:

- To use Device Guard, PCs you manage must be running the Windows 10 Creators Update, or later.
- Once a policy is successfully processed on a client PC, Configuration Manager is configured as a Managed Installer on that client, and software deployed through SCCM after the policy is processed is automatically trusted. Software installed by Configuration Managed before the Device Guard policy is processed is not automatically trusted.
- Device Guard management is a pre-release feature for Configuration Manager, and is subject to change.
- When you enable Device Guard with Configuration Manager, note that the policy does not prevent users with local administrator rights from circumventing the Device Guard policy or otherwise executing untrusted software.
- In this pre-release version, once a client PC receives a deployment of a Device Guard policy, it will randomize the processing time of this policy over a two-hour period. 
- Client PCs must have connectivity to their Domain Controller in order for a Device Guard policy to be processed successfully.
- The default compliance evaluation schedule for Device Guard policies, configurable during deployment, is every 1 day. If issues in policy processing are observed, it may be beneficial to configure the compliance evaluation schedule to be shorter, for example every 1 hour. This schedule dictates how often clients will re-attempt to process a Device Guard policy in the case of a failure.
- Regardless of the enforcement mode you select, when you deploy a Device Guard policy, client PCs will not be able to run HTML applications with the extension .hta.

## How to create a Device Guard policy
1.	In the Configuration Manager console, click **Assets and Compliance**.
2.	In the **Assets and Compliance** workspace, expand **Endpoint Protection**, and then click **Device Guard Policies**.
3.	On the **Home** tab, in the **Create** group, click **Create Device Guard Policy**.
4.	On the **General** page of the **Create Device Guard Policy Wizard**, specify the following:
	- **Name** - Enter a unique name for this Device Guard policy. 
	- **Description** - Optionally, enter a description for the policy that will help you identify it in the Configuration Manager console.
	- **Enforcement Mode** - Choose one of the following enforcement methods for Device Guard on the client PC.
		- **Enforcement Enabled** - Only allow trusted executables are allowed to run.
		- **Audit Only** - Allow all executables to run, but log untrusted executables that run in the local client event log.
5.	Click **Next**, then complete the wizard.

## How to deploy a Device Guard policy
1.	In the Configuration Manager console, click **Assets and Compliance**.
2.	In the **Assets and Compliance** workspace, expand **Endpoint Protection**, and then click **Device Guard Policies**.
3.	From the list of policies, select the one you want to deploy, and then, on the **Home** tab, in the **Deployment** group, click **Deploy**.
4.	In the **Deploy Device Guard Policy** dialog box, select the collection to which you want to deploy the policy, configure a schedule for when clients will evaluate the policy, and finally, select whether the client can evaluate the policy outside of any configured maintenance windows.
5.	When you are finished, click **OK** to deploy the policy. 

Once the policy is processed on a client PC, a restart will be scheduled on that client according the **Client Settings** for **Computer Restart**.
**Until you restart the client PC, the policy will not take effect.**

## How to monitor a Device Guard policy

Use the information in the [Monitor compliance settings](/sccm/compliance/deploy-use/monitor-compliance-settings) topic to help you monitor the deployed policy to ensure it has been applied to all PCs correctly.

Use the following log file on client PCs to monitor the processing of a Device Guard policy:

**%WINDIR%\CCM\Logs\DeviceGuardHandler.log**

To verify the specific software being blocked or audited, see the following local client event logs. In Event Viewer, the relevant logs are as follows:

1.	For blocking and auditing of executable files, use **Applications and Services Logs** > **Microsoft** > **Windows** > **Code Integrity** > **Operational**.
2.	For blocking and auditing of Windows Installer and script files, use **Applications and Services Logs** > **Microsoft** > **Windows** > **AppLocker** > **MSI and Script**.

## Security and privacy information for Device Guard

- In this pre-release version, do not deploy Device Guard policies with the enforcement mode **Audit Only** in a production environment. This mode is intended to help you test the capability in a lab setting only.
- Devices that have a policy deployed to them in **Audit Only** mode, or devices that have a policy deployed to them in **Enforcement Enabled** mode, that have not yet been restarted to enforce the policy are vulnerable to untrusted software being installed.
In this situation, the software might continue to be allowed to run even if the device restarts, or receives a policy in **Enforcement Enabled** mode.
- To ensure that the Device Guard policy is effective, prepare the device in a lab environment, deploy the **Enforcement Enabled** policy, then restart the device before you give the device to an end user.
- Do not deploy a policy with **Enforcement Enabled**, and then later deploy a policy with **Audit Only** to the same device. This might result in untrusted software being allowed to run.



