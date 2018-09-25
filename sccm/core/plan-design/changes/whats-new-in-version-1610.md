---
title: "New version 1610"
titleSuffix: "Configuration Manager"
description: "Get details about changes and new capabilities introduced in version 1610 of System Center Configuration Manager."
ms.date: 11/23/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: f7eb0803-3f8f-4ab6-825a-99ac11f5ba7d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: "NOINDEX, NOFOLLOW"
---
# What&#39;s new in version 1610 of System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Update 1610 for System Center Configuration Manager current branch is available as an in-console update for previously installed sites that run version 1511, 1602, or 1606.


> [!TIP]  
> To install a new site, you must use a baseline version of Configuration Manager.  
>  Learn more about:    
>  -   [Installing new sites](https://technet.microsoft.com/library/mt590197.aspx)  
>  -   [Installing updates at sites](https://technet.microsoft.com/library/mt607046.aspx)  
>  -   [Baseline and update versions](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

The following sections provide details about changes and new capabilities introduced in version 1610 of Configuration Manager.  


## In-console monitoring of update installation status  
Beginning with version 1610, when you install an update pack and monitor the installation in the console, there is a new phase: **Post Installation**. This phase includes status for tasks like restarting key services, and initialization of replication monitoring. (This phase is not available in the console until after your site updates to version 1610.) For more information about update installation status, see [Install in-console updates](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkinstalla-install-in-console-updates).


## Exclude clients from automatic upgrade
You can exclude Windows clients from getting upgraded with new versions of the client software. To do this, you include the client computers in a collection that is specified to be excluded from upgrade. Clients in the excluded collection ignore requests to update the client software.  For more information, see [Exclude Windows clients from upgrades](../../clients/manage/upgrade/exclude-clients-windows.md).


## Improvements for boundary groups
Version 1610 introduces important changes to boundary groups and how they work with distribution points. These changes can simplify the design of your content infrastructure, while giving you more control over how and when clients fallback to search additional distribution points as content source locations. This includes both on-premises and cloud-based distribution points.
These improvements replace concepts and behaviors you might be familiar with (like configuring distribution points to be fast or slow). The new model should be easier to set up and maintain. These changes also lay the groundwork for future changes that will improve other site system roles you associate to boundary groups.

When you update to version 1610, the update converts your current boundary group configurations to fit the new model so that these changes do not disturb your existing content distribution configurations.

For more information, see [Boundary groups](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#a-namebkmkboundarygroupsa-boundary-groups).


## Peer Cache for content distribution to clients
Beginning with version 1610, client **Peer Cache** helps you manage deployment of content to clients in remote locations. Peer Cache is a built-in Configuration Manager solution for clients to share content with other clients, directly from their local cache.

After you deploy client settings that enable Peer Cache to a collection, members of that collection can act as a peer content source for other clients in the same boundary group.

You can also use the new **Client Data Sources** dashboard to understand the use of Peer Cache content sources in your environment.

> [!TIP]  
> With version 1610, Peer Cache and the Client Data Sources dashboard are pre-release features. To enable them, see [Use pre-release features from updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease).

For more information, see [Peer Cache for Configuration Manager clients](/sccm/core/plan-design/hierarchy/client-peer-cache), and [Client Data Sources dashboard](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard).


## Migrate multiple shared distribution points at the same time
You can now use the option to **Reassign Distribution Point** to have Configuration Manager process in parallel the reassignment of up to 50 shared distribution points at the same time. Prior to this release, reassigned distribution points were processed one at a time. For more information see, [Migrate multiple shared distribution points at the same time](/sccm/core/migration/planning-a-content-deployment-migration-strategy#migrate-multiple-shared-distribution-points-at-the-same-time).

## Cloud management gateway for managing Internet-based clients

Cloud management gateway provides a simple way to manage Configuration Manager clients on the Internet. The cloud management gateway service, which is deployed to Microsoft Azure and requires an Azure subscription, connects to your on-premises Configuration Manager infrastructure using a new role called the cloud management gateway connection point. Once it's completely deployed and configured, clients can communicate with on-premises Configuration Manager site system roles and cloud-based distribution points regardless of whether they're connected to the internal private network or on the Internet. For more information and to see how cloud management gateway compares with Internet-based client management, see [Manage clients on the Internet](/sccm/core/clients/manage/manage-clients-internet).

## Improvements to the Windows 10 Edition Upgrade Policy
In this release, the following improvements have been made to this policy type:

- You can now use the edition upgrade policy with Windows 10 PCs that run the Configuration Manager client in addition to Windows 10 PCs that are enrolled with Microsoft Intune.
- You can upgrade from Windows 10 Professional to any of the platforms in the wizard that are compatible with your hardware.

## Manage hardware identifiers
You can now provide a list of hardware IDs that Configuration Manager should ignore for the purpose of PXE boot and client registration. There are two common issues that this helps to address:

1. Many devices, like the Surface Pro 3, do not include an onboard Ethernet port. A USB-to-Ethernet adapter is generally used to establish a wired connection for the purpose of deploying an operating system. However, due to cost and general usability, these are often shared adapters. Because the MAC address of this adapter is used to identify the device, reusing the adapter becomes problematic without additional administrator actions between each deployment. Now in Configuration Manager version 1610, you can exclude the MAC address of this adapter so that it can easily be reused in this scenario.
2. The SMBIOS ID is supposed to be a unique hardware identifier, but some specialty hardware devices are built with duplicate IDs. This issue may not be as common as the USB-to-Ethernet adapter scenario just described, but you can address it by using the list of excluded hardware IDs.

For details, see [Manage duplicate hardware identifiers](/sccm/core/clients/manage/manage-clients#manage-duplicate-hardware-identifiers).

## Enhancements to Windows Store for Business integration with Configuration Manager
Changes in this release:
- Previously, you could only deploy free apps from the Windows Store for Business. Configuration Manager now additionally supports deploying paid online licensed apps (for Intune enrolled devices only).
- You can now initiate an immediate synchronization between the Windows Store for Business and Configuration Manager.
- You can now modify the client secret key that you obtained from Azure Active Directory.
- You can delete a subscription to the store.

For details, see [Manage apps from the Windows Store for Business with System Center Configuration Manager](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business).


## Policy sync for Intune-enrolled devices
You can now request a policy sync for an Intune-enrolled device from the Configuration Manager console, instead of needing to request a sync from the Company Portal app on the device itself. Sync request state information is available as a new column in device views, called **Remote Sync State**. The information is also available in the discovery data section of the **Properties** dialog for each device.
For details, see [Remotely synchronize policy on Intune-enrolled devices from the Configuration Manager console](/sccm/mdm/deploy-use/sync-intune-device).


## Use compliance settings to configure Windows Defender settings
You can now configure Windows Defender client settings on Intune-enrolled Windows 10 computers by using configuration items in the Configuration Manager console.
For details, see the **Windows Defender** section in [Create configuration items for Windows 8.1 and Windows 10 devices managed without the System Center Configuration Manager client](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client).



## General improvements to Software Center
- Users can now request apps from Software Center, as well as the Application Catalog.
- Improvements to help users understand what software is new and relevant.

## New columns in device collection views
You can now display columns for **IMEI** and **Serial Number** (for iOS devices) in device collection views.
For more details, see [Predeclare devices with IMEI or iOS serial numbers](https://docs.microsoft.com/sccm/mdm/deploy-use/predeclare-devices-with-hardware-id).

## Customizable branding for Software Center dialogs
Custom branding for the Software Center was introduced in Configuration Manager version 1602. In version 1610, that branding is now extended to all associated dialog boxes to provide a more consistent experience to Software Center users.

Custom branding for the Software Center is applied according to the following rules:

- If the Application Catalog website point site server role is not installed, then Software Center displays the organization name specified in the **Computer Agent** client setting **Organization name displayed in Software Center**. For instructions, see [How to configure client settings](../../clients/deploy/configure-client-settings.md).

- If the Application Catalog website point site server role is installed, then Software Center displays the organization name and color specified in the Application Catalog website point site server role properties. For more information, see [Configuration options for Application Catalog website point](/sccm/core/servers/deploy/configure/configuration-options-for-site-system-roles#Application-Catalog-website-point).

- If a Microsoft Intune subscription is configured and connected to the Configuration Manager environment, then Software Center displays the organization name, color, and company logo specified in the Intune subscription properties. For more information, see [Configuring the Microsoft Intune subscription](/sccm/mdm/deploy-use/setup-hybrid-mdm#step-3-configure-intune-subscription).


## Enforcement grace period for required application and software update deployments
In some cases, you might want to give users more time to install required application deployments or software updates beyond any deadlines you set up. For example, this might be necessary when a computer has been turned off for an extended period of time and it needs to install a large number of application or update deployments. For example, if an end user has just returned from vacation, they might have to wait for a long while as overdue application deployments are installed. To help solve this problem, you can now define an enforcement grace period by deploying Configuration Manager client settings to a collection. 

To configure the grace period, take the following actions:
1.      On the **Computer Agent** page of client settings, configure the new property **Grace period for enforcement after deployment deadline (hours)** with a value between **1** and **120** hours.
2.      In a new required application deployment, or in the properties of an existing deployment, on the **Scheduling** page, select the check box **Delay enforcement of this deployment according to user preferences, up to the grace period defined in client settings**. All deployments that have this check box selected, and are targeted to devices to which you also deployed the client setting, will use the enforcement grace period.

If you configure an enforcement grace period and select the checkbox, once the application install deadline is reached, it will be installed in the first non-business window that the user configured up to that grace period. However, the user can still open Software Center and install the application at any time they want. Once the grace period expires, enforcement reverts to normal behavior for overdue deployments. Similar options have been added to the software updates deployment wizard, automatic deployment rules wizard, and properties pages.



## Improved functionality in dialog boxes about required software
When a user receives required software, from the **Snooze and remind me:** setting, they can select from the following drop-down list of values: 
- **Later**. Specifies that notifications are scheduled based on the notification settings configured in Client Agent settings.
- **Fixed time**. Specifies that the notification will be scheduled to display again after the selected time (for example, in 30 minutes).

![Computer Agent page in Client Agent settings](media/client-notification-settings.png)

The maximum snooze time is based on notification values configured in the Client Agent settings. For example, if the **Deployment deadline greater than 24 hours, remind users every (hours)** setting on the Computer Agent page is configured for 10 hours, and it is more than 24 hours before the deadline, the user would see a set of snooze options up to but never greater than 10 hours. As the deadline approaches, fewer options are available, consistent with the relevant Client Agent settings for each component of the deployment timeline.

Additionally, for a high-risk deployment, such as a task sequence that deploys an operating system, the user notification experience is now more intrusive. Instead of a transient taskbar notification, each time the user is notified that critical software maintenance is required, a dialog box such as the following displays on the user's computer:

![Required Software dialog](media/client-toast-notification.png)


For more information:
- [Settings to manage high-risk deployments](../../../protect/understand/settings-to-manage-high-risk-deployments.md)
- [How to configure client settings](../../clients/deploy/configure-client-settings.md)

## Software updates dashboard
Use the new software updates dashboard to view the current compliance status of devices in your organization, and quickly analyze the data to see which devices are at risk. To view the dashboard, navigate to **Monitoring** > **Overview** > **Security** > **Software Updates Dashboard**.

For details, see [Monitor software updates](/sccm/sum/deploy-use/monitor-software-updates).


## Improvements to the application request process
After you have approved an application for installation, you can subsequently choose to deny the request by clicking **Deny** in the Configuration Manager console. Previously, this button was grayed out after approval.

This action does not cause the application to be uninstalled from any devices. However, it does stop users from installing new copies of the application from Software Center.

## Filter by content size in automatic deployment rules
You can now filter on the content size for software updates in automatic deployment rules. For example, to download only software updates that are smaller than 2 MB, you can set the **Content Size (KB)** filter to **< 2048**. Using this filter prevents large software updates from automatically downloading, which better supports simplified Windows down-level servicing when network bandwidth is limited. For details, see:
- [Configuration Manager and Simplified Windows Servicing on Down Level Operating Systems](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/07/configuration-manager-and-simplified-windows-servicing-on-down-level-operating-systems/)
- [Automatically deploy software updates](/sccm/sum/deploy-use/automatically-deploy-software-updates)

To configure the **Content Size (KB)** field, do one of the following:
- When you create an automatic deployment rule, in the Create Automatic Deployment Rule wizard, go to the **Software Updates** page.
- In the properties for an existing automatic deployment rule, go to the **Software Updates** tab.

## Office 365 Client Management dashboard
The Office 365 Client Management dashboard is now available in the Configuration Manager console. To view the dashboard, go to **Software Library** > **Overview** > **Office 365 Client Management**.

The dashboard displays charts for the following:

- Number of Office 365 clients
- Office 365 client versions
- Office 365 client languages
- Office 365 client channels     

For details, see [Manage Office 365 ProPlus updates](/sccm/sum/deploy-use/manage-office-365-proplus-updates).

## Task sequence steps to manage BIOS to UEFI conversion
You can now customize an operating system deployment task sequence with a new variable, TSUEFIDrive, so that the **Restart Computer** step will prepare a FAT32 partition on the hard drive for transition to UEFI. The following procedure provides an example of how you can create task sequence steps to prepare the hard drive for the BIOS to UEFI conversion. For details, see  [Task sequence steps to manage BIOS to UEFI conversion](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion).

##  Improvements to the task sequence step: Prepare ConfigMgr Client for Capture  
The Prepare ConfigMgr Client step will now completely remove the Configuration Manager client, instead of only removing key information. When the task sequence deploys the captured operating system image, it will install a new Configuration Manager client each time. For details, see [Task sequence steps](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture).



## Intune compliance policy charts
You can now get a quick view of overall compliance for devices, and the top reasons for non-compliance, by using new charts under the **Monitoring** workspace in the Configuration Manager console. You can click a section in the chart to drill down to a list of the devices in that category. For details, see [Monitor the compliance policy](/sccm/protect/deploy-use/create-compliance-policy#monitor-the-compliance-policy).


## Lookout integration for hybrid implementations to protect iOS and Android devices
Microsoft is integrating with Lookout’s mobile threat protection solution to protect iOS and Android mobile devices by detecting malware, risky apps, and more, on devices. Lookout’s solution helps you determine the threat level, which is configurable. You can create a compliance policy rule in System Center Configuration Manager to determine device compliance based on the risk assessment by Lookout. Using conditional access policies, you can allow or block access to company resources based on the device compliance status. To learn about the integration and how it works, see [Manage access based on device, network, and application risk](/sccm/protect/deploy-use/manage-access-based-on-device-network-app-risk).

Users of noncompliant iOS devices will be prompted to enroll. They'll be required to install the Lookout for Work app on their devices, activate the app, and remediate threats reported in the Lookout for Work application to gain access to company data. Learn how to [Configure and deploy Lookout for Work apps](/sccm/protect/deploy-use/configure-and-deploy-lookout-for-work-apps).



## New compliance settings for configuration items
There are many new settings you can use in your configuration items for various device platforms. These are settings that previously existed in Microsoft Intune in a standalone configuration, and are now available when you use Intune with Configuration Manager.
For details, see [Configuration items for devices managed without the System Center Configuration Manager client](/sccm/compliance/deploy-use/configuration-items-for-devices-managed-without-the-client).

### New settings for Android devices
#### Password settings
- **Remember password history**
- **Allow fingerprint unlock**

#### Security settings
- **Require encryption on storage cards**
- **Allow screen capture**
- **Allow diagnostic data submission**

#### Browser settings
- **Allow web browser**
- **Allow autofill**
- **Allow pop-up blocker**
- **Allow cookies**
- **Allow active scripting**

#### App settings
- **Allow Google Play store**

#### Device capability settings
- **Allow removable storage**
- **Allow Wi-Fi tethering**
- **Allow geolocation**
- **Allow NFC**
- **Allow Bluetooth**
- **Allow voice roaming**
- **Allow data roaming**
- **Allow SMS/MMS messaging**
- **Allow voice assistant**
- **Allow voice dialing**
- **Allow copy and paste**

### New settings for iOS devices
#### Password settings
- **Number of complex characters required in password**
- **Allow simple passwords**
- **Minutes of inactivity before password is required**
- **Remember password history**

### New settings for Mac OS X devices
#### Password settings
- **Number of complex characters required in password**
- **Allow simple passwords**
- **Remember password history**
- **Minutes of inactivity before screensaver activates**

### New settings for Windows 10 Desktop and Mobile devices
#### Password settings
- **Minimum number of character sets**
- **Remember password history**
- **Require a password when the device returns from an idle state**

#### Security settings
- **Require encryption on mobile device**
- **Allow manual unenrollment**

#### Device capability settings
- **Allow VPN over cellular**
- **Allow VPN roaming over cellular**
- **Allow phone reset**
- **Allow USB connection**
- **Allow Cortana**
- **Allow action center notifications**

### New settings for Windows 10 Team devices
#### Device settings
- **Enable Azure Operational Insights**
- **Enable Miracast wireless projection**
- **Choose the meeting information displayed on the welcome screen**
- **Lockscreen background image URL**

### New settings for Windows 8.1 devices
#### Applicability settings
- **Apply all configurations to Windows 10**

#### Password settings
- **Required password type**
- **Minimum number of character sets**
- **Minimum password length**
- **Number of repeated sign-in failures to allow before the device is wiped**
- **Minutes of inactivity before screen turns off**
- **Password expiration (days)**
- **Remember password history**
- **Prevent reuse of previous passwords**
- **Allow picture password and PIN**

#### Browser settings
- **Allow automatic detection of intranet network**

### New settings for Windows Phone 8.1 devices
#### Applicability settings
- **Apply all configurations to Windows 10**

#### Password settings
- **Minimum number of character sets**
- **Allow simple passwords**
- **Remember password history**

#### Device capability settings
- **Allow automatic connection to free Wi-Fi hotspots**
