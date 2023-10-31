---
title: New version 1706
titleSuffix: Configuration Manager
description: Get details about changes and new capabilities introduced in version 1706 of Configuration Manager.
ms.date: 08/11/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ROBOTS: NOINDEX
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# What&#39;s new in version 1706 of Configuration Manager

*Applies to: Configuration Manager (current branch)*

Update 1706 for Configuration Manager current branch is available as an in-console update for previously installed sites that run version 1606, 1610, or 1702.

> [!TIP]  
> To install a new site, you must use a baseline version of Configuration Manager.  
>
> Learn more about:    
> - [Installing new sites](../../servers/deploy/install/installing-sites.md)  
> - [Installing updates at sites](../../servers/manage/updates.md)  
> - [Baseline and update versions](../../servers/manage/updates.md#bkmk_Baselines)  

The following sections provide details about changes and new capabilities introduced in version 1706 of Configuration Manager.  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated items](deprecated/removed-and-deprecated.md).

Version 1706 drops support for the following products:
-->


## Site infrastructure

### Client Peer Cache support for express installation files for Windows 10 and Microsoft 365  
<!-- 1352486 -->
Beginning with this release, Peer Cache supports distribution of content express installation files for Windows 10, and of update files for Microsoft 365. No additional configurations are required to support this change.

### Updates for the data warehouse
<!-- 1277922 -->
The data warehouse is no longer a pre-release feature. We have also updated the prerequisites to include support for the database on SQL Server Always On availability groups, and failover cluster instances. For more information, see [The Data Warehouse service point](../../servers/manage/data-warehouse.md).

### Accessibility improvements
<!-- 1253000 -->
We have added additional improvements to accessibility for the Configuration Manager console. For details, see [Accessibility features](../../understand/accessibility-features.md).

