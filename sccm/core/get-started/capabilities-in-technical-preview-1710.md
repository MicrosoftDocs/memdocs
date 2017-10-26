---
title: "Technical Preview 1710 | Microsoft Docs"
titleSuffix: "Configuration Manager"
description: "Learn about features available in the Technical Preview version 1710 for System Center Configuration Manager."
ms.custom: na
ms.date: 10/27/2017
ms.prod: configuration-manager
ms.technology:
  - configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f4706a58-1f11-4eab-b1eb-3d1a0da02d0f
author: Brenduns
ms.author: brenduns
manager: angrobe
---
# Capabilities in Technical Preview 1710 for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Technical Preview)*

This article introduces the features that are available in the Technical Preview for System Center Configuration Manager, version 1710. You can install this version to update and add new capabilities to your Configuration Manager technical preview site. Before installing this version of the technical preview, review [Technical Preview for System Center Configuration Manager](../../core/get-started/technical-preview.md) to become familiar with general requirements and limitations for using a technical preview, how to update between versions, and how to provide feedback about the features in a technical preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Known Issues in this Technical Preview:**
-   **Support for Windows 10, version 1709 (also known as the Fall Creators Update)**.  Beginning with this Windows release, Windows media includes multiple editions. When configuring a task sequence to use an operating system upgrade package or operating system image, be sure to select an [edition that is supported for use by Configuration Manager](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-as-a-client).
-   **Update to a new preview version fails when you have a site server in passive mode**. When you run a preview version that has a [primary site server in passive mode](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability), you must uninstall the passive mode site server before you can successfully update your preview site to this new preview version. You can reinstall the passive mode site server after your site completes the update.

  To uninstall the passive mode site server:
  1. In the console go to **Administration** > **Overview** > **Site Configuration** > **Servers and Site System Roles**, and then select the passive mode site server.
  2. In the **Site System Roles** pane, right click on the **Site server** role, and then choose **Remove Role**.
  3. Right-click on the passive mode site server, and then choose **Delete**.
  4. After the site server uninstalls, on the active primary site server restart the service **CONFIGURATION_MANAGER_UPDATE**.



**The following are new features you can try out with this version.**  

<!--  Section Template
##  FEATURE
### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->



## Limit Windows 10 Enhanced telemetry to only send data relevant to Windows Analytics Device Health
<!-- 1356148 -->

You must limit the Windows 10 telemetry data collection level to **Enhanced** to gain actionable insight about devices in your environment. With Windows 10 version 1709 or later, you can restrict the data reported by the device to data relevant to Windows Analytics. Configure the Windows telemetry on your Windows 10 clients to collect this data.

### Try it out!
To configure Windows 10 telemetry collection on clients, see [How to configure client settings](/sccm/core/clients/deploy/configure-client-settings). Open the **Cloud Services** window, and set Windows 10 telemetry to **Enhanced**.


## Software Center no longer distorts icons larger than 250x250  
<!-- 1356194 -->

With this release, Software Center will no longer distort icons that are larger than 250x250. Software Center made such icons look blurry. You can now set an icon with a pixel dimensions of up to 512x512, and it displays without distortion.

### Try it out!
Add an icon for your app in Software Center. To try it out see [Create applications](/sccm/apps/deploy-use/create-applications).



