---
title: "What&#39;s new in version 1606 of System Center Configuration Manager"
ms.custom: na
ms.date: 2016-08-02
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: df2e57b9-6445-4067-98e7-ace85d4e6aa6
caps.latest.revision: 40
author: Brenduns
---
# What&#39;s new in version 1606 of System Center Configuration Manager
Update 1606 for System Center Configuration Manager is an update that is available as an in-console update for previously installed sites that run version 1511 or 1602. Version 1511 is the initial baseline version you use to install new Configuration Manager sites.
> [!TIP]  
>  Learn more about:  
>   
>  -   [Installing new sites](https://technet.microsoft.com/library/mt590197.aspx) (using a baseline version like 1511)  
>  -   [Installing updates at sites](https://technet.microsoft.com/library/mt607046.aspx) (like update 1602 or 1606)  

 The following sections provide details about changes and new capabilities introduced in version 1606 of Configuration Manager.  



## <a name="updatesandservicing"></a>Updates and Servicing

### Changes for the Updates and Servicing Node
The following are changes to Updates and Servicing in the Configuration Manager console:
> [!NOTE]
> These changes are not available until after you install version 1606.

- **Node name change:**

    In the **Monitoring** workspace, the **Site Servicing status** node has been renamed to **Updates and Servicing Status**.
- **More installation status:**

    When you view the update installation status for a site, the console now displays separate details for the following actions:
    - **Download**  (This applies only to the top-tier site where the service connection point site system role is installed)
    - **Replication**
    - **Prerequisites Check**
    - **Installation**

  Additionally, there is now more detailed information for each step, including in which log file you can view for more information.  
-   **New option to retry prerequisite failures:**

    In both the **Administration** and **Monitoring** workspaces, the **Updates and Servicing** node includes a new button on the Ribbon named **Ignore prerequisite warnings**.

    When you install updates without using the option to Ignore prerequisite warnings (from within the Updates Wizard), and that update installation halts with a State of **Prereq warning**, you can then select **Ignore prerequisite warnings** from the ribbon to trigger an automatic continuation of that update install that ignores the prerequisite warnings.  



- **Cleaner view of updates:**

    When you view the **Updates and Servicing** node, you now see only the most recently installed update, and any new updates that are available for you to install. To view previously installed updates, you click the new **History** button which appears in the Ribbon.  

-   **Renamed option for pre-production:**

    In the Updates and Servicing node, the button what was named **Client options** is now renamed to **Promote Pre-production Client**.


###  Pre-release features
Beginning with 1606, you must give consent to use Pre-Release features in System Center Configuration Manager before you can select and enable their use. For more information, see [Use pre-release features from updates](../../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease).

### New distribution point update behavior
Update 1606 introduces changes that improve the availability of distribution points when installing future updates.

After update 1606 is installed, when you next install an update at that site that requires the automatic reinstallation of standard and pull-distribution point site system roles, all distribution points no longer go off-line to update at the same time. Instead, the site server uses the site’s content distribution settings to distribute the update to a subset of distribution points at a time. The result is that only some distribution points go off-line to install the update. This allows distribution points that have not yet begun to update or that have completed the update to remain on-line and able to provide content to clients.



## <a name="accessibility"></a> Accessibility
Beginning with version 1606, to navigate between the different nodes of a workspace, you can enter the first letter of a nodes name. Each key press moves the cursor to the next node that begins with that letter, and when using a screen reader, the reader reads out the name of that node. For more information about Accessibility options, see [Accessibility features in System Center Configuration Manager](../../../core/understand/accessibility-features.md).

## <a name="administration"></a>Administration
The following are changes to Administration in the Configuration Manager console:
### OMS Connector

You can now connect  Configuration Manager as collections from System Center Configuration Manager to the [Microsoft Operations Management Suite (OMS)](https://azure.microsoft.com/en-us/documentation/articles/operations-management-suite-overview/). This makes data such as collections from your Configuration Manager deployment visible in OMS. Find out more about [syncing data from Configuration Manager to the Microsoft Operations Management Suite here](../../../core/clients/manage/sync-data-microsoft-operations-management-suite.md).

The OMS Connector is a prerelease feature. To enable it, see [Use pre-release features from updates](../../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease).

### Support for cache size in Client Settings

You can now configure the size of the cache folder on client computers with Client Settings in the Configuration Manager console. Previously, you could only set the client cache size when installing or reinstalling the client software (using the SMSCACHESIZE property). Now you can specify the cache size as a client setting (either default or custom), and then have those settings applied with the next policy update on the client without requiring a client reinstall. For more information, [Configure the Client Cache for Configuration Manager Clients](../../../core/clients/manage/manage-clients.md#BKMK_ClientCache).

## On-premises Mobile Device Management

### Support for multiple device management points

On-premises Mobile Device Management (MDM) now supports a new capability in Windows 10 Anniversary Update that automatically configures an enrolled device to have more than one device management point available for use. This capability allows the device to fallback to another device management point when the one it normal uses is not available. This capability only works for PCs and devices with Windows 10 Anniversary Update installed.


## Application management

### Manage apps from the Windows Store for Business

The [Windows Store for Business](https://www.microsoft.com/business-store) is where you can find and purchase Windows apps for your organization, individually or in volume. By connecting the store to Configuration Manager, you can synchronize the list of apps you've purchased with Configuration Manager, view these in the Configuration Manager console, and deploy them like you would any other app.

For details, see [Manage apps from the Windows Store for Business with System Center Configuration Manager](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).

### Manage iOS volume-purchased apps

The work flow for managing volume-purchased iOS apps and deploying these with Configuration Manager has been improved.

For details, see [Manage volume-purchased iOS apps with System Center Configuration Manager](../../../apps/deploy-use/manage-volume-purchased-ios-apps.md).

### Software Center User Interface

The Software Center interface has been streamlined to make the end user experience easier to navigate.
*  The **Installation Status** and **Installed Software** tabs have been combined into a single **Installation Status** tab.
*  **Updates**, **Operating Systems** and **Applications** have been separated into three separate tabs.
* Multiple updates can now be selected for installation at once, or all updates can be installed at once by clicking the **Install All** button.

### Content status links
When viewing the properties of an application or package, there is now a link that takes you to the status for that object.

## Software updates

### Client setting to manage the Office 365 client agent
You can now use a Configuration Manager client setting to manage the Office 365 client agent. After you configure this setting and deploy Office 365 updates, the Configuration Manager client agent communicates with the Office 365 client agent to download Office 365 updates from a distribution point and install them.

For details, see [Manage Office 365 ProPlus updates with Configuration Manager](../../../sum/deploy-use/manage-office-365-proplus-updates.md).

### Manually switch clients to a new software update point
You can now enable the option for Configuration Manager clients to switch to a new software update point when there are issues with the active software update point. Once enabled, the clients will look for another software update point at the next scan.

For details, see [Plan for software updates in Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md#BKMK_ManuallySwitchSUPs).

### Restart options for Windows 10 clients after software update installation
When a software update that requires a restart is deployed using Configuration Manager and installed on a computer, a pending restart is scheduled and a restart dialog box is displayed. Beginning in Configuration Manager version 1606, the option to **Update and Restart**, and **Update and Shutdown** is available on Windows 10 computers in the Windows Power options whenever there is a pending restart for a Configuration Manager software update. After using one of these options, the restart dialog will not display after the computer restarts.

For details, see [Plan for software updates in System Center Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md#BKMK_RestartOptions).

## Operating system deployment

### Improvements to the Install Software Updates task sequence step
There is a new setting, **Evaluate software updates from cached scan results** that gives you the option to do a full scan for software updates instead of using the cached scan results. For details, see [Task sequence steps in System Center Configuration Manager](../../../osd/understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates).

Also, a new task sequence variable, **SMSTSSoftwareUpdateScanTimeout** is available to give you the ability to control the timeout for the software updates scan during the Install software updates task sequence step. The default value is 30 minutes. For details, see [Task sequence built-in variables in System Center Configuration Manager](../../../osd/understand/task-sequence-built-in-variables.md).

### OSDPreserveDriveLetter task sequence variable has been deprecated
Beginning in Configuration Manager version 1606, The OSDPreserveDriveLetter task sequence variable has been deprecated. Starting in Configuration Manager version 1606, Windows Setup determines the best drive letter to use (typically C:) during an operating system deployment, by default.

For details, see [Task sequence built-in variables in System Center Configuration Manager](../../../osd/understand/task-sequence-built-in-variables.md).

### Customize the RamDisk TFTP window size for PXE-enabled distribution points
You can now customize the RamDisk window size for PXE-enabled distribution points. If you have customized your network, it could cause the boot image download to fail with a time-out error because the window size is too large. The RamDisk TFTP window size customization allow you to optimize TFTP traffic when using PXE to meet your specific network requirements.

For details, see [Prepare site system roles for operating system deployments with System Center Configuration Manager](../../../osd/plan-design/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_RamDiskTFTP).

## Compliance settings

### Smart Lock setting for Android devices
A new setting, **Allow Smart Lock and other trust agents** has been added to the Android and Samsung KNOX configuration item.

This setting lets you control the Smart Lock feature on compatible Android devices. This phone capability, sometimes known as trust agents lets you disable or bypass the device lock screen password if the device is in a trusted location such as when it is connected to a specific Bluetooth device, or when it is near to an NFC tag. You can use this setting to prevent end users from configuring Smart Lock.

For details, see [How to create configuration items for Android and Samsung KNOX devices managed without the System Center Configuration Manager client](../../../compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client.md).

## Device configuration and protection

### Product name changes

* Microsoft Passport for Work is now known as **Windows Hello for Business**.
* Enterprise data protection is now known as **Windows Information Protection**.

The Configuration Manager console has been updated to reflect these changes.

### iOS Activation Lock
Configuration Manager can help you manage iOS Activation Lock, a feature of the Find My iPhone app for iOS 7.1 and later devices. When Activation Lock is enabled, the user's Apple ID and password must be entered before anyone can:
* Turn off Find My iPhone
* Erase the device
* Reactivate the device

Configuration Manager can help you manage Activation Lock in two ways:

1. Enable Activation Lock on supervised devices.
2. Bypass Activation Lock on supervised devices.

For details, see [Manage iOS Activation Lock with System Center Configuration Manager](../../../mdm/deploy-use/manage-ios-activation-lock.md)


### Windows Defender Advanced Threat Protection

Endpoint Protection can help manage and monitor Windows Defender Advanced Threat Protection (ATP). Windows Defender ATP is a new service that will help enterprises to detect, investigate, and respond to advanced attacks on their networks. Configuration Manager policies can help you onboard and monitor managed Windows 10, version 1607 (build 14328) or later.

For details, see [Windows Defender Advanced Threat Protection](../../../protect/deploy-use/windows-defender-advanced-threat-protection.md).

### Device categories
You can create device categories, which can be used to automatically place devices in device collections when you are using Configuration Manager with Microsoft Intune. Users are then required to choose a device category when they enroll a device in Intune. You can additionally change the category of a device from the Configuration Manager console.

For details, see [How to automatically categorize devices into collections with System Center Configuration Manager](../../../core/clients/manage/collections/automatically-categorize-devices-into-collections.md).

### Predeclare devices with IMEI or iOS serial numbers

You can identify corporate-owned devices by importing their international station mobile equipment identity (IMEI) numbers or iOS serial numbers. You can upload a comma-separated values (.csv) file containing device IMEI numbers or you can manually enter device information. Imported information will set **Ownership** of the devices that enroll as “**Corporate**” in lists of devices. An Intune license is still required for each user that accesses the service.

For more details, see [Predeclare devices with IMEI or iOS serial numbers](../../../mdm/deploy-use/predeclare-devices-with-imei-or-ios-serial-numbers.md).

### On-premises Health Attestation service communication

You can now enable Health Attestation services monitoring for Windows 10 PCs using only on-premises infrastructure so that computers without internet access can report Device Health Attestation (DHA).

For details, see [Health attestation for System Center Configuration Manager](../../../core/servers/manage/health-attestation.md#How-to-enable-Health-Attestation-service-communication-on-Configuration-Manager-client-computers).  

## Remote Control
Allow your end-users the opportunity to accept or deny file transfers before transferring content from the shared clipboard in a remote control session. End-users will only need to grant permission once per session, and the viewer will not have the ability to give themselves permission to proceed with the file transfer. You can find this new setting in the **Administration** workspace, then navigating to **Client Settings**, then opening the **Remote Tools** panel in **Default Settings**.
