---
title: "New version 1710 | Microsoft Docs"
titleSuffix: "Configuration Manager"
description: "Get details about changes and new capabilities introduced in version 1710 of System Center Configuration Manager."
ms.custom: na
ms.date:  12/08/2017
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bc6c3e5f-b9e2-400e-9d9d-446ff93c520c
author: mestew
ms.author: mstewart
manager: angrobe
---
# What&#39;s new in version 1710 of System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Update 1710 for System Center Configuration Manager current branch is available as an in-console update for previously installed sites that run version 1610, 1702, or 1706.

> [!TIP]  
> To install a new site, you must use a baseline version of Configuration Manager.  
>  Learn more about:    
>   - [Installing new sites](/sccm/core/servers/deploy/install/installing-sites)  
>   - [Installing updates at sites](/sccm/core/servers/manage/updates)  
>   - [Baseline and update versions](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

The following sections provide details about changes and new capabilities introduced in version 1710 of Configuration Manager.  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated features](/sccm/core/plan-design/changes/removed-and-deprecated-features).

Version 1710 drops support for the following products:
-->


## Site infrastructure

### Updates for Peer Cache  <!-- sms500850 -->
Beginning with this release, Peer Cache is no longer a pre-release feature.  No other changes for Peer Cache are introduced with this release. For more information, see  [Peer Cache for Configuration Manager clients](/sccm/core/plan-design/hierarchy/client-peer-cache).

### Cloud distribution point support for Azure Government Cloud   <!-- sms491428 -->
You can now use [cloud-based distribution points](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point) in the Azure Government cloud.   

### Inventory default unit revision <!-- sms503697 -->
As devices now include hard drives with sizes in the gigabyte (GB), terabyte (TB) and larger scales, this release changes the default unit (SMS_Units) used in many views from megabytes (MB) to GB. For example, the v_gs_LogicalDisk.FreeSpace value now reports GB units.


<!-- ## Migration  -->


## Client management

### Co-management for Windows 10 devices    
<!-- 1350871 -->
In the previous Windows 10 updates, you can already join a Windows 10 device to on-premises Active Directory (AD) and cloud-based Azure AD at the same time (hybrid Azure AD). Starting with Configuration Manager version 1710, co-management takes advantage of this improvement and enables you to concurrently manage Windows 10, version 1709 (also known as the Fall Creators Update) devices by using both Configuration Manager and Intune. It’s a solution that provides a bridge from traditional to modern management and gives you a path to make the transition using a phased approach. For details, see [Co-management for Windows 10 devices](/sccm/core/clients/manage/co-management-overview).

### Restart computers from the Configuration Manager console  <!-- 1356283 -->
Beginning with this release, you can use the Configuration Manager console to identify client devices that require a restart, and then use a client notification action to restart them.

