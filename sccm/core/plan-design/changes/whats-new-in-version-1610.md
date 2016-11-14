---
title: "New in 1610 | System Center Configuration Manager"
description: "Get details about changes and new capabilities introduced in version 1610 of System Center Configuration Manager."
ms.custom: na
ms.date:  
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f7eb0803-3f8f-4ab6-825a-99ac11f5ba7d
caps.latest.revision: 40
author: Brendunsms.author: brendunsmanager: angrobe
ROBOTS: "NOINDEX, NOFOLLOW"
---
# What&#39;s new in version 1610 of System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
Update 1610 for System Center Configuration Manager current branch is an update that is available as an in-console update for previously installed sites that run version 1511, 1602, or 1606. Version 1511 is the initial baseline version you use to install new Configuration Manager sites.
> [!TIP]  
>  Learn more about:  
>   
>  -   [Installing new sites](https://technet.microsoft.com/library/mt590197.aspx) (using a baseline version like 1511)  
>  -   [Installing updates at sites](https://technet.microsoft.com/library/mt607046.aspx) (like update 1602 or 1606)  

The following sections provide details about changes and new capabilities introduced in version 1610 of Configuration Manager.  


## In-console monitoring of update installation status
Beginning with version 1610, when you install an update pack and monitor the installation in the console, there is a new phase: **Post Installation**. This phase includes status for tasks like restarting key services, and initialization of replication monitoring. (This phase is not available in the console until after your site updates to version 1610.) For more information about update installation status, see [Install in-console updates](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkinstalla-install-in-console-updates).


## Exclude clients from automatic upgrade
You can exclude Windows clients from getting upgraded with new versions of the client software. To do this, you include the client computers in a collection that is specified to be excluded from upgrade. Client in the excluded collection ignore requests to update the client software.  For more information, see [Exclude Windows clients from upgrades](../../clients/manage/upgrade/exclude-clients-windows.md).


## Improvements for boundary groups
Version 1610 introduces important changes to boundary groups and how they work with distribution points. These changes can simplify the design of your content infrastructure while giving you more control over how and when clients fallback to search additional distribution points as content source locations. This includes both on-premises and cloud-based distribution points.
These improvements replace concepts and behaviors you might be familiar with today (like configuring distribution points to be fast or slow) and replaces them with a new model that should be easier to setup and maintain. These changes are also groundwork for future changes that will improve other site system roles you associate to boundary groups.

When you update to version 1610, the update converts your current boundary group configurations to fit the new model so that these changes do not disturb your existing content distribution configurations.

For more information, see [Boundary groups](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#a-namebkmkboundarygroupsa-boundary-groups).


## Peer Cache for content distribution to clients
Beginning with version 1610, client **Peer Cache** helps you manage deployment of content to clients in remote locations. Peer Cache is a built-in Configuration Manager solution for clients to share content with other clients directly from their local cache.

After you deploy client settings that enable Peer Cache to a collection, members of that collection can act as a peer content source for other clients in the same boundary group.

You can also use the new **Client Data Sources** dashboard to understand the use of Peer Cache content sources in your environment.

> [!TIP]  
> With version 1610, Peer Cache and the Client Data Sources dashboard are pre-release features. To enable them, see [Use pre-release features from updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease).

For more information see [Peer Cache for Configuration Manager clients](/sccm/core/plan-design/hierarchy/client-peer-cache), and [Client Data Sources dashboard](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard).


## Migrate multiple shared distribution points at the same time
You can now use the option to **Reassign Distribution Point** to have Configuration Manager process in parallel the reassignment of up to 50 shared distribution points at the same time. Prior to this release, reassigned distribution points were processed one at a time. For more information see, [Migrate multiple shared distribution points at the same time](/sccm/core/migration/planning-a-content-deployment-migration-strategy#migrate-multiple-shared-distribution-points-at-the-same-time).


## Improvements to the Windows 10 Edition Upgrade Policy
In this release, the following improvements have been made to this policy type:

- You can now use the edition upgrade policy with Windows 10 PCs that run the Configuration Manager client in addition to Windows 10 PCs are enrolled with Microsoft Intune.
- You can upgrade from Windows 10 Professional to any of the platforms in the wizard that are compatible with your hardware.


## Enhancements to Windows Store for Business integration with Configuration Manager
Changes in this release:
- Previously, you could only deploy free apps from the Windows Store for Business. Configuration Manager now additionally supports deploying paid online licensed apps (for Intune enrolled devices only).
- You can now initiate an immediate synchronization between the Windows Store for Business and Configuration Manager.
- You can now modify the client secret key that you obtained from Azure Active Directory
- You can delete a subscription to the store

For details, see [Manage apps from the Windows Store for Business with System Center Configuration Manager](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)


## Policy sync for Intune-enrolled devices
You can now request a policy sync for an Intune-enrolled device from the Configuration Manager console instead of needing to request a sync from the Company Portal app on the device itself. Sync request state information is available as a new column in device views, called **Remote Sync State**, as well as in the discovery data section of the **Properties** dialog for each device.
For details, see [Remotely synchronize policy on Intune-enrolled devices from the Configuration Manager console](/sccm/mdm/deploy-use/sync-intune-device)


## Use compliance settings to configure Windows Defender settings
You can now configure Windows Defender client settings on Intune-enrolled Windows 10 computers using configuration items in the Configuration Manager console.
For details, see the **Windows Defender** section in [Create configuration items for Windows 8.1 and Windows 10 devices managed without the System Center Configuration Manager client](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client)



## General improvements to Software Center
- Users can now request apps from Software Center, as well as the Application Catalog.
- Improvements to help users understand what software is new and relevant.


## Customizable Branding for Software Center Dialogs
Custom branding for the Software Center was introduced in Configuration Manager version 1602. In version 1610, that branding is now extended to all associated dialog boxes to provide a more consistent experience to Software Center users.

Custom branding for the Software Center is applied according to the following rules:

1. If the Application Catalog website point site server role is not installed, then Software Center will display the organization name specified in the **Computer Agent** client setting **Organization name displayed in Software Center**. For instructions, see [How to configure client settings](../../core/clients/deploy/configure-client-settings.md).

2. If the Application Catalog website point site server role is installed, then Software Center will display the organization name and color specified in the Application Catalog website point site server role properties. For more information, see [Configuration options for Application Catalog website point](../../core/servers/deploy/configure/configuration-options-for-site-system-roles.md#Application-Catalog-website-point).

3. If a Microsoft Intune subscription is configured and connected to the Configuration Manager environment, then Software Center will display the organization name, color and company logo specified in the Intune subscription properties. For more information, see [Configuring the Microsoft Intune subscription](../../mdm/deploy-use/setup-hybrid-mdm.md#step-3-configure-intune-subscription).


## Enforcement grace period for required application and software update deployments
In some cases, you might want to give users more time to install required application deployments or software updates beyond any deadlines you configured. This might typically be required when a computer has been turned off for an extended period of time and needs to install a large number of application or update deployments. For example, if an end user has just returned from vacation, they might have to wait for a long while as overdue application deployments are installed. To help solve this problem, you can now define an enforcement grace period by deploying Configuration Manager client settings to a collection.

To configure the grace period, take the following actions:
1.      On the **Computer Agent** page of client settings, configure the new property **Grace period for enforcement after deployment deadline (hours)** with a value between **1** and **120** hours.
2.      In a new required application deployment, or in the properties of an existing deployment, on the **Scheduling** page, select the checkbox **Delay enforcement of this deployment according to user preferences, up to the grace period defined in client settings**. All deployments that have this check-box selected and are targeted to devices to which you also deployed the client setting will use the enforcement grace period.

If you configure an enforcement grace period and select the checkbox, once the application install deadline is reached, it will be installed in the first non-business window that the user configured up to that grace period. However, the user can still open Software Center and install the application at any time they want. Once the grace period expires, enforcement reverts to normal behavior for overdue deployments. Similar options have been added to the software updates deployment wizard, automatic deployment rules wizard, and properties pages.



## Improved functionality for required software dialogs
When a user receives required software, from the **Snooze and remind me:** setting, they can select from the following drop-down list of values:
- Later: specifies that notifications are scheduled based on the notification settings configured in Client Agent settings.
- Fixed time: specifies that the notification will be scheduled to display again after the selected time. For example, if a user selects 30 minutes, the notification will display again in 30 minutes.

![Computer Agent page in Client Agent settings](media/client-notification-settings.png)

The maximum snooze time is always based on the notification values configured in the Client Agent settings at every time along the deployment timeline. For example, if the **Deployment deadline greater than 24 hours, remind users every (hours)** setting on the Computer Agent page is configured for 10 hours, and it is more than 24 hours before the deadline when the dialog is launched, the user would be presented with a set of snooze options up to but never greater than 10 hours. As the deadline approaches, the dialog will show fewer options, consistent with the relevant Client Agent settings for each component of the deployment timeline.

Additionally, for a high-risk deployment, such as a task sequence that deploys an operating system, the end-user notification experience is now more intrusive. Instead of a transient taskbar notification, each time the user is notified that critical software maintenance is required, a dialog box such as the following displays on the user's computer:

![Required Software dialog](media/client-toast-notification.png)


For more information:
- [Settings to manage high-risk deployments](../../protect/understand/settings-to-manage-high-risk-deployments.md)
- [How to configure client settings](../clients/deploy/configure-client-settings.md)


## Improvements to the application request process
After you have approved an application for installation, you can subsequently choose to deny the request by clicking **Deny** in the Configuration Manager console (previously this button was grayed out after approval).
This action does not cause the application to be uninstalled from any devices. However, it does stop users from installing new copies of the application from Software Center.


## New compliance settings for configuration items
We've added many new settings you can use in your configuration items for various device platforms. These are settings that previously existed in Microsoft Intune in a standalone configuration, and are now available when you use Intune with Configuration Manager.
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
