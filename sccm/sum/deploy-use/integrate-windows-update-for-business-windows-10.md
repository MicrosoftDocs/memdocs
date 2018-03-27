---

title: Integration with Windows Update for Business in Windows 10
titleSuffix: "Configuration Manager"
description: "Use Windows Update for Business to keep Windows 10-based devices in your organization up to date for devices connected to the Windows Update service."
keywords:
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 03/22/2018
ms.topic: article
ms.prod: configuration-manager
ms.service:
ms.technology:
 - configmgr-sum
ms.assetid: 183315fe-27bd-456f-b2c5-e8d25e05229b

---
# Integration with Windows Update for Business in Windows 10

*Applies to: System Center Configuration Manager (Current Branch)*

Windows Update for Business (WUfB) allows you to keep Windows 10-based devices in your organization always up-to-date with the latest security defenses and Windows features when these devices connect directly to the Windows Update (WU) service. Configuration Manager can differentiate between Windows 10 computers that use WUfB and WSUS for getting software updates.  

 Some Configuration Manager features are no longer available when Configuration Manager clients are configured to receive updates from WU, which includes WUfB or Windows Insiders:  

-   Windows Update compliance reporting:  

    -   Configuration Manager will be unaware of the updates that are published to WU. The Configuration Manager clients configured to received updates from WU will display **unknown** for these updates in the Configuration Manager console.  

    -   Troubleshooting overall compliance status is difficult  because **unknown** status was only for the clients that hadn't reported scan status back from WSUS. Now it also includes Configuration Manager clients that receive updates from WU.  

    -   Conditional access (for corporate resources) based on update compliance status will not work as expected for clients that receive updates from WU because they would never meet compliance from Configuration Manager.  

    -   Definition Updates compliance is part of overall update compliance reporting and will not work as expected either.  Definition update compliance is also part of conditional access evaluation  

-   Overall Endpoint Protection reporting for Defender based on update compliance status will not return accurate results because of the missing scan data.  

-   Configuration Manager will not be able to deploy Microsoft updates, such as Office, IE, and Visual Studio to clients that are connected to WUfB to receive updates.  

-   Configuration Manager will not be able to deploy 3rd party updates that are published to WSUS and managed through Configuration Manager to clients that are connected to WUfB to receive updates.  

-   Configuration Manager full client deployment that uses the software updates infrastructure will not work for clients that are connected to WUfB to receive updates.  

## Identify clients that use WUfB for Windows 10 updates  
 Use the following procedure to identify clients that use WUfB to get Windows 10 updates and upgrades. Then configure these clients to stop using WSUS to get updates, and deploy a client agent setting to disable   the software updates workflow for these clients.  

 **Prerequisites**  

-   Clients that run Windows 10 Desktop Pro or Windows 10 Enterprise Edition version 1511 or later  