### Improvements  for SQL Server Always On availability groups
<!-- 1352094 -->
With this release, you can now use asynchronous commit replicas in the SQL Server Always On availability groups you use with Configuration Manager. This means you can add additional replicas to your availability groups to use as off-site (remote) backups, and then use them in a disaster recovery scenario.  
- Configuration Manager supports using the asynchronous commit replica to recover your synchronous replica. See [site database recovery options](../../servers/manage/recover-sites.md#site-database-recovery-options) in the Backup and Recovery topic for information on how to accomplish this.
- This release does not support failover to use the asynchronous commit replica as your site database.
For more information, see [Prepare to use an availability group](../../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).

### Update reset tool
<!-- 1324589 -->
Beginning with version 1706, Configuration Manager primary sites, and central administration sites include the Configuration Manager Update Reset Tool, **CMUpdateReset.exe**. Use this tool with any version of the current branch that remains in support, to fix issues when in-console updates have problems downloading or replicating. For more information, see [Update reset tool](../../servers/manage/update-reset-tool.md).

### High DPI console support  
<!-- 1353476 -->
With this release, issues with how the Configuration Manager console scales and displays different parts of the UI when viewed on high DPI devices (like a Surface book) should be fixed.

### Improved boundary groups for software update points
<!-- 1324591 -->
This release includes improvements for how software update points work with boundary groups. The following summarizes the new fallback behavior:
- Fallback for software update points now uses a configurable time for fallback to neighbor boundary groups.
- Independent of the fallback configuration, a client attempts to reach the last software update point it used for 120 minutes. After failing to reach that server for 120 minutes, the client then checks its pool of available software update points, so it can find a new one.
- After failing to reach its original server for two hours, the client switches to a shorter cycle for contacting a new software update point. This means if a client fails to connect with a new server, it quickly selects the next server from its pool of available servers and attempts to contact that one.

For more information, see [software update points](../../servers/deploy/configure/boundary-groups-software-update-points.md) in the Boundary Groups topic for the Current Branch.

### Azure AD integration with Configuration Manager
<!-- 1248187, 1290765, 1258052, 1298097, 1319334, 1319883, 1352135, 1353331 -->
With this release, we have improved the integration of Configuration Manager and Azure Active Directory (Azure AD).  These improvements streamline how you configure the Azure services you use with Configuration Manager, and help you to manage clients and users who authenticate though Azure AD.

The improved integration makes the following possible:  
- Azure Services Wizard – This Wizard provides a common configuration experience that replaces the individual workflows to set up the following Azure services you use with Configuration Manager.
  - **Cloud Management**
    Enable clients to authenticate by using Azure Active Directory (Azure AD). You can also configure Azure AD User Discovery.
  - **Log Analytics Connector**
    Connect to Azure Log Analytics and sync collection data.
  - **Upgrade Readiness**
    Connect to Upgrade Readiness and view client upgrade-compatibility data.
  - **Windows Store for Business**
    Connect to the on-line store for Windows Store for Business and get apps for your organization that you can deploy with Configuration Manager.


  This is done by using an [Azure server web app](/azure/app-service/app-service-authentication-overview) to provide the subscription and configuration details that you otherwise enter each time you set up a new Configuration Manager component or service with Azure. For more information, see [Azure Services Wizard](../../servers/deploy/configure/azure-services-wizard.md).

- Use Azure AD to authenticate clients on the internet to access your Configuration Manager sites. Azure AD replaces the need to configure and use client authentication certificates. This requires the cloud management gateway site system role. For more information, see [Install and assign Configuration Manager clients from the internet using Azure AD for authentication](../../clients/deploy/deploy-clients-cmg-azure.md).

- Install and manage the Configuration Manager client on computers that are located on the internet. This requires the use of the cloud management gateway site system role. For more information, see [Install and assign Configuration Manager clients from the internet using Azure AD for authentication](../../clients/deploy/deploy-clients-cmg-azure.md).

- Configure Azure AD User Discovery.  Use the Azure Services Wizard to configure this new discovery method. This new method queries your Azure AD for user data you can then use along-side traditional discovery data.  Both full and delta synchronization are supported.  For more information see [Azure AD User Discovery](../../servers/deploy/configure/about-discovery-methods.md#azureaddisc).

### Peer cache improvements
<!-- 1252345 -->
Peer cache no longer uses the Network Access Account to authenticate download requests from peers. There is one caveat to this when the account remains required by clients. This remains a requirement for clients that boot in to WinPE and then access content from a peer cache source. For more information, see [requirements and considerations for peer cache](../hierarchy/client-peer-cache.md#requirements).


<!-- ## Migration  -->


<!-- ## Client management  -->


## Compliance settings

### New configuration settings for Windows 10 devices that are not managed with the Configuration Manager client
<!-- 1354715 -->
In this release, we've added new configuration item settings for Windows 10 devices that are enrolled with Intune, or managed on premises by Configuration Manager. The settings are:

- **Password**
  - Device Encryption
- **Device**
  - Region settings modification (desktop only)
  - Power and sleep settings modification
  - Language settings modification
  - System time modification
  - Device name modification
- **Store**
  - Auto-update apps from store
  - Use private store only
  - Store originated app launch
- **Microsoft Edge**
  - Block access to about:flags
  - SmartScreen prompt override
  - SmartScreen prompt override for files
  - WebRTC localhost IP address
  - Default search engine
  - OpenSearch XML URL
  - Homepages (desktop only)

For details of all Windows 10 settings, see [How to create configuration items for Windows 8.1 and Windows 10 devices managed without the Configuration Manager client](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).

### New device compliance policy rules

* **Required password type**. Specify whether the user must create an alphanumeric password or a numeric password. For alphanumeric passwords, you also specify the minimum number of character sets that the password must have. The four character sets are: Lowercase, uppercase letters, symbols and numbers.

  **Supported on:**
  * Windows Phone 8+
  * Windows 8.1+
  * iOS 6+
  <br></br>
* **Block USB debugging on device**. You do not have to configure this settings as USB debugging is already disabled on Android for Work devices.

  **Supported on:**
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
  <br></br>
* **Block apps from unknown sources**. Require that devices prevent installation of apps from unknown sources. You do not have to configure this setting as Android for Work devices always restrict installation from unknown sources.

  **Supported on:**
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
  <br></br>
* **Require threat scan on apps**. This setting specifies that the Verify apps feature is enabled on the device.

  **Supported on:**
  * Android 4.2 through 4.4
  * Samsung KNOX Standard 4.0+


## Application Management

### Run PowerShell scripts from the Configuration Manager console
<!-- 1236459 -->

In Configuration Manager, you can deploy scripts to client devices using packages and programs. In this release, we've added new functionality that lets you take the following actions:

- Import PowerShell Scripts to Configuration Manager
- Edit the scripts from the Configuration Manager console (for unsigned scripts only)
- Mark scripts as Approved or Denied, to improve security
- Run scripts on collections of Windows client PCs, and on-premises managed Windows PCs. You don't deploy scripts, instead, they are run in near real time on client devices.
- Examine the results returned by the script in the Configuration Manager console.

For more information, see [Create and run PowerShell scripts from the Configuration Manager console](../../../apps/deploy-use/create-deploy-scripts.md).

### New mobile application management policy settings    
<!--1324760-->
Beginning with this release, you can use three new mobile application management (MAM) policy settings:

- **Block screen capture (Android devices only):** Specifies that the screen capture capabilities of the device are blocked when using this app.


## Operating system deployment

### Hardware inventory collects Secure Boot information
Hardware inventory now collects information about whether Secure Boot is enabled on clients. This information is stored in the **SMS_Firmware** class (introduced in version 1702) and enabled in hardware inventory by default. For more information about hardware inventory, see  [How to configure hardware inventory](../../clients/manage/inventory/configure-hardware-inventory.md).

### Collapsible task sequence groups
This version introduces the ability to expand and collapse task sequence groups. You can expand or collapse individual groups or expand or collapse all groups at once.

### Reload boot images with current Windows PE version
When you run **Update Distribution Points** on a selected boot image, you can now choose to reload the latest version of Windows PE (from the Windows ADK installation directory) in the boot image. For more information, see [Update distribution points with the boot image](../../../osd/get-started/manage-boot-images.md#update-distribution-points-with-the-boot-image).

## Software updates

### Improvements to Express Update download time
In this release, we have significantly improved the download time for Express Updates. For more information, see [Manage Express installation files for Windows 10 updates](../../../sum/deploy-use/manage-express-installation-files-for-windows-10-updates.md).

### Manage Microsoft Surface driver updates
<!-- 1098490 -->
You can now use Configuration Manager to manage Microsoft Surface driver updates.    


#### Prerequisites
- All software update points must run Windows Server 2016.    
- This is a pre-release feature that you must turn on for it to be available. For more information, see [Use pre-release features from updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease).

#### To manage Surface driver updates

1. Enable Synchronization for Microsoft Surface drivers. Use the procedure in [Configure classification and products](../../../sum/get-started/configure-classifications-and-products.md) and select the **Include Microsoft Surface drivers and firmware updates** checkbox on the **Classifications** tab to enable Surface drivers.
2. [Synchronize the Microsoft Surface drivers](../../../sum/get-started/synchronize-software-updates.md).
3. [Deploy synchronized Microsoft Surface drivers](../../../sum/deploy-use/deploy-software-updates.md)

### Configure Windows Update for Business deferral policies
<!-- 1290890 -->
You can now configure deferral policies for Windows 10 Feature Updates or Quality Updates for Windows 10 devices managed directly by Windows Update for Business. You can manage the deferral policies in the new **Windows Update for Business Policies** node under **Software Library** > **Windows 10 Servicing**.

For details, see [Integration with Windows Update for Business in Windows 10](../../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md#configure-windows-update-for-business-deferral-policies).

### Improved user notifications for Microsoft 365 updates
Improvements have been made to leverage the Office Click-to-Run user experience when a client installs a Microsoft 365 update. This includes pop-up and in-app notifications, and a countdown experience. For more information, see [Restart behavior and client notifications for Microsoft 365 updates](../../../sum/deploy-use/manage-office-365-proplus-updates.md)

## Reporting

### Use Windows Analytics with Configuration Manager
<!-- 1318608 -->
Windows Analytics is a set of solutions that allow you to form insight into the current state of your environment. Devices in your environment report Windows telemetry data. The data can be accessed through the Azure portal. In the case of Upgrade Readiness the data is directly available in the monitoring node of the Configuration Manager console.


<!-- ## Inventory  -->

## Mobile device management

### Updates to Android for Work sharing configuration
<!-- 1338403 -->
With this release, the values for the **Allow data sharing between work and personal profile** setting in the **Work Profile** setting group have been updated. We've also added a custom setting to block copy-paste between work and personal profiles.


### Android and iOS enrollment restrictions
<!-- 1290826 -->
With this release, you can now specify that users cannot enroll personal Android or iOS devices. New device restriction settings let you limit Android device enrollment to predeclared devices. For iOS devices, you can block enrollment of all devices except those enrolled with Apple's Device Enrollment Program, Apple Configurator, or the Intune device enrollment manager account.

## Protect devices

### Include trust for specific files and folders in a Device Guard policy
<!--1324676-->
In this release, we've added further capabilities to Device Guard policy management.

You can now optionally add trust for specific files for folders in a Device Guard policy. This lets you:

- Overcome issues with managed installer behaviors
- Trust line-of-business apps that cannot be deployed with Configuration Manager
- Trust apps that are included in an operating system deployment image

For more details, see [Device Guard management with Configuration Manager](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md).