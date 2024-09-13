---
title: Manage Windows Defender Application Control
titleSuffix: Configuration Manager
description: Learn how to use Configuration Manager to manage Windows Defender Application Control.
ms.date: 04/11/2022
ms.service: configuration-manager
ms.subservice: protect
ms.topic: how-to
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# Windows Defender Application Control management with Configuration Manager

*Applies to: Configuration Manager (current branch)*

Windows Defender Application Control is designed to protect devices against malware and other untrusted software. It prevents malicious code from running by ensuring that only approved code, that you know, can be run.

Application Control is a software-based security layer that enforces an explicit list of software that is allowed to run on a PC. On its own, Application Control doesn't have any hardware or firmware prerequisites. Application Control policies deployed with Configuration Manager enable a policy on devices in targeted collections that meet the minimum Windows version and SKU requirements outlined in this article. Optionally, hypervisor-based protection of Application Control policies deployed through Configuration Manager can be enabled through group policy on capable hardware.

For more information, see the [Windows Defender Application Control deployment guide](/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control-deployment-guide).

> [!NOTE]
> This feature was previously known as _configurable code integrity_ and _Device Guard_.

## Using Application Control with Configuration Manager

You can use Configuration Manager to deploy an Application Control policy. This policy lets you configure the mode in which Application Control runs on devices in a collection.

You can configure one of the following modes:

1. **Enforcement enabled** - Only trusted executables are allowed to run.
2. **Audit only** - Allow all executables to run, but log untrusted executables that run in the local client event log.

## What can run when you deploy an Application Control policy?

Application Control lets you strongly control what can run on devices you manage. This feature can be useful for devices in high-security departments, where it's vital that unwanted software can't run.

When you deploy a policy, typically, the following executables can run:

- Windows OS components
- Hardware Dev Center drivers with Windows Hardware Quality Labs signatures
- Windows Store apps
- The Configuration Manager client
- All software deployed through Configuration Manager that devices install after they process the Application Control policy
- Updates to built-in Windows components from:
    - Windows Update
    - Windows Update for Business
    - Windows Server Update Services
    - Configuration Manager
    - Optionally, software with a good reputation as determined by the Microsoft Intelligent Security Graph (ISG). The ISG includes Windows Defender SmartScreen and other Microsoft services. The device must be running Windows Defender SmartScreen and Windows 10 version 1709 or later for this software to be trusted.

> [!IMPORTANT]
> These items don't include any software that isn't built-into Windows that automatically updates from the internet or third-party software updates. This limitation applies whether they're installed by any of the listed update mechanisms or from the internet. Application Control only allows software changes that are deployed through the Configuration Manager client.

## <a name="bkmk_os"></a> Supported operating systems

To use Application Control with Configuration Manager, devices must be running supported versions of:

- Windows 11 or later, Enterprise edition
- Windows 10 or later, Enterprise edition
- Windows Server 2019 or later <!--7752243, 8581848-->

> [!TIP]
> Existing Application Control policies created with Configuration Manager version 2006 or earlier won't work with Windows Server. To support Windows Server, create new Application Control policies.

## Before you start

- Once a policy is successfully processed on a device, Configuration Manager is configured as a _managed installer_ on that client. After the policy processes, software deployed by Configuration Manager is automatically trusted. Before the device processes the Application Control policy, software installed by Configuration Manager isn't automatically trusted.

  > [!NOTE]
  > For example, you can't use the **Install Application** step in a task sequence to install applications during an OS deployment. For more information, see [Task sequence steps - Install Application](../../osd/understand/task-sequence-steps.md#BKMK_InstallApplication).<!-- 13847501 -->

- The default compliance evaluation schedule for Application Control policies is every day. This schedule is configurable during policy deployment. If you notice issues in policy processing, configure the compliance evaluation schedule to be more frequent. For example, every hour. This schedule dictates how often clients reattempt to process an Application Control policy if a failure occurs.

- Regardless of the enforcement mode you select, when you deploy an Application Control policy, devices can't run HTML applications with the `.hta` file extension.

## Create an Application Control policy

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace.