See [How to manage clients in System Center Configuration Manager](/sccm/core/clients/manage/manage-clients#restart-clients)


<!-- ## Compliance settings -->


## Application Management
### Improvements for Run Scripts   <!-- 1236459 -->
This release brings several improvements to the **Run Scripts** feature, which lets you deploy PowerShell scripts to run on managed devices. This feature was first introduced in version 1706.

Improvements include:
- Use Security Scopes to help control who can use Run Scripts
- Real-time monitoring of the scripts you run
- Parameters for the script display in Create Script Wizard, support validation, and are identified as mandatory or optional.

For more on using Run Scripts, see [Create and run scripts](../../../apps/deploy-use/create-deploy-scripts.md).

### New mobile application management policy settings
<!-- 1324760 -->
The following settings have been added to the mobile application management policy settings:
- **Disable contact sync**: Prevents the app from saving data to the native Contacts app on the device.
- **Disable printing**: Prevents the app from printing work or school data.

### Software Center no longer distorts icons larger than 250x250  
<!-- 1356194 -->

With this release, Software Center will no longer distort icons that are larger than 250x250. Software Center made such icons look blurry. You can now set an icon with a pixel dimensions of up to 512x512, and it displays without distortion.

To add an icon for your app in Software Center, see [Create applications](/sccm/apps/deploy-use/create-applications).

## Operating system deployment
 > [!TIP]   
 > <!-- 1354281 -->
 > Beginning with the Windows 10, version 1709 (also known as the Fall Creators Update) release, Windows media includes multiple editions. When configuring a task sequence to use an operating system upgrade package or operating system image, be sure to select an [edition that is supported for use by Configuration Manager](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-as-a-client).

### Add child task sequences to a task sequence
<!-- 1261338 -->

You can add a new task sequence step that runs another task sequence, which creates a parent/child relationship between the task sequences. This allows you to create more modular task sequences that you can re-use.  

To learn more about the child task sequence, see [Child task sequence](/sccm/osd/understand/task-sequence-steps#child-task-sequence).

## Software Center customization
<!-- 1351224 -->
You can add enterprise branding elements and specify the visibility of tabs on Software Center. You can add your Software Center specific company name, set a Software Center configuration color theme, set a company logo, and set the visible tabs for client devices.

For more information, see [Plan for and configure application management in System Center Configuration Manager](/sccm/apps/plan-design/plan-for-and-configure-application-management).

## Software updates

### Surface driver updates  <!-- 1098490 -->
Beginning with this release, managing Surface driver updates is no longer a pre-release feature.  


## Reporting

### Limit Windows 10 Enhanced telemetry to only send data relevant to Windows Analytics Device Health
<!-- 1356148 -->

You can now set the Windows 10 telemetry data collection level to **Enhanced (Limited)**. This setting enables you to gain actionable insight about devices in your environment without devices reporting all of the data in the **Enhanced** telemetry level with Windows 10 version 1709 or later.

For more information, see [How to configure client settings in System Center Configuration Manager](/sccm/core/clients/deploy/configure-client-settings).

<!-- ## Inventory  -->


## Mobile device management

### Actions for non-compliance 
<!--1321366 -->    
You can now configure a time-ordered sequence of actions that are applied to devices that fall out of compliance. For example, you can notify users of non-compliant devices via e-mail or mark those devices non-compliant. For details, see [Set up actions for non-compliance](/sccm/mdm/deploy-use/actions-for-noncompliance).

### Windows 10 ARM64 device support
<!-- 1355000 -->

Hybrid mobile device management (MDM) scenarios will be supported on ARM64 devices running Windows 10 when these devices are available.

These scenarios include:

- [Enroll devices](../../../mdm/deploy-use/enroll-hybrid-windows.md)
- [Perform remote full and selective wipe actions](../../../mdm/deploy-use/wipe-lock-reset-devices.md)
- [Manage settings through configuration items and baselines](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)
- [Manage compliance policy](../../../mdm/deploy-use/device-compliance-policies.md)
- Manage access to company resources through:
   - [Certificate profiles](../../../mdm/deploy-use/create-pfx-certificate-profiles.md)
   - [VPN profiles](../../../mdm/deploy-use/create-vpn-profiles.md)
   - [Wi-Fi profiles](../../../mdm/deploy-use/create-wifi-profiles.md)
   - [Email profiles](../../../mdm/deploy-use/create-exchange-activesync-profiles.md)
- [Configure Windows Hello for Business policy](../../../mdm/deploy-use/windows-hello-for-business-settings.md)
- [Manage applications](../../../mdm/deploy-use/management-tasks-applications.md)

### Improved VPN Profile Experience in Configuration Manager Console 
<!-- 1318232 -->

With this release, we’ve updated the VPN profile wizard and properties pages to display settings appropriate for the selected platform:


- Each platform has its own workflow, meaning that new VPN profiles contain only the setting supported by the platform.
- The **Supported Platforms** page now appears after the **General** page.  You now choose the platform before setting property values.
- When the platform is set to **Android**, **Android for Work**, or **Windows Phone 8.1**, the **Supported platforms** page is not needed and is not displayed.
- The Configuration Manager client-based workflow has been combined with the hybrid mobile device (MDM) client-based Windows 10 workflows; they support the same settings.
- Each platform workflow includes just the settings appropriate for that workflow.  For example, the Android workflow contains settings appropriate for Android; settings appropriate for iOS or Windows 10 Mobile no longer appear in the Android workflow.
- The Automatic VPN page is obsolete and has been removed.

These changes apply to new VPN profiles.  

To minimize compatibility risk, existing VPN profiles are unchanged.  When you edit an existing profile, the settings appear as they did when the profile was created.  

For more information, see [VPN Profiles on mobile devices in System Center Configuration Manager](../../../mdm/deploy-use/create-vpn-profiles.md).

### Limited support for Cryptography: Next Generation (CNG) certificates <!-- 1356191 -->

Configuration Manager has limited support for Cryptography: Next Generation (CNG) certificates. Configuration Manager clients can use PKI client authentication certificate with private key in CNG Key Storage Provider (KSP). With KSP support, Configuration Manager clients support hardware-based private key, such as TPM KSP for PKI client authentication certificates.

For more information, see [CNG certificates overview](../network/cng-certificates-overview.md).

## Protect devices

### Create and deploy Exploit Guard policies
<!-- 1355468 -->

You can [create and deploy policies](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy) that manage all four components of Windows Defender Exploit Guard, including attack surface reduction, controlled folder access, exploit protection, and network protection.

### Create and deploy Windows Defender Application Guard policy
<!-- 1351960 -->

You can [create and deploy Windows Defender Application Guard policies](/sccm/protect/deploy-use/create-deploy-application-guard-policy) by using the Configuration Manager endpoint protection.

### Device Guard policy changes
<!-- 1355092 -->
The following three changes have been made in relation to Device Guard policies:

- Device Guard policies have been renamed to Windows Defender Application Control policies. So, for example, the **Create Device Guard policy wizard** is now named **Create Windows Defender Application Control policy wizard**.
- Devices using the Fall Creators Update for Windows version 1709 don’t require a restart to apply the Windows Defender Application Control policies. Restarting is still the default, but you can [turn off restarts](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager).
- You can [set devices to automatically run software](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager) trusted by the Intelligent Security Graph.





## Next Steps
When your ready to install this version, see [Updates for Configuration Manager](/sccm/core/servers/manage/updates).