## Check compliance from Software Center for co-managed devices
<!-- 1356374 -->
In this release, users can use Software Center to check the compliance of their co-managed Windows 10 devices even when conditional access is managed by Intune. For details, see [Co-management for Windows 10 devices](./capabilities-in-technical-preview-1709.md#co-management-for-windows-10-devices).


## Support for Exploit Guard
This release adds support for Windows Defender Exploit Guard. You can configure and deploy policies that manage all four components of Exploit Guard. These components include:
-   Attack Surface Reduction
-   Controlled folder access
-   Exploit protection
-   Network protection

Compliance data for Exploit Guard policy deployment is available from within the Configuration Manager console.

For more information about Exploit Guard and specific components and rules, see [Windows Defender Exploit Guard](https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/windows-defender-exploit-guard) in the Windows documentation library.

### Prerequisites
Managed devices must run Windows 10 1709 Fall Creators Update or later and satisfy the following requirements depending on the components and rules configured:

|Exploit Guard component |Additional prerequisites|
|------------------------|------------------------|
| Attack Surface Reduction  | Devices must have [Windows Defender AV real-time protection]( https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/controlled-folders-exploit-guard) enabled.  |
| Controlled folder access  | Devices must have [Windows Defender AV real-time protection]( https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/controlled-folders-exploit-guard) enabled.   |
| Exploit protection  | None  |
| Network protection  |  Devices must have [Windows Defender AV real-time protection]( https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/controlled-folders-exploit-guard) enabled.  |

### Create an Exploit Guard policy  <!--1355468 -->
1.	In the Configuration Manager console, go to **Assets and compliance** > **Endpoint Protection**, and then click **Windows Defender Exploit Guard**.
2.	On the **Home** tab, in the **Create** group, click **Create Exploit Policy**.
3.	On the **General** page of the **Create Configuration Item Wizard**, specify a name, and optional description for the configuration item.
4.	Next, select the Exploit Guard components you want to manage with this policy. For each component you select, you can then configure additional details.
  - 	**Attack Surface Reduction:** Configure the Office threat, scripting threats, and email threats you want to block or audit. You can also exclude specific files or folders from this rule.
  - 	**Controlled folder access:** Configure blocking or auditing, and then add Apps that can bypass this policy.  You can also specify additional folders that are not protected by default.
  - 	**Exploit protection:**  Specify an XML file that contains settings for mitigating exploits of system processes and apps. You can export these settings from the Windows Defender Security Center app on a Windows 10 device.
  - 	**Network protection:** Set network protection to block or audit access to suspicious domains.
5.	Complete the wizard to create the policy, which you can later deploy to devices.

### Deploy an Exploit Guard policy     
After you create Exploit Guard policies, use the Deploy Exploit Guard Policy wizard to deploy them. To do so, open the Configuration Manager console to **Assets and compliance** > **Endpoint Protection**, and then click **Deploy Exploit Guard Policy**.



## Improved descriptions for pending computer restarts   <!--1356283 -->
In [technical preview 1708](/sccm/core/get-started/capabilities-in-technical-preview-1708#restart-computers-from-the-configuration-manager-console), we added the capability to identify devices that are pending a restart from within the Configuration Manager console.

Beginning with this technical preview, the console displays additional details that provide information about the process or action that is requesting the reboot.

## Device Guard policy changes <!-- 1355092 -->
With the 1710 Technical Preview build, the following three changes have been made in relation to Device Guard policies:

### Device Guard policies renamed to Windows Defender Application Control policies
Device Guard policies have been renamed to Windows Defender Application Control policies. So, for example, the **Create Device Guard policy wizard** is now named **Create Windows Defender Application Control policy wizard**.

### Restart is not required to apply policies
Starting with the Fall Creators Update for Windows version 1709, devices using the new version of Windows don’t require a restart to apply the Windows Defender Application Control policies.

Restarting is the default.

#### Try it out!  

If you want to turn off restarts, follow these steps:

1.	Open the **Create Windows Defender Application Control Policy** wizard.
2.	On the **General** page, clear the check box for **Enforce a restart of devices so that this policy can be enforced for all processes**.
3.	Click **Next** until the wizard completes.

For older versions of Windows, an automated restart is still enforced.

### Automatically run software trusted by the Intelligent Security Graph

Administrators now have the option to allow locked-down devices to run trusted software with a good reputation as determined by the Microsoft Intelligent Security Graph (ISG). The ISG is comprised of Windows Defender SmartScreen and other Microsoft services.

The devices must be running Windows Defender SmartScreen for the software to be trusted.

#### Try it out!  

To let a device running Windows Defender SmartScreen run trusted software, follow these steps:

1.	Open the **Create Windows Defender Application Control Policy wizard**.
2.	On the **Inclusions** page, check the box for **Authorize software that is trusted by the Intelligent Security Graph**.
3.	In the **Trusted files or folder** box, add the files and folders that you want to be trusted.
4.	Click **Next** until the wizard completes.

## Configure and deploy Windows Defender Application Guard policies <!-- 1351960 -->

[Windows Defender Application Guard](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97) is a new Windows feature that helps protect your users by opening untrusted web sites in a secure isolated container that is not accessible by other parts of the operating system. In this technical preview, we’ve added support to configure this feature using Configuration Manager compliance settings which you configure, and then deploy to a collection. This feature will be released in preview for the 64-bit version of the Windows 10 Creator’s Update (codename: RS2). To test this feature now, you must be using a preview version of this update.
 
### Before you start
To create and deploy Windows Defender Application Guard policies, the Windows 10 devices to which you deploy the policy must be configured with a network isolation policy. For more details, see the blog post referenced later. This capability works only with current Windows 10 Insider builds. To test it, your clients must be running a recent Windows 10 Insider Build.

### Try it out!

Ensure you have read the blog post to understand the basics about Windows Defender Application Guard.

To create a policy, and to browse the available settings:
1. In the Configuration Manager console, choose Assets and Compliance.
2. In the Assets and Compliance workspace, choose Overview > Endpoint Protection > Windows Defender Application Guard.
3. In the Home tab, in the Create group, click Create Windows Defender Application Guard Policy.
4. Using the blog post as a reference, you can browse and configure the available settings to try the feature out.
5. In this release, we’ve added the new Network Definition page to the wizard. Here, specify the corporate identity, and define your corporate network boundary.

Note:
Windows 10 PCs store only one network isolation list on the client. In this release, you can create two different kinds of network isolation lists (one from Windows Information Protection, and one from Windows Defender Application Guard), and deploy them to the client. If you deploy both policies, these network isolation lists must match. If you deploy lists that don’t match to the same client, the deployment will fail.
You can find more information about how to specify network definitions in the [Windows Information Protection documentation](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/create-wip-policy-using-sccm). 

6. When you are finished, complete the wizard, and deploy the policy to one or more Windows 10 devices.

### Further reading

To read more about Windows Defender Application Guard, see [this blog post](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97). Additionally, to learn more about Windows Defender Application Guard Standalone mode, see [this blog post](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903).



## Next Steps
For information about installing or updating the technical preview branch, see [Technical Preview for System Center Configuration Manager](/sccm/core/get-started/technical-preview).    
