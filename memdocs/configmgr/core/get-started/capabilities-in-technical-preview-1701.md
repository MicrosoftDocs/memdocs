---
title: Capabilities in Technical Preview 1701
titleSuffix: Configuration Manager
description: Learn about features available in the Technical Preview for Configuration Manager, version 1701.
ms.date: 01/23/2017
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: conceptual
author: Banreet
manager: apoorvseth
ms.author: banreetkaur
ROBOTS: NOINDEX
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# Capabilities in Technical Preview 1701 for Configuration Manager

*Applies to: Configuration Manager (technical preview branch)*



This article introduces the features that are available in the Technical Preview for Configuration Manager, version 1701. You can install this version to update and add new capabilities to your Configuration Manager technical preview site. Before installing this version of the technical preview, review the introductory topic, [Technical Preview for Configuration Manager](../../core/get-started/technical-preview.md), to become familiar with general requirements and limitations for using a technical preview, how to update between versions, and how to provide feedback about the features in a technical preview.    


**The following are new features you can try out with this version.**  

## Boundary groups improvements for software update points
Beginning with this preview, you now use boundary groups to associate clients with software update points. This is part of continuing work to expand the changes for boundary groups to manage additional site system roles.  Changes for boundary groups was first introduced in Technical Preview 1609 and the Current Branch in version 1610.  

With this preview, you use the new boundary group behavior to manage which software update points a client can use, similar to how you manage which distribution point a client can use:  

- You configure boundary groups to associate one or more servers that host a software update point.
- Clients that are seeking a new software update point will try to use one that is associated with their current boundary group.
- When the client fails to reach their current software update point and cannot find one from their current boundary group, the client uses Fallback behavior to expand the available pool of software update points it can use.    

For more information on boundary groups, see [Boundary groups](../servers/deploy/configure/boundary-groups.md) in the content for the Current Branch.

However, with this preview, boundary groups for software update points are only partially implemented. You can add software update points and configure neighbor boundary groups that contain software update points, but the fallback time for software update points is not yet supported, and clients will wait two hours before starting fallback.

The following describes the behavior for software update points with this technical preview:  

- **New clients use boundary groups to select software update points,**
  A client that you install after you install version 1701 selects a software update point from those associated with the client's boundary group.

  This replaces the previous behavior where clients select a software update point randomly from a list of those that share the clients forest.   

- **Previously installed clients continue to use their current software update point until they fallback to find a new one.**
  Clients that were previously installed and that already have a software update point will continue to use that software update point until they fallback. This includes software update points that are not associated with the client's current boundary group. They do not immediately attempt to find and use a software update point from their current boundary group.

  A client that already has a software update point begins to use this new boundary group behavior only after the client fails to reach its current software update point and starts fallback.
  This delay in switching over to the new behavior is intentional. This is because a change of software update point can result in a large use of network bandwidth as the client synchronizes data with the new software update point. The delay in transition can help to avoid saturating your network should all your clients switch to new software update points at the same time.

- **Configurations for fallback time:**
  Configurations for when clients start fallback to search for a new software update point are not supported in this technical preview. This includes configurations for **Fallback times (in minutes)** and **Never fallback**, that you might configure for different boundary group relationships.

  Instead, clients retain their current behavior where a client attempts to connect to its current software update point for two hours before it starts fallback, to find a new software update point it can use.

  When a client does use fallback, it will use the boundary group configurations for fallback to create a pool of available software update points. This pool includes all software update points from the clients *current boundary group*, *neighbor boundary groups*, and the clients *site default boundary group*.

- **Configure the default site boundary group:**  
  Consider adding a software update point to the *Default-Site-Boundary-Group&lt;sitecode>*. This ensures that clients that are not members of another boundary group can fallback to find a software update point.


To manage software update points for boundary groups, use the [procedures from the Current Branch documentation](../servers/deploy/configure/boundary-group-procedures.md), but remember that fallback times you might configure are not yet used for software update points.


## Hardware inventory collects UEFI information
A new hardware inventory class (**SMS_Firmware**) and property (**UEFI**) are available to help you determine whether a computer starts in UEFI mode. When a computer is started in UEFI mode, the **UEFI** property is set to **TRUE**. This is enabled in hardware inventory by default. For more information about hardware inventory, see [How to configure hardware inventory](../clients/manage/inventory/configure-hardware-inventory.md).

## Improvements to operating system deployment
We have made the following improvements to operating system deployment, many of which were the result of your feedback.
- **Support for more applications for the Install Applications task sequence step**: We have increased the maximum number of applications that you can install to 99 in the **Install Applications** task sequence step. The previous maximum number was 9 applications.
- **Select multiple apps in the Install App task sequence step**: When you add applications to the Install Application task sequence step in the task sequence editor, you can now select multiple applications from the **Select the application to install** pane.
- **Expire standalone media**: When you create standalone media, there are new options to set optional start and expiration dates on the media. These settings are disabled by default. The dates are compared to the system time on the computer before the stand-alone media runs. When the system time is earlier than the start time or later than the expiration time, the stand-alone media is not started. These options are also available by using the New-CMStandaloneMedia PowerShell cmdlet.
- **Support for additional content in stand-alone media**: Additional content is now supported in stand-alone media. You can select additional packages, driver packages, and applications to be staged on the media along with the other content referenced in the task sequence. Previously, only content referenced in the task sequence was staged on stand-alone media.
- **Configurable timeout for Auto Apply Driver task sequence step**: New task sequence variables are now available to configure the timeout value on the Auto Apply Driver task sequence step when making HTTP catalog requests. The following variables and default values (in seconds) are available:
   - SMSTSDriverRequestResolveTimeOut
     Default: 60
   - SMSTSDriverRequestConnectTimeOut
     Default: 60
   - SMSTSDriverRequestSendTimeOut
     Default: 60
   - SMSTSDriverRequestReceiveTimeOut
     Default: 480
