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
  1. In the console, go to **Administration** > **Overview** > **Site Configuration** > **Servers and Site System Roles**, and then select the passive mode site server.
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

With this release, you can now set the Windows 10 telemetry data collection level to **Enhanced (Limited)**. This setting enables you to gain actionable insight about devices in your environment without devices reporting all of the data in the **Enhanced** telemetry level with Windows 10 version 1709 or later.

The Enhanced (Limited) telemetry level includes metrics from the basic level, as well as a subset of data collected from the **Enhanced** level relevant to Windows Analytics. For more information on telemetry levels, see [Telemetry levels](https://docs.microsoft.com/windows/configuration/configure-windows-telemetry-in-your-organization#telemetry-levels).

### Try it out!

To configure Windows 10 telemetry collection on clients, see [How to configure client settings](/sccm/core/clients/deploy/configure-client-settings). Open the **Cloud Services** window, and set Windows 10 telemetry to **Enhanced**.

## Software Center no longer distorts icons larger than 250x250  
<!-- 1356194 -->

With this release, Software Center will no longer distort icons that are larger than 250x250. Software Center made such icons look blurry. You can now set an icon with a pixel dimensions of up to 512x512, and it displays without distortion.

### Try it out!

Add an icon for your app in Software Center. To try it out see [Create applications](/sccm/apps/deploy-use/create-applications).


<!-- ## See also
For information about installing or updating the technical preview branch, see [Technical Preview for System Center Configuration Manager](/sccm/core/get-started/technical-preview).   -->
