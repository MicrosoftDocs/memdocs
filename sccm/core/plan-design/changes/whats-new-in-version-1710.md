---
title: "New version 1710 | Microsoft Docs"
titleSuffix: "Configuration Manager"
description: "Get details about changes and new capabilities introduced in version 1710 of System Center Configuration Manager."
ms.custom: na
ms.date:  11/20/2017
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bc6c3e5f-b9e2-400e-9d9d-446ff93c520c
author: Brenduns
ms.author: brenduns
manager: angrobe
---
# What&#39;s new in version 1710 of System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Update 1710 for System Center Configuration Manager current branch is available as an in-console update for previously installed sites that run version 1610, 1702, or 1706.

> [!TIP]  
> To install a new site, you must use a baseline version of Configuration Manager.  
>  Learn more about:    
>   - [Installing new sites](https://technet.microsoft.com/library/mt590197.aspx)  
>   - [Installing updates at sites](https://technet.microsoft.com/library/mt607046.aspx)  
>   - [Baseline and update versions](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

The following sections provide details about changes and new capabilities introduced in version 1710 of Configuration Manager.  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated features](/sccm/core/plan-design/changes/removed-and-deprecated-features).

Version 1710 drops support for the following products:
-->


## Site infrastructure

### Updates for Peer Cache  
Beginning with this release, Peer Cache is no longer a pre-release feature.  No other changes for Peer Cache are introduced with this release. For more information, see  [Peer Cache for Configuration Manager clients](/sccm/core/plan-design/hierarchy/client-peer-cache).

### Cloud distribution point support for Azure Government Cloud
You can now use [cloud-based distribution points](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point) in the Azure Government cloud.   


<!-- ## Migration  -->


## Client management

### Co-management for Windows 10 devices    
<!-- 1350871 -->
Starting with the Windows 10, version 1607 (also known as the Anniversary Update), you can join a Windows 10 device to on-premises Active Directory (AD) and cloud-based Azure AD at the same time (hybrid Azure AD). Co-management takes advantage of this improvement and enables you to concurrently manage Windows 10 devices by using both Configuration Manager and Intune. It’s a solution that provides a bridge from traditional to modern management and gives you a path to make the transition using a phased approach. For details, see [Co-management for Windows 10 devices](/sccm/core/clients/manage/co-management-overview.md).


<!--  ## Compliance settings  -->


## Application Management
### Improvements for Run Scripts   <!-- 1236459 -->
This release brings several improvements to the **Run Scripts** feature which lets you deploy PowerShell scripts to run on managed devices. This feature was first introduced in version 1706.

Improvements include:
- Use Security Scopes to help control who can use Run Scripts
- Real-time monitoring of the scripts you run
- Parameters for the script display in Create Script Wizard, support validation, and are identified as mandatory or optional.

For more on using Run Scripts, see [Create and run scripts](../../../apps/deploy-use/create-deploy-scripts.md).

### New mobile application management policy settings
<!-- 1324760 -->
- **Disable contact sync**: Prevents the app from saving data to the native Contacts app on the device.
- **Disable printing**: Prevents the app from printing work or school data.

## Operating system deployment
 > [!TIP]
 > Beginning with the Windows 10, version 1709 (also known as the Fall Creators Update) release, Windows media includes multiple editions. When configuring a task sequence to use an operating system upgrade package or operating system image, be sure to select an [edition that is supported for use by Configuration Manager](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-as-a-client).


<!--  ## Software updates  -->


<!--  ## Reporting  -->


<!-- ## Inventory  -->


## Mobile device management

### Windows 10 ARM64 device support
<!-- 1355000 -->

Hybrid mobile device management (MDM) scenarios will be supported on ARM64 devices running Windows 10 when these devices are available.

These scenarios include:

- [Enroll devices](../../../mdm/deploy-use/enroll-hybrid-windows.md)
- [Perform remote full and selective wipe actions](../../../mdm/deploy-use/wipe-lock-reset-devices.md)
- [Manage settings through configuration items and baselines](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)
- [Manage compliance policy](../../../mdm/deploy-use/device-compliance-policies.md)
- [Manage conditional access](../../../mdm/deploy-use/manage-access-to-services.md)
- Manage access to company resources through:
   - [Certificate profiles](../../../mdm/deploy-use/create-pfx-certificate-profiles.md)
   - [VPN profiles](../../../mdm/deploy-use/create-vpn-profiles.md)
   - [Wi-Fi profiles](../../../mdm/deploy-use/create-wifi-profiles.md)
   - [Email profiles](../../../mdm/deploy-use/create-exchange-activesync-profiles.md)
- [Configure Windows Hello for Business policy](../../../mdm/deploy-use/windows-hello-for-business-settings.md)
- [Manage applications](../../../mdm/deploy-use/management-tasks-applications.md)

### Improved VPN Profile Experience in Configuration Manager Console <!-- 1318232 -->

With this release, we’ve updated the VPN profile wizard and properties pages to display settings appropriate for the selected platform:


- Each platform has its own workflow, meaning that new VPN profiles contain only the setting supported by the platform.
- The **Supported Platforms** pages now appears after the **General** page.  You now choose the platform before setting property values.
- When the platform is set to **Android**, **Android for Work**, or **Windows Phone 8.1**, the **Supported platforms** page is not needed and is not displayed.
- The Configuration Manager client-based workflow has been combined with the hybrid mobile device (MDM) client-based Windows 10 workflows; they support the same settings.
- Each platform workflow includes just the settings appropriate for that workflow.  For example, the Android workflow contains settings appropriate for Android; settings appropriate for iOS or Windows 10 Mobile no longer appear in the Android workflow.
- For Windows 8.1 devices, connection types managed by Configuration Manager client only (not supported by Intune) are clearly marked.
- The Automatic VPN page is obsolete and has been removed.

These changes apply to new VPN profiles.  

To minimize compatibility risk, existing VPN profiles are unchanged.  When you edit an existing profile, the settings appear as they did when the profile was created.  

For more information, see [VPN Profiles on mobile devices in System Center Configuration Manager](../../../mdm/deploy-use/create-vpn-profiles.md).


<!--  ## Protect devices   -->


## Next Steps
When your ready to install this version, see [Updates for Configuration Manager](/sccm/core/servers/manage/updates).