- **Package ID is now displayed in task sequence steps**: Any task sequence step that references a package, driver package, operating system image, boot image, or operating system upgrade package will now display the package ID of the referenced object. When a task sequence step references an application it will display the object ID.
- **Windows 10 ADK tracked by build version**: The Windows 10 ADK is now tracked by build version to ensure a more supported experience when customizing Windows 10 boot images. For example, if the site uses the Windows ADK for Windows 10, version 1607, only boot images with version 10.0.14393 can be customized in the console. For details about customizing WinPE versions, see [Customize boot images](../../osd/get-started/customize-boot-images.md).
- **Default boot image source path can no longer be changed**: Default boot images are managed by Configuration Manager and the default boot image source path can no longer be changed in the Configuration Manager console or by using the Configuration Manager SDK. You can continue to configure a custom source path for custom boot images.

## Host software updates on cloud-based distribution points
Beginning with this preview version, you can use a cloud-based distribution point to host a software update package. However, because you can configure clients to download software updates directly from Microsoft Update, consider the additional costs that deploying a software update package to a cloud-based distribution point can incur.

For information about using cloud-based distribution points, see [Use a cloud-based distribution point](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md) in the content for the Current Branch of Configuration Manager.

## Validate device health attestation data via management points

Beginning with this preview version, you can configure management points to validate health attestation reporting data for cloud or on-premises health attestation service. A new **Advanced Options** tab in the **Management Point Component Properties** dialog box lets you **Add**, **Edit**, or **Remove** the **On-premises device health attestation service URL**. You can also specify **Custom Device Settings** for the client agent to **Use on-premises Health Attestation Service**.  Setting **Yes** for this setting will enable reporting to the on-premises management point instead of the cloud-based service.

### Try it out

- **Enable on-premises device health attestation on a management point**<br>  In the Configuration Manager console, navigate to the management point and open **Management Point Component Properties** and then click the **Advanced Options** tab. Click **Add** and specify the on-premises URL (for example, https://10.10.10.10) for **On-premises device health attestation service URLs**.
- **Enable on-premises management point health attestation reporting for the client agent**<br>In the Configuration Manager console, choose **Administration** > **Client Settings** and double-click or create a new **Custom Device Settings**. Select **Computer Agent** and set **Use on-premises Health Attestation Service** to **Yes**. If **Enable communication with Device Health Attestation Service** is set to **Yes** and **Use on-premises Health Attestation** is set to **No**, the management point will use the cloud-based device health attestation service.

## Use the OMS connector for Microsoft Azure Government cloud
With this technical preview, you can now use the Microsoft Operations Management Suite (OMS) connector to connect to an OMS workspace that is on Microsoft Azure Government cloud.  

To do so, you modify a configuration file to point to the Government cloud, and then install the OMS connector.

### Set up an OMS connector to Microsoft Azure Government cloud
1. On any computer that has the Configuration Manager console installed, edit the following configuration file to point to the government cloud:  ***&lt;CM install path>\AdminConsole\bin\Microsoft.configurationManagmenet.exe.config***

   **Edits:**

   Change the value for the setting name *FairFaxArmResourceID* to be equal to ```<https://management.usgovcloudapi.net/>```

   - **Original:**
     &lt;setting name="FairFaxArmResourceId" serializeAs="String">   
     &lt;value>&lt;/value>   
     &lt;/setting>

   - **Edited:**     
     &lt;setting name="FairFaxArmResourceId" serializeAs="String">
     &lt;value&gt;https://management.usgovcloudapi.net/&lt;/value&gt;  
     &lt;/setting>

   Change the value for the setting name *FairFaxAuthorityResource* to be equal to "<https://login.microsoftonline.com/>"

   - **Original:**
     &lt;setting name="FairFaxAuthorityResource" serializeAs="String">   
     &lt;value>&lt;/value>

   - **Edited:**
     &lt;setting name="FairFaxAuthorityResource" serializeAs="String">   
     &lt;value&gt;[https://login.microsoftonline.com](https://login.microsoftonline.com)&lt;/value&gt;

2. After you save the file with the two changes, restart the Configuration Manager console on the same computer, and then use that console to install the OMS connector. To install the connector, use the information in [Sync data from Configuration Manager to the Microsoft Operations Management Suite](/azure/azure-monitor/platform/collect-sccm), and select the **Operations Management Suite Workspace** that is on the Microsoft Azure Government cloud.

3. After the OMS connector installs, the connection to the Government cloud is available when you use any console that connects to the site.

## Android and iOS versions are no longer targetable in creation wizards for hybrid MDM

Beginning in this technical preview for hybrid mobile device management (MDM), you no longer need to target specific versions of Android and iOS when creating new policies and profiles for Intune-managed devices. Instead, you choose one of the following device types:

- Android
- Samsung KNOX Standard 4.0 and higher
- iPhone
- iPad

This change affects the wizards for creating the following items:

- Configuration items
- Compliance policies
- Certificate profiles
- Email profiles
- VPN profiles
- Wi-Fi profiles

With this change, hybrid deployments can provide support more quickly for new Android and iOS versions without needing a new Configuration Manager release or extension. Once a new version is supported in Intune standalone, users will be able to upgrade their mobile devices to that version.

To prevent issues when upgrading from prior versions of Configuration Manager, mobile operating system versions are still available in the properties pages for these items. If you still need to target a specific version, you can create the new item, and then specify the targeted version on the properties page of the newly created item.
