---
title: Integrate Windows Update for Business
titleSuffix: Configuration Manager
description: Use Windows Update for Business to keep Windows up-to-date for devices connected to the Windows Update service.
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.date: 10/20/2021
ms.topic: conceptual
ms.service: configuration-manager
ms.subservice: software-updates
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# Integrate with Windows Update for Business

*Applies to: Configuration Manager (current branch)*

Windows Update for Business allows you to keep Windows 10 or later devices in your organization always up-to-date with the latest security defenses and Windows features when these devices connect directly to the Windows Update (WU) service. Configuration Manager can differentiate between Windows computers that use Windows Update for Business and WSUS for getting software updates.  

> [!WARNING]
> If you are using co-management for your devices and you have moved the [Windows Update policies](../../comanage/workloads.md#windows-update-policies) to Intune, then your devices will get their [Windows Update client policies from Intune](/mem/intune/protect/windows-update-for-business-configure).
> - If the Configuration Manager client is still installed on the co-managed device then settings for Cumulative Updates and Feature Updates are managed by Intune. However, third-party patching, if enabled in [**Client Settings**](../../core/clients/deploy/about-client-settings.md#enable-third-party-software-updates), is still managed by Configuration Manager.  

 Some Configuration Manager features are no longer available when Configuration Manager clients are configured to receive updates from WU, which includes Windows Update for Business or Windows Insiders:  

- Windows Update compliance reporting:  
  - Configuration Manager will be unaware of the updates that are published to WU. The Configuration Manager clients configured to received updates from WU will display **unknown** for these updates in the Configuration Manager console.  

  - Troubleshooting overall compliance status is difficult because **unknown** status was only for the clients that hadn't reported scan status back from WSUS. Now it also includes Configuration Manager clients that receive updates from WU.  

  - Definition Updates compliance is part of overall update compliance reporting and won't work as expected either.

- Overall Endpoint Protection reporting for Defender based on update compliance status won't return accurate results because of the missing scan data.  

- Configuration Manager won't be able to deploy or report compliance on Microsoft app updates for clients configured to use Windows Update for Business to receive updates. This includes updates for Microsoft 365 Apps, Internet Explorer, Edge, and Visual Studio.

- Configuration Manager can still deploy 3rd party updates that are published to WSUS and managed through Configuration Manager to clients that are connected to Windows Update for Business to receive updates. If you don't want any 3rd party updates to be installed on clients connecting to Windows Update for Business, then disable the client setting named [Enable software updates on clients](../../core/clients/deploy/about-client-settings.md#software-updates).

- Configuration Manager full client deployment that uses the software updates infrastructure won't work for clients that are connected to Windows Update for Business to receive updates.  

## Identify clients that use Windows Update for Business for Windows updates

Use the following procedure to identify clients that use Windows Update for Business to get Windows updates and upgrades. Then configure these clients to stop using WSUS to get updates, and deploy a client agent setting to disable the software updates workflow for these clients.  

### Prerequisites for Windows Update for Business

- Clients that run Windows 10 Desktop Pro or Windows 10 Enterprise Edition version 1511 or later

- [Windows Update for Business](/windows/deployment/update/waas-manage-updates-wufb) is deployed and clients use Windows Update for Business to get Windows updates and upgrades.  

### To identify clients that use Windows Update for Business  

1. Ensure the Windows Update Agent isn't scanning against WSUS, if it was previously enabled. The following registry key can be used to indicate whether the computer is scanning against WSUS or Windows Update. If the registry key doesn't exist, it's not scanning against WSUS.
    - **HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU\UseWUServer**
1. There's a new attribute, **UseWUServer**, under the **Windows Update** node in Configuration Manager Resource Explorer.
1. Create a collection based on the **UseWUServer** attribute for all the computers that are connected via Windows Update for Business for updates and upgrades. You can create a collection based on a query similar to the one below:  

    ```wql
    Select sr.* from SMS_R_System as sr join SMS_G_System_WINDOWSUPDATE as su on sr.ResourceID=su.ResourceID where su.UseWUServer is null
    ```

1. Create a client agent setting to disable the software update workflow. Deploy the setting to the collection of computers that are connected directly to Windows Update for Business.
1. The computers that are managed via Windows Update for Business will display **Unknown** in the compliance status and won't be counted as part of the overall compliance percentage.  

## Configure Windows Update for Business deferral policies
<!-- 1290890 -->
You can configure deferral policies for Windows 10 or later Feature Updates or Quality Updates for Windows devices managed directly by Windows Update for Business. You can manage the deferral policies in the new **Windows Update for Business Policies** node under **Software Library** > **Windows Servicing**.

> [!NOTE]
> You can set deferral policies for Windows Insider. <!--507201-->  
For more information about the Windows Insider program, see [Getting started with Windows Insider program for Business](/windows-insider/business/server-get-started).

### Prerequisites for deferral policies

- Windows 10 version 1703 or later
- Windows 10 or later devices managed by Windows Update for Business must have Internet connectivity

#### To create a Windows Update for Business deferral policy

1. In **Software Library** > **Windows Servicing** > **Windows Update for Business Policies**
1. On the **Home** tab, in the **Create** group, select **Create Windows Update for Business Policy** to open the Create Windows Update for Business Policy Wizard.
1. On the **General** page, provide a name and description for the policy.
1. On the **Deferral Policies** page, configure whether to defer or pause Feature Updates. Feature Updates are generally new features for Windows. After you configure the **Branch readiness level** setting, you can then define if, and for how long, you would like to defer receiving Feature Updates following their availability from Microsoft.
    - **Branch readiness level**: Set the branch for which the device will receive Windows updates. Choose either Semi-Annual Channel (Targeted), Semi-Annual Channel, or a Windows Insider build.

        > [!NOTE]
        > Deploy policies for **Semi-Annual Channel** to Windows 10, *version 1903 or later*. Deploy policies for **Semi-Annual Channel (Targeted)** to Windows 10, *version 1809 or earlier*.
        >
        > If you deploy a policy for **Semi-Annual Channel (Targeted)** to Windows 10, version 1903 or later, the deployment fails with the error **0x8004100c**.<!-- 5593139 -->

    - **Deferral period (days)**:  Specify the number of days for which Feature Updates will be deferred. You can defer receiving these Feature Updates for up to 365 days from their release.
    - **Pause Features Updates starting**: Select whether to pause devices from receiving Feature Updates for up to 35 days from the time you pause the updates. After the maximum days have passed, pause functionality will automatically expire and the device will scan Windows Updates for applicable updates. Following this scan, you can pause the updates again. You can unpause Feature Updates by clearing the checkbox.
1. Choose whether to defer or pause Quality Updates. Quality Updates are generally fixes and improvements to existing Windows functionality and are typically published the second Tuesday of every month, though can be released at any time by Microsoft. You can define if, and for how long, you would like to defer receiving Quality Updates following their availability.
    - **Deferral period (days)**: Specify the number of days for which Quality Updates will be deferred. You can defer receiving these Quality Updates for up to 30 days from their release.
    - **Pause Quality Updates starting**: Select whether to pause devices from receiving Quality Updates for up to 35 days from the time you pause the updates. After the maximum days have passed, pause functionality will automatically expire and the device will scan Windows Updates for applicable updates. Following this scan, you can pause the updates again. You can unpause Quality Updates by clearing the checkbox.
1. Select **Install updates from other Microsoft Products** to enable the group policy setting that make deferral settings applicable to Microsoft Update, as well as Windows Updates.
1. Select **Include drivers with Windows Update** to automatically update drivers from Windows Updates. If you clear this setting, driver updates aren't downloaded from Windows Updates.
1. Complete the wizard to create the new deferral policy.

#### To deploy a Windows Update for Business deferral policy

1. In **Software Library** > **Windows Servicing** > **Windows Update for Business Policies**
1. On the **Home** tab, in the **Deployment** group, select **Deploy Windows Update for Business Policy**.
1. Configure the following settings:
    - **Configuration policy to deploy**: Select the Windows Update for Business policy that you would like to deploy.
    - **Collection**: Click **Browse** to select the collection where you want to deploy the policy.
    - **Allow remediation outside the maintenance window**: If a maintenance window has been configured for the collection to which you're deploying the policy, enable this option to let policy settings remediate the value outside of the maintenance window. For more information about maintenance windows, see [How to use maintenance windows](../../core/clients/manage/collections/use-maintenance-windows.md).
    - **Schedule**: Specify the compliance evaluation schedule by which the deployed policy is evaluated on client computers. The schedule can be either a simple or a custom schedule.
1. Complete the wizard to deploy the policy.