-   [Windows Update for Business](https://technet.microsoft.com/library/mt622730\(v=vs.85\).aspx) is deployed and clients use WUfB to get Windows 10 updates and upgrades.  

#### To identify clients that use WUfB  

1.  Disable the Windows Update Agent so it doesn't scan against WSUS, if it was previously enabled. The following registry key can be set to indicate whether the computer is scanning against WSUS or Windows Update.  When the value is 2, it's not scanning against WSUS.  
    - **HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU\UseWUServer**

2.  There is a new attribute, **UseWUServer**, under the **Windows Update** node in Configuration Manager Resource Explorer.  

3.  Create a collection based on the **UseWUServer** attribute for all the computers that are connected via WUfB for updates and upgrades.  

4.  Create a client agent setting to disable the software update workflow. Deploy the setting to the collection of computers that are connected directly to WUfB.  

5.  The computers that are managed via WUfB will display **Unknown** in the compliance status and won't be counted as part of the overall compliance percentage.  

## Configure Windows Update for Business deferral policies
<!-- 1290890 -->
Beginning in Configuration Manager version 1706, you can configure deferral policies for Windows 10 Feature Updates or Quality Updates for Windows 10 devices managed directly by Windows Update for Business. You can manage the deferral policies in the new **Windows Update for Business Policies** node under **Software Library** > **Windows 10 Servicing**.

>[!NOTE] 
>Beginning in Configuration Manager version 1802, you can set deferral policies for Windows Insider. <!--507201-->For more information about the Windows Insider program, see [Getting started with Windows Insider program for Business](https://docs.microsoft.com/windows/deployment/update/waas-windows-insider-for-business).

### Prerequisites
Windows 10 devices managed by Windows Update for Business must have Internet connectivity.

#### To create a Windows Update for Business deferral policy
1. In **Software Library** > **Windows 10 Servicing** > **Windows Update for Business Policies**
2. On the **Home** tab, in the **Create** group, select **Create Windows Update for Business Policy** to open the Create Windows Update for Business Policy Wizard.
3. On the **General** page, provide a name and description for the policy.
4. On the **Deferral Policies** page, configure whether to defer or pause Feature Updates. Feature Updates are generally new features for Windows. After you configure the **Branch readiness level** setting, you can then define if, and for how long, you would like to defer receiving Feature Updates following their availability from Microsoft.
    - **Branch readiness level**: Set the branch for which the device will receive Windows updates (Current Branch or Current Branch for Business).
    - **Deferral period (days)**:  Specify the number of days for which Feature Updates will be deferred. You can defer receiving these Feature Updates for a period of 180 days from their release.
    - **Pause Features Updates starting**: Select whether to pause devices from receiving Feature Updates for a period of up to 60 days from the time you pause the updates. After the maximum days have passed, pause functionality will automatically expire and the device will scan Windows Updates for applicable updates. Following this scan, you can pause the updates again. You can unpause Feature Updates by clearing the checkbox.   
5. Choose whether to defer or pause Quality Updates. Quality Updates are generally fixes and improvements to existing Windows functionality and are typically published the first Tuesday of every month, though can be released at any time by Microsoft. You can define if, and for how long, you would like to defer receiving Quality Updates following their availability.
    - **Deferral period (days)**: Specify the number of days for which Feature Updates will be deferred. You can defer receiving these Feature Updates for a period of 180 days from their release.
    - **Pause Quality Updates starting**: Select whether to pause devices from receiving Quality Updates for a period of up to 35 days from the time you pause the updates. After the maximum days have passed, pause functionality will automatically expire and the device will scan Windows Updates for applicable updates. Following this scan, you can pause the updates again. You can unpause Quality Updates by clearing the checkbox.
6. Select **Install updates from other Microsoft Products** to enable the group policy setting that make deferral settings applicable to Microsoft Update, as well as Windows Updates.
7. Select **Include drivers with Windows Update** to automatically update drivers from Windows Updates. If you clear this setting, driver updates are not downloaded from Windows Updates.
8. Complete the wizard to create the new deferral policy.

#### To deploy a Windows Update for Business deferral policy
1. In **Software Library** > **Windows 10 Servicing** > **Windows Update for Business Policies**
2. On the **Home** tab, in the **Deployment** group, select **Deploy Windows Update for Business Policy**.
3. Configure the following settings:
    - **Configuration policy to deploy**: Select the Windows Update for Business policy that you would like to deploy.
    - **Collection**: Click **Browse** to select the collection where you want to deploy the policy.
    - **Remediate noncompliant rules when supported**: Select to automatically remediate any rules that are noncompliant for Windows Management Instrumentation (WMI), the registry, scripts, and all settings for mobile devices that are enrolled by Configuration Manager.
    - **Allow remediation outside the maintenance window**: If a maintenance window has been configured for the collection to which you are deploying the policy, enable this option to let compliance settings remediate the value outside of the maintenance window. For more information about maintenance windows, see [How to use maintenance windows](/sccm/core/clients/manage/collections/use-maintenance-windows).
    - **Generate an alert**: Configures an alert that is generated if the configuration baseline compliance is less than a specified percentage by a specified date and time. You can also specify whether you want an alert to be sent to System Center Operations Manager.
    - **Random delay (hours)**: Specifies a delay window to avoid excessive processing on the Network Device Enrollment Service. The default value is 64 hours.
    - **Schedule**: Specify the compliance evaluation schedule by which the deployed profile is evaluated on client computers. The schedule can be either a simple or a custom schedule. The profile is evaluated by client computers when the user logs on.
4.  Complete the wizard to deploy the profile.
