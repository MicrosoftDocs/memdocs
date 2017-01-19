---
title: "Capabilities in Technical Preview 1701 for System Center Configuration Manager | Microsoft Docs"
description: "Learn about features available in the Technical Preview for System Center Configuration Manager, version 1701."
ms.custom: na
ms.date: 1/20/2017
ms.prod: configuration-manager
ms.technology:
  - configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 18598eaa-1131-44ff-8f8b-6093e87ac7a1
caps.latest.revision: 5
author: Brendunsms.author: brendunsmanager: angrobe
---
# Capabilities in Technical Preview 1701 for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Technical Preview)*



This article introduces the features that are available in the Technical Preview for System Center Configuration Manager, version 1701. You can install this version to update and add new capabilities to your Configuration Manager technical preview site. Before installing this version of the technical preview, review the introductory topic, [Technical Preview for System Center Configuration Manager](../../core/get-started/technical-preview.md), to become familiar with general requirements and limitations for using a technical preview, how to update between versions, and how to provide feedback about the features in a technical preview.    


**The following are new features you can try out with this version.**  

## Boundary groups improvements for software update points
Beginning with this preview, you now use boundary groups to associate clients with software update points. This is part of continuing work to expand the changes for boundary groups to manage additional site system roles.  Changes for boundary groups was first introduced in Technical Preview 1609 and the Current Branch in version 1610.  

With this preview, you use the new boundary group behavior to manage which software update points a client can use, similar to how you manage which distribution point a client can use:  

- You configure boundary groups to associate one or more servers that host a software update point.
- Clients that are seeking a new software update point will try to use one that is associated with their current boundary group.
- When the client fails to reach their current software update point and cannot find one from their current boundary group, the client uses Fallback behavior to expand the available pool of software update points it can use.    

