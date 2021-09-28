---
title: How to manage Windows Defender Application Control
titleSuffix: Configuration Manager
description: Learn how to use Configuration Manager to manage Windows Defender Application Control.
ms.date: 11/30/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
author: mestew
ms.author: mstewart
manager: dougeby
ms.localizationpriority: medium
---

# Windows Defender Application Control management with Configuration Manager

*Applies to: Configuration Manager (current branch)*

## Introduction
Windows Defender Application Control is designed to protect PCs against malware and other untrusted software. It prevents malicious code from running by ensuring that only approved code, that you know, can be run.

Windows Defender Application Control is a software-based security layer that enforces an explicit list of software that is allowed to run on a PC. On its own, Application Control does not have any hardware or firmware prerequisites. Application Control policies deployed with Configuration Manager enable a policy on PCs in targeted collections that meet the minimum Windows version and SKU requirements outlined in this article. Optionally, hypervisor-based protection of Application Control policies deployed through Configuration Manager can be enabled through Group Policy on capable hardware.

To learn more about Windows Defender Application Control, read the [Windows Defender Application Control deployment guide](/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control-deployment-guide).

   > [!NOTE]
   > - Beginning with Windows 10, version 1709, configurable code integrity policies are known as Windows Defender Application Control.
   > - Beginning in Configuration Manager version 1710, Device Guard policies have been renamed to Windows Defender Application Control policies.

## Using Windows Defender Application Control with Configuration Manager

You can use Configuration Manager to deploy a Windows Defender Application Control policy. This policy lets you configure the mode in which Windows Defender Application Control runs on PCs in a collection. 

You can configure one of the following modes:

1. **Enforcement enabled** - Only trusted executables are allowed to run.
2. **Audit only** - Allow all executables to run, but log untrusted executables that run in the local client event log.

> [!Tip]  
> This feature was first introduced in version 1702 as a [pre-release feature](../../core/servers/manage/pre-release-features.md). Beginning with version 1906, it's no longer a pre-release feature.  

## What can run when you deploy a Windows Defender Application Control policy?

Windows Defender Application Control lets you strongly control what can run on PCs you manage. This feature can be useful for PCs in high-security departments, where it's vital that unwanted software cannot run.

When you deploy a policy, typically, the following executables can run:

- Windows operating system components
- Hardware Dev Center drivers (that have Windows Hardware Quality Labs signatures)
- Windows Store apps
- The Configuration Manager client 
- All software deployed through Configuration Manager that PCs install after the Windows Defender Application Control policy is processed. 
- Updates to windows components from:
    - Windows Update
    - Windows Update for Business
    - Windows Server Update Services
    - Configuration Manager
    - Optionally, software with a good reputation as determined by the Microsoft Intelligent Security Graph (ISG). The ISG includes Windows Defender SmartScreen and other Microsoft services. The device must be running Windows Defender SmartScreen and Windows 10 version 1709 or later for this software to be trusted.

>[!IMPORTANT]
>These items do not include any software that is *not* built-into Windows that automatically updates from the internet or third-party software updates whether they are installed via any of the update mechanisms mentioned previously, or from the internet. Only software changes that are deployed though the Configuration Manager client can run.

## <a name="bkmk_os"></a> Supported operating systems

To use Windows Defender Application Control with Configuration Manager, devices you manage must be running:
- Windows 10 Enterprise version 1703, or later.
- Windows Server 2019, or later (Introduced in version 2010) <!--7752243, 8581848-->

> [!Tip]
> Create new policies to target Windows Server operating systems after installation of Configuration Manager 2010 and installing the updated client. Existing Windows Defender Application Control polices created prior to installing 2010 won't work with Windows Server operating systems.

## Before you start

Before you configure or deploy Windows Defender Application Control policies, read the following information:

- Once a policy is successfully processed on a client PC, Configuration Manager is configured as a Managed Installer on that client. Software deployed through it, after the policy processes, is automatically trusted. Software installed by Configuration Manager before the Windows Defender Application Control policy processes is not automatically trusted.
- The default compliance evaluation schedule for Application Control policies, configurable during deployment, is every one day. If issues in policy processing are observed, it may be beneficial to configure the compliance evaluation schedule to be shorter, for example every hour. This schedule dictates how often clients reattempt to process a Windows Defender Application Control policy if a failure occurs.
- Regardless of the enforcement mode you select, when you deploy a Windows Defender Application Control policy, client PCs cannot run HTML applications with the extension .hta.
- Create new policies to target Windows Server operating systems after installation of Configuration Manager 2010 and installing the updated client. Existing Windows Defender Application Control polices created prior to installing 2010 won't work with Windows Server operating systems.

## How to create a Windows Defender Application Control policy
1. In the Configuration Manager console, click **Assets and Compliance**.
2. In the **Assets and Compliance** workspace, expand **Endpoint Protection**, and then click **Windows Defender Application Control**.
3. On the **Home** tab, in the **Create** group, click **Create Application Control policy**.
4. On the **General** page of the **Create Application Control policy Wizard**, specify the following settings:
    - **Name** - Enter a unique name for this Windows Defender Application Control policy. 
    - **Description** - Optionally, enter a description for the policy that helps you identify it in the Configuration Manager console.
    - **Enforce a restart of devices so that this policy can be enforced for all processes** - After the policy is processed on a client PC, a restart is scheduled on the client according to the **Client Settings** for **Computer Restart**.
        - Devices running Windows 10 version 1703 or earlier will always be automatically restarted.
        - Starting with Windows 10 version 1709, applications currently running on the device will not have the new Application Control policy applied to them until after a restart. However, applications launched after the policy applies will honor the new Application Control policy. 
    - **Enforcement Mode** - Choose one of the following enforcement methods for Windows Defender Application Control on the client PC.
        - **Enforcement Enabled** - Only allow trusted executables are allowed to run.
        - **Audit Only** - Allow all executables to run, but log untrusted executables that run in the local client event log.
