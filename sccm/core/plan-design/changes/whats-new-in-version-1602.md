---
title: "New in version 1602"
titleSuffix: "Configuration Manager"
description: "Get details about changes and new capabilities introduced in version 1602 of System Center Configuration Manager."
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 4021eca1-adfb-4e5a-adee-159263c29637
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: noindex,nofollow
---
# What&#39;s new in version 1602 of System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*


Update 1602 for System Center Configuration Manager is only available as an in-console update for previously installed sites that run version 1511. Version 1511 is the initial, baseline version you use to install new Configuration Manager sites.  


> [!TIP]  
>  Learn more about:  
>   
>   -   [Installing new sites](/sccm/core/servers/deploy/install) (using a baseline version like 1511)  
>   -   [Installing updates at sites](/sccm/core/servers/manage/updates) (like update 1602)  

 The following sections provide details about changes and new capabilities introduced in version 1602 of Configuration Manager.  

## Site infrastructure  

###  <a name="bkmk_UpgradeOS"></a> In-place upgrade the operating system of site servers that run Windows Server 2008 R2  
 Configuration Manager sites that run version 1602 or later support the in-place upgrade of the site servers operating system from Windows Server 2008 R2 to Windows Server 2012 R2.  

> [!WARNING]  
>  Before you upgrade to Windows Server 2012 R2, you must uninstall WSUS 3.2 from the server.  
>   
>  For information about this critical step, see the "New and changed functionality" section in [Windows Server Update Services Overview](https://technet.microsoft.com/library/hh852345.aspx), in the Windows Server documentation.  

 To upgrade a server, use the Windows Server 2012 R2 upgrade procedures. You do not need to run a Configuration Manager site server restore after the upgrade. For upgrade procedures, see [Upgrade Options for Windows Server 2012 R2](https://technet.microsoft.com/library/dn303416.aspx) in the Windows Server documentation.  

###  <a name="bkmk_AOAG"></a> SQL Server AlwaysOn availability groups  
 Use SQL Server AlwaysOn availability groups to host the site database at primary sites, and the central administration site as a high-availability and disaster-recovery solution.  

 For details, see [SQL Server AlwaysOn for a highly available site database for System Center Configuration Manager](../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).  

## Operating system deployment  

### Windows 10 servicing  
 The following improvements for Windows 10 servicing were added in Configuration Manager version 1602:  

-   New filter options are available for servicing plans that allow you to filter for **Language**, **Required**, and **Title**. Only upgrades that meet the specified criteria will be added to the associated deployment.  

-   When you select the **Upgrades** classification for software updates synchronization, a warning is displayed. This warning lets you know that [hotfix 3095113](https://support.microsoft.com/kb/3095113) for Windows Server Update Services (WSUS) 4.0 is required before you can successfully synchronize software updates, and for the Windows 10 Servicing to work properly. From the warning message, you can go to the associated knowledge base article.  

-   Available Windows 10 upgrades now only display in the **Windows 10 Servicing** \ **All Windows 10 Updates** node of the Configuration Manager console. These updates no longer display in the **Software Updates** \ **All Software Updates** node of the console.  

-   A servicing plan is considered a high-risk deployment, and the **Select Collection** window displays only the custom collections that meet the deployment verification settings that are configured in the site’s properties. For more information, see [Settings to manage high-risk deployments for System Center Configuration Manager](../../../protect/understand/settings-to-manage-high-risk-deployments.md).  

-   Users who start a Windows 10 Upgrade package now receive a message that they will be upgrading their operating system.  

## Application management  

### iOS app configuration policies  
 Use Configuration Manager app configuration policies to supply settings that might be required when the user runs an iOS app. For example, an app might require the user to specify a custom port number, language, security settings, or branding settings (such as a company logo). If these settings are incorrectly entered, this can increase the burden on your help desk, and also slow the adoption of new apps.  

 App configuration policies can help you eliminate these problems by letting you deploy these settings to users in a policy, before they run the app. The settings are then supplied automatically, and the user doesn't need to take any action. For details, see [Configure iOS apps with app configuration policies in System Center Configuration Manager](../../../apps/deploy-use/configure-ios-apps-with-app-configuration-policies.md).  

### Manage volume-purchased iOS apps  
 Configuration Manager can help you deploy and manage apps you purchased in volume from the Apple Volume-Purchase Program (VPP). Configuration Manager imports the license information from the app store, and tracks how many of the licenses you have used.  

 For details, see [Manage volume-purchased iOS apps with System Center Configuration Manager](../../../apps/deploy-use/manage-volume-purchased-ios-apps.md).  

### Automatic creation of Office mobile apps  
 When you update to version 1602 from 1511, Configuration Manager automatically creates the following Microsoft Office mobile apps for Android and iOS:  

-   Microsoft Word  

-   Microsoft Excel  

-   Microsoft PowerPoint  

-   Microsoft OneDrive  

-   Microsoft OneNote (iOS only)  

-   Microsoft Outlook  

You will find these apps in the **Applications** node of the Configuration Manager console.  

 For more information about deploying applications, see [How to deploy applications with System Center Configuration Manager](../../../apps/deploy-use/deploy-applications.md).  

## Software updates  

### Manage Office 365 client updates  
 System Center Configuration Manager has the ability to manage Office 365 client updates by using the software update management workflow. For more information, see [Manage Office 365 ProPlus updates with System Center Configuration Manager](/sccm/sum/deploy-use/manage-office-365-proplus-updates).  

## Compliance settings  

### Compliance settings for devices running Windows 10 Team  
 New settings have been added to the **Windows 8.1 and Windows 10** configuration item. These settings help you control devices running Windows 10 Team, such as a Surface Hub device.  

 For details, see [How to create configuration items for Windows 8.1 and Windows 10 devices managed without the System Center Configuration Manager client](../../../compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).  

### Kiosk mode settings for Android Samsung KNOX Standard devices  
 Kiosk mode allows you to lock a device so that only certain features work. For example, you can allow a device to run only one managed app that you specify, or you can disable the volume buttons on a device. These settings might be used for a demonstration model of a device, or a device that is dedicated to performing only one function, such as a point-of-sale device. In Configuration Manager, you can now specify kiosk mode settings for Samsung KNOX Standard devices.  

 For details, see [How to create configuration items for Android and Samsung KNOX Standard devices managed without the System Center Configuration Manager client](../../../compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client.md).  

## Conditional access  

### Conditional access for PCs managed by System Center Configuration Manager  
 Previous to this release, to set up conditional access for a PC, the PC either had to be enrolled in Intune or had to be a domain-joined PC. Beginning with the 1602 update, conditional access for PCs managed by System Center Configuration manager is supported. For your PCs that are managed by System Center Configuration Manager, you can restrict access to Exchange Online and SharePoint Online only to devices that are compliant with the compliance policies you set.  

 For details, see [Manage access to O365 services for PCs managed by System Center Configuration Manager](../../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md).  

### Restricting access based on the health of devices  
 You can now restrict access to email and 0ffice 365 services based on the health of the devices, as reported by the Health Attestation Service. Additionally, devices managed by Intune are included in the device health reports.  

 The Configuration Manager console features a new compliance rule that allows you to specify if the devices should be allowed or blocked access based on their health status. For details about Health Attestation Service and how the health of devices is reported in Intune, see [Health attestation for System Center Configuration Manager](../../../core/servers/manage/health-attestation.md).  

### New compliance policy rules  
 New compliance policy rules, like automatic updates and requiring a password to unlock devices, have been added to support better security requirements.

 For more details, see [Device compliance policies in System Center Configuration Manager](../../../protect/deploy-use/device-compliance-policies.md).  

### Make sure enrolled and compliant devices always have access to Exchange on-premises  
 When you check the following option, devices that are enrolled in Intune, and compliant with the compliance policies, are allowed to access Exchange on-premises: **Default rule override - Always allow Intune enrolled and compliant devices to access Exchange on-premises:**. This rule is available on the  **General page** of the **Configure Conditional Access Policy Wizard** for Exchange on-premises.

 This rule overrides the default rule, which means that even if you set the default rule to quarantine or block access, enrolled and compliant devices will still be able to access Exchange on-premises. Use this setting when you want enrolled and compliant devices to always have access to email through Exchange on-premises.   

 For the detailed walkthrough, see [Manage email access in System Center Configuration Manager](../../../protect/deploy-use/manage-email-access.md).  

## Client management  

### Client online status  
 A new  status for clients is available for monitoring if a computer is online or not. A computer is considered online if it's connected to its assigned management point. To indicate that the computer is online, the client sends ping-like messages to the management point. If the management point doesn't receive a message after 5 minutes, the client is considered offline.  

 For details, see [How to monitor clients in System Center Configuration Manager](../../../core/clients/manage/monitor-clients.md).  

### Refresh PC machine and user policy from Software Center  
 A new option, **Sync Policy**, has been added to the **Options** > **Computer Maintenance** page of Software Center that causes the PC to refresh its Configuration Manager machine and user policy.  

### Software Center branding changes  
 You can change the color, organization name, and icon that appear in Software Center. These settings are applied according to the following rules:  

- If the Application Catalog website point site server role is not installed, then Software Center displays the organization name specified in the **Computer Agent** client setting called **Organization name displayed in Software Center**.  

- If the Application Catalog website point site server role is installed, then Software Center displays the organization name and color specified in properties of the Application Catalog website point site server role.  

- If a Microsoft Intune subscription is configured and connected to the Configuration Manager environment, then Software Center displays the organization name, color, and company logo specified in the Intune subscription properties.  

### Health Attestation  
 Administrators can view the status of Windows 10 Device Health Attestation in the Configuration Manager console. This is available for Configuration Manager, as well as Configuration Manager with Microsoft Intune. Device health attestation lets the administrator ensure that client computers have the following trustworthy BIOS, TPM, and boot software configurations enabled:  

-   Early-launch antimalware  

-   BitLocker  

-   Secure Boot  

-   Code Integrity  

For details, see [Health attestation for System Center Configuration Manager](../../../core/servers/manage/health-attestation.md).  

### Improvements to Endpoint Protection antimalware settings  
 1602 adds the following new settings in Endpoint Protection antimalware policy for Windows Defender:  

-   Real-time protection: Block potentially unwanted applications at download, prior to installation.  

-   Scan settings: Scan mapped network drives during a full scan.  

-   Automatic sample file submission settings:  

     The antimalware engine may request file samples to be sent to Microsoft for further analysis. By default, it will always prompt before it sends such samples. Administrators can now manage the following settings to configure this behavior:  

    -   Advanced: Enable automatic sample file submission to help Microsoft determine whether certain detected items are malicious.  

    -   Advanced: Allow users to modify automatic sample file submission settings.  

    Additionally, in the “Exclusion settings” section of endpoint protection antimalware policy, the existing **Exclude files and folders** setting now allows device exclusions.  

For details, see [How to create and deploy antimalware policies for Endpoint Protection in System Center Configuration Manager](../../../protect/deploy-use/endpoint-antimalware-policies.md).  

## Mobile device management  

### iOS Activation Lock  
 Configuration Manager can help you manage iOS Activation Lock, a feature of the Find My iPhone app for iOS 7.1 and later devices. Activation Lock is enabled automatically when the Find My iPhone app is used on a device. After it is enabled, the user's Apple ID and password must be entered before anyone can:  

-   Turn off Find My iPhone.  

-   Erase the device.  

-   Reactivate the device.  

Configuration Manager can request the Activation Lock status of both supervised and unsupervised devices that run iOS 7.1 and later. For supervised devices, Configuration Manager can retrieve the Activation Lock bypass code and directly issue it to the device.  

 For details, see [Help protect iOS devices with Activation Lock bypass in System Center Configuration Manager](/sccm/mdm/deploy-use/manage-ios-activation-lock).  

### Monitor terms and conditions deployments  
 You can monitor terms and conditions deployments in the Configuration Manager console.  

 Select the terms and conditions deployment from the list of deployments. The summary area shows the following statistics:  

-   **Compliant**: Users have accepted the latest version of the terms and conditions.  

-   **Error**  

-   **Noncompliant**: Users have accepted a version of the terms and conditions, but not the latest version.  

-   **Unknown**: Users have never accepted the terms and conditions, including those without an enrolled device.  