For more information on boundary groups, see [Boundary groups](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#BKMK_BoundaryGroups) in the content for the Current Branch.

However, with this preview, boundary groups for software update points are only partially implemented. You can add software update points and configure neighbor boundary groups that contain software update points, but the fallback time for software update points is not yet supported, and clients will wait two hours before starting fallback.

The following describes the behavior for software update points with this technical preview:  

-	**New clients use boundary groups to select software update points,**
A client that you install after you install version 1701 selects a software update point from those associated with the client’s boundary group.

  This replaces the previous behavior where clients select a software update point randomly from a list of those that share the clients forest.   

-	**Previously installed clients continue to use their current software update point until they fallback to find a new one.**
Clients that were previously installed and that already have a software update point will continue to use that software update point until they fallback. This includes software update points that are not associated with the client’s current boundary group. They do not immediately attempt to find and use a software update point from their current boundary group.

  A client that already has a software update point begins to use this new boundary group behavior only after the client fails to reach its current software update point and starts fallback.
This delay in switching over to the new behavior is intentional. This is because a change of software update point can result in a large use of network bandwidth as the client synchronizes data with the new software update point. The delay in transition can help to avoid saturating your network should all your clients switch to new software update points at the same time.

-	**Configurations for fallback time:**
Configurations for when clients start fallback to search for a new software update point are not supported in this technical preview. This includes configurations for **Fallback times (in minutes)** and **Never fallback**, that you might configure for different boundary group relationships.

  Instead, clients retain their current behavior where a client attempts to connect to its current software update point for two hours before it starts fallback, to find a new software update point it can use.

  When a client does use fallback, it will use the boundary group configurations for fallback to create a pool of available software update points. This pool includes all software update points from the clients *current boundary group*, *neighbor boundary groups*, and the clients *site default boundary group*.

- **Configure the default site boundary group:**  
 Consider adding a software update point to the *Default-Site-Boundary-Group&lt;sitecode>*. This ensures that clients that are not members of another boundary group can fallback to find a software update point.


To manage software update points for boundary groups, use the [procedures from the Current Branch documentation](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#procedures-for-boundary-groups), but remember that fallback times you might configure are not yet used for software update points.


## Hardware inventory collects UEFI information
A new hardware inventory class (**SMS_Firmware**) and property (**UEFI**) are available to help you determine whether a computer starts in UEFI mode. When a computer is started in UEFI mode, the **UEFI** property is set to **TRUE**. This is enabled in hardware inventory by default. For more information about hardware inventory, see [How to configure hardware inventory](/sccm/core/clients/manage/inventory/configure-hardware-inventory).

## Improvements to operating system deployment
We have made the following improvements to operating system deployment, many of which were the result of your user voice feedback.
- [**Support for more applications for the Install Applications task sequence step**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17062207-task-sequence-allow-more-than-9-applications-in-t): We have increased the maximum number of applications that you can install to 99 in the **Install Applications** task sequence step. The previous maximum number was 9 applications.
- [**Select multiple apps in the Install App task sequence step**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/15459978-when-adding-items-to-an-install-application-step): When you add applications to the Install Application task sequence step in the task sequence editor, you can now select multiple applications from the **Select the application to install** pane.
- [**Expire standalone media**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/14448564-provide-a-method-for-expiring-standalone-media): When you create standalone media, there are new options to set optional start and expiration dates on the media. These settings are disabled by default. The dates are compared to the system time on the computer before the stand-alone media runs. When the system time is earlier than the start time or later than the expiration time, the stand-alone media is not started. These options are also available by using the New-CMStandaloneMedia PowerShell cmdlet.
- [**Support for additional content in stand-alone media**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8341257-support-installation-of-packages-apps-via-dynamic): Additional content is now supported in stand-alone media. You can select additional packages, driver packages, and applications to be staged on the media along with the other content referenced in the task sequence. Previously, only content referenced in the task sequence was staged on stand-alone media.
- [**Configurable timeout for Auto Apply Driver task sequence step**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17153660-auto-apply-driver-timeout): New task sequence variables are now available to configure the timeout value on the Auto Apply Driver task sequence step when making HTTP catalog requests. The following variables and default values (in seconds) are available:
   - SMSTSDriverRequestResolveTimeOut
     Default: 60
   - SMSTSDriverRequestConnectTimeOut
     Default: 60
   - SMSTSDriverRequestSendTimeOut
     Default: 60
   - SMSTSDriverRequestReceiveTimeOut
     Default: 480
- [**Package ID is now displayed in task sequence steps**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/16167430-display-packageid-when-viewing-a-task-sequence-ste): Any task sequence step that references a package, driver package, operating system image, boot image, or operating system upgrade package will now display the package ID of the referenced object. When a task sequence step references an application it will display the object ID.
- **Windows 10 ADK tracked by build version**: The Windows 10 ADK is now tracked by build version to ensure a more supported experience when customizing Windows 10 boot images. For example, if the site uses the Windows ADK for Windows 10, version 1607, only boot images with version 10.0.14393 can be customized in the console. For details about customizing WinPE versions, see [Customize boot images](/sccm/osd/get-started/customize-boot-images).
- **Default boot image source path can no longer be changed**: Default boot images are managed by Configuration Manager and the default boot image source path can no longer be changed in the Configuration Manager console or by using the Configuration Manager SDK. You can continue to configure a custom source path for custom boot images.

## Host software updates on cloud-based distribution points
Beginning with this preview version, you can use a cloud-based distribution point to host a software update package. However, because you can configure clients to download software updates directly from Microsoft Update, consider the additional costs that deploying a software update package to a cloud-based distribution point can incur.

For information about using cloud-based distribution points, see [Use a cloud-based distribution point](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point) in the content for the Current Branch of Configuration Manager.


## Use the OMS connector for Microsoft Azure Government cloud
With this technical preview, you can now use the Microsoft Operations Management Suite (OMS) connector to connect to an OMS workspace that is on Microsoft Azure Government cloud.  

To do so, you modify a configuration file to point to the Government cloud, and then install the OMS connector.

### Set up an OMS connector to Microsoft Azure Government cloud
1.  On any computer that has the Configuration Manager console installed, edit the following configuration file to point to the government cloud:  ***&lt;CM install path>\AdminConsole\bin\Microsoft.configurationManagmenet.exe.config***

  **Edits:**

    Change the value for the setting name *FairFaxArmResourceID* to be equal to “https://management.usgovcloudapi.net/”

   - **Original:**
      &lt;setting name="FairFaxArmResourceId" serializeAs="String">   
      &lt;value>&lt;/value>   
      &lt;/setting>

   - **Edited:**     
      &lt;setting name="FairFaxArmResourceId" serializeAs="String">
      &lt;value>https://management.usgovcloudapi.net/&lt;/value>  
      &lt;/setting>

  Change the value for the setting name *FairFaxAuthorityResource* to be equal to ""https://login.microsoftonline.com/""

  - **Original:**
    &lt;setting name="FairFaxAuthorityResource" serializeAs="String">   
    &lt;value>&lt;/value>

	- **Edited:**
    &lt;setting name="FairFaxAuthorityResource" serializeAs="String">   
    &lt;value>https://login.microsoftonline.com/&lt;/value>

2.	After you save the file with the two changes, restart the Configuration Manager console on the same computer, and then use that console to install the OMS connector. To install the connector, use the information in [Sync data from Configuration Manager to the Microsoft Operations Management Suite](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite), and select the **Operations Management Suite Workspace** that is on the Microsoft Azure Government cloud.

3.	After the OMS connector installs, the connection to the Government cloud is available when you use any console that connects to the site.