5. On the **Inclusions** tab of the **Create Application Control policy Wizard**, choose if you want to **Authorize software that is trusted by the Intelligent Security Graph**.
6. Click **Add** if you want to add trust for specific files or folders on PCs. In the **Add Trusted File or Folder** dialog box, you can specify a local file or a folder path to trust. You can also specify a file or folder path on a remote device on which you have permission to connect. When you add trust for specific files or folders in a Windows Defender Application Control policy, you can:
    - Overcome issues with managed installer behaviors
    - Trust line-of-business apps that cannot be deployed with Configuration Manager
    - Trust apps that are included in an operating system deployment image. 
8. Click **Next**, to complete the wizard.

>[!IMPORTANT]
>The inclusion of trusted files or folders is only supported on client PCs running version 1706 or later of the Configuration Manager client. If any inclusion rules are included in a Windows Defender Application Control policy and the policy is then deployed to a client PC running an earlier version on the Configuration Manager client, the policy will fail to be applied. Upgrading these older clients will resolve this issue. Policies that do not include any inclusion rules may still be applied on older versions of the Configuration Manager client.

## How to deploy a Windows Defender Application Control policy
1. In the Configuration Manager console, click **Assets and Compliance**.
2. In the **Assets and Compliance** workspace, expand **Endpoint Protection**, and then click **Windows Defender Application Control**.
3. From the list of policies, select the one you want to deploy, and then, on the **Home** tab, in the **Deployment** group, click **Deploy Application Control Policy**.
4. In the **Deploy Application Control policy** dialog box, select the collection to which you want to deploy the policy. Then, configure a schedule for when clients evaluate the policy. Finally, select whether the client can evaluate the policy outside of any configured maintenance windows.
5. When you are finished, click **OK** to deploy the policy. 

<!--Reworked article to put this inline while working on VSO 1355092
### Restarting the device after deploying the policy

After the policy is processed on a client PC, a restart is scheduled on that client according to the **Client Settings** for **Computer Restart**. A restart is not required to apply policies, but it is the default. If you want to turn off restarts, follow these steps:

1. Open the **Create Windows Defender Application Policy** wizard.
2. On the **General** page, clear the check box for **Enforce a restart of devices so that this policy can be enforced for all processes**.
3. Click **Next** until the wizard completes.-->


## How to monitor a Windows Defender Application Control policy

Use the information in the [Monitor compliance settings](../../compliance/deploy-use/monitor-compliance-settings.md) article to help you monitor that the deployed policy has been applied to all PCs correctly.

To monitor the processing of a Windows Defender Application Control policy, use the following log file on client PCs:

**%WINDIR%\CCM\Logs\DeviceGuardHandler.log**

To verify the specific software being blocked or audited, see the following local client event logs:

1. For blocking and auditing of executable files, use **Applications and Services Logs** > **Microsoft** > **Windows** > **Code Integrity** > **Operational**.
2. For blocking and auditing of Windows Installer and script files, use **Applications and Services Logs** > **Microsoft** > **Windows** > **AppLocker** > **MSI and Script**.

<!--Reworked article to put this inline while working on VSO 1355092
## Automatically let software run if it is trusted by Intelligent Security Graph

You can let locked-down devices run software with a good reputation as determined by the Microsoft Intelligent Security Graph (ISG). The ISG includes [Windows Defender SmartScreen](/windows/security/threat-protection/microsoft-defender-smartscreen/microsoft-defender-smartscreen-overview) and other Microsoft services. The devices must be running Windows Defender SmartScreen for this software to be trusted.

1. Open the **Create Windows Defender Application Policy** wizard.
2. On the **Inclusions** page, check the box for **Authorize software that is trusted by the Intelligent Security Graph**.
3. Click **Next** until the wizard completes.
-->


## Security and privacy information for Windows Defender Application Control

- Devices that have a policy deployed to them in **Audit Only** or **Enforcement Enabled** mode that have not been restarted to enforce the policy, are vulnerable to untrusted software being installed.
In this situation, the software might continue to be allowed to run even if the device restarts, or receives a policy in **Enforcement Enabled** mode.
- To ensure that the Windows Defender Application Control policy is effective, prepare the device in a lab environment. Then, deploy the **Enforcement Enabled** policy, and finally, restart the device before you give the device to an end user.
- Do not deploy a policy with **Enforcement Enabled**, and then later deploy a policy with **Audit Only** to the same device. This configuration might result in untrusted software being allowed to run.
- When you use Configuration Manager to enable Windows Defender Application Control on client PCs, the policy does not prevent users with local administrator rights from circumventing the Application Control policies or otherwise executing untrusted software.
- The only way to prevent users with local administrator rights from disabling Application Control is to deploy a signed binary policy. This deployment is possible through Group Policy but not currently supported in Configuration Manager.
- Setting up Configuration Manager as a Managed Installer on client PCs uses AppLocker policy. AppLocker is only used to identify Managed Installers and all enforcement happens with Windows Defender Application Control. 

## Next steps

 [Manage antimalware policies and firewall settings](endpoint-antimalware-firewall.md)