1. Expand **Endpoint Protection**, and then select the **Windows Defender Application Control** node.

1. On the **Home** tab of the ribbon, in the **Create** group, select **Create Application Control policy**.

1. On the **General** page of the **Create Application Control policy Wizard**, specify the following settings:

    - **Name**: Enter a unique name for this Application Control policy.

    - **Description**: Optionally, enter a description for the policy that helps you identify it in the Configuration Manager console.

    - **Enforce a restart of devices so that this policy can be enforced for all processes**: After the device processes the policy, a restart is scheduled on the client according to the **Client Settings** for **Computer Restart**. Applications currently running on the device won't apply the new Application Control policy until after a restart. However, applications launched after the policy applies will honor the new policy.

    - **Enforcement Mode**: Choose one of the following enforcement methods:

        - **Enforcement Enabled**: Only trusted applications are allowed to run.

        - **Audit Only**: Allow all applications to run, but log untrusted programs that run. The audit messages are in the local client event log.

1. On the **Inclusions** tab of the **Create Application Control policy Wizard**, choose if you want to **Authorize software that is trusted by the Intelligent Security Graph**.

1. If you want to add trust for specific files or folders on devices, select **Add**. In the **Add Trusted File or Folder** dialog box, you can specify a local file or a folder path to trust. You can also specify a file or folder path on a remote device on which you have permission to connect. When you add trust for specific files or folders in an Application Control policy, you can:

    - Overcome issues with managed installer behaviors.

    - Trust line-of-business apps that you can't deploy with Configuration Manager.

    - Trust apps that are included in an OS deployment image.

1. Complete the wizard.

## Deploy an Application Control policy

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace.

1. Expand **Endpoint Protection**, and then select the **Windows Defender Application Control** node.

1. From the list of policies, select the one you want to deploy. On the **Home** tab of the ribbon, in the **Deployment** group, select **Deploy Application Control Policy**.

1. In the **Deploy Application Control policy** dialog box, select the collection to which you want to deploy the policy. Then configure a schedule for when clients evaluate the policy. Finally, select whether the client can evaluate the policy outside of any configured maintenance windows.

1. When you're finished, select **OK** to deploy the policy.

## Monitor an Application Control policy

In general, use the information in the [Monitor compliance settings](../../compliance/deploy-use/monitor-compliance-settings.md) article. This information can help you monitor that the deployed policy has been correctly applied to all devices.

To monitor the processing of an Application Control policy, use the following log file on devices:

`%WINDIR%\CCM\Logs\DeviceGuardHandler.log`

To verify the specific software being blocked or audited, see the following local client event logs:

- For blocking and auditing of executable files, use **Applications and Services Logs** > **Microsoft** > **Windows** > **Code Integrity** > **Operational**.

- For blocking and auditing of Windows Installer and script files, use **Applications and Services Logs** > **Microsoft** > **Windows** > **AppLocker** > **MSI and Script**.

## Security and privacy information

- Devices that have a policy deployed to them in **Audit Only** or **Enforcement Enabled** mode, but haven't been restarted to enforce the policy, are vulnerable to untrusted software being installed. In this situation, the software might continue to run even if the device restarts, or receives a policy in **Enforcement Enabled** mode.

- To help the effectiveness of the Application Control policy, first prepare the device in a lab environment. Deploy an **Enforcement Enabled** policy, then restart the device. Once you verify the apps work, then give the device to the user.

- Don't deploy a policy with **Enforcement Enabled** and then later deploy a policy with **Audit Only** to the same device. This configuration might result in untrusted software being allowed to run.

- When you use Configuration Manager to enable Application Control on devices, the policy doesn't prevent users with local administrator rights from circumventing the Application Control policies or otherwise running untrusted software.

- The only way to prevent users with local administrator rights from disabling Application Control is to deploy a signed binary policy. This deployment is possible through group policy, but not currently supported in Configuration Manager.

- Setting up Configuration Manager as a managed installer on devices uses a Windows AppLocker policy. AppLocker is only used to identify managed installers. All enforcement happens with Application Control.

## Next steps

[Manage antimalware policies and firewall settings](endpoint-antimalware-firewall.md)
