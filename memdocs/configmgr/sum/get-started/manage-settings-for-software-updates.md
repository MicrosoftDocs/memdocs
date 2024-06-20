---
title: Manage settings for software updates
titleSuffix: Configuration Manager
description: Learn about the client settings that are appropriate for software updates at your site after you install the software update point.
ms.date: 11/30/2020
ms.topic: conceptual
ms.service: configuration-manager
ms.subservice: software-updates
manager: apoorvseth
author: BalaDelli
ms.author: baladell
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

#  <a name="BKMK_ManageSUSettings"></a> Manage settings for software updates  

*Applies to: Configuration Manager (current branch)*

After you synchronize software updates in Configuration Manager, configure and verify the settings in the following sections.

##  <a name="BKMK_ClientSettings"></a> Client settings for software updates  
After you install the software update point, software updates is enabled on clients by default, and the settings on the **Software Updates** page in client settings have default values. The client settings are used site-wide and affect when software updates are scanned for compliance, and how and when software updates are installed on client computers. Before you deploy software updates, verify that the client settings are appropriate for software updates at your site.  

> [!IMPORTANT]  
> - The **Enable software updates on clients** setting is enabled by default. If you clear this setting, Configuration Manager removes the existing deployment policies from the client.
>
> - Beginning with the September 2020 cumulative update, HTTP-based WSUS servers will be secure by default. A client scanning for updates against an HTTP-based WSUS will no longer be allowed to leverage a user proxy by default. If you still require a user proxy despite the security trade-offs, a new [software updates client setting](../../core/clients/deploy/about-client-settings.md#software-updates) is available to allow these connections. For more information about the changes for scanning WSUS, see [September 2020 changes to improve security for Windows devices scanning WSUS](https://go.microsoft.com/fwlink/?linkid=2144403). To ensure that the best security protocols are in place, we highly recommend that you use the TLS/SSL protocol to help [secure your software update infrastructure](../get-started/software-update-point-ssl.md). 

For information about how to configure client settings, see [How to configure client settings](../../core/clients/deploy/configure-client-settings.md).  

For more information about the client settings, see [About client settings](../../core/clients/deploy/about-client-settings.md). 


##  <a name="BKMK_GroupPolicy"></a> Group policy settings for software updates  
There are specific group policy settings that are used by Windows Update Agent (WUA) on client computers to connect to WSUS that runs on the software updates point. These group policy settings are also used to successfully scan for software update compliance, and to automatically update the software updates and the WUA.

### Specify Intranet Microsoft Update Service Location local policy  
When the software update point is created for a site, clients receive a machine policy that provides the software update point server name and configures the **Specify intranet Microsoft update service location** local policy on the computer. The WUA retrieves the server name that is specified in the **Set the intranet update service for detecting updates** setting, and then it connects to this server when it scans for software updates compliance. When a domain policy is created for the **Specify intranet Microsoft update service location** setting, it overrides the local policy, and the WUA might connect to a server other than the software update point. If this happens, the client might scan for software update compliance based on different products, classifications, and languages. Therefore, you should not configure the Active Directory policy for client computers.  

### Allow Signed Content from Intranet Microsoft Update Service Location group policy  
You must enable the **Allow signed content from intranet Microsoft update service location** Group Policy setting before the WUA on computers will scan for software updates that were created and published with System Center Updates Publisher. When the policy setting is enabled, WUA will accept software updates that are received through an intranet location if the software updates are signed in the **Trusted Publishers** certificate store on the local computer. For more information about the Group Policy settings that are required for Updates Publisher, see [Updates Publisher 2011 Documentation Library](/previous-versions/system-center/updates-publisher-2011/hh134742(v=technet.10)).  

### Automatic updates configuration  
Automatic Updates allows security updates and other important downloads to be received on client computers. Automatic Updates is configured through the **Configure Automatic Updates** Group Policy setting or through the Control Panel on the local computer. When Automatic Updates is enabled, client computers will receive update notifications and, depending on the configured settings, the client computers will download and install the required updates. When Automatic Updates coexists with software updates, each client computer might display notification icons and popup display notifications for the same update. Also, when a restart is required, each client computer might display a restart dialog box for the same update.  

### Self Update  
When Automatic Updates is enabled on client computers, the WUA automatically performs a self-update when a newer version becomes available or when there are problems with a WUA component. When Automatic Updates is not configured or is disabled, and client computers have an earlier version of the WUA, the client computers must run the WUA installation file.  

## Software updates properties
The software update properties provide information about software updates and associated content. You can also use these properties to configure settings for software updates. When you open the properties for multiple software updates, only the **Maximum Run Time** and **Custom Severity** tabs are displayed.   

Use the following procedure to open software update properties.  

#### To open software update properties  

1. In the Configuration Manager console, click **Software Library**.  
2. In the Software Library workspace, expand **Software Updates**, and click **All Software Updates**.  
3. Select one or more software updates, and then, on the **Home** tab, click **Properties** in the **Properties** group.  

   > [!NOTE]  
   >  On the **All Software Updates** node, Configuration Manager displays only the software updates that have a **Critical** and **Security** classification and that have been released in the last 30 days.  

###  <a name="BKMK_SoftwareUpdatesInformation"></a> Review software updates information  
In software update properties, you can review detailed information about a software update. The detailed information is not displayed when you select more than one software update. The following sections describe the information that is available for a selected software update.  

####  <a name="BKMK_SoftwareUpdateDetails"></a> Software update details  
In the **Update Details** tab, you can view the following summary information about the selected software update:  

- **Bulletin ID**: Specifies the bulletin ID that is associated with security software updates. You can find security bulletin details by searching on the bulletin ID on the [Microsoft Security Response Center](https://portal.msrc.microsoft.com/) Web page.  

> [!NOTE]
> The way Microsoft documents security updates is changing. The previous model used security bulletin webpages and included security bulletin ID numbers (e.g. MS16-XXX) as a pivot point. This form of security update documentation, including bulletin ID numbers, is being retired and replaced with the Security Update Guide. Instead of bulletin IDs, the new guide pivots on vulnerability ID numbers and KB Article ID numbers. For more information, see the [Security Update Guide FAQs](https://www.microsoft.com/msrc/faqs-security-update-guide).


- **Article ID**: Specifies the article ID for the software update. The referenced article provides more detailed information about the software update and the issue that the software update fixes or improves.  

- **Date revised**: Specifies the date that the software update was last modified.  

- **Maximum severity rating**: Specifies the vendor-defined severity rating for the software update.  

- **Description**: Provides an overview of what condition the software update fixes or improves.  

- **Applicable languages**: Lists the languages for which the software update is applicable.  

- **Affected products**: Lists the products for which the software update is applicable.  

####  <a name="BKMK_ContentInformation"></a> Content information  
In the **Content Information** tab, review the following information about the content that is associated with the selected software update:  

-   **Content ID**: Specifies the content ID for the software update.  

-   **Downloaded**: Indicates whether Configuration Manager has downloaded the software update files.  

-   **Language**: Specifies the languages for the software update.  

-   **Source Path**: Specifies the path to the software update source files.  

-   **Size (MB)**: Specifies the size of the software update source files.  

####  <a name="BKMK_CustomBundleInformation"></a> Custom bundle information  
In the **Custom Bundle Information** tab, review the custom bundle information for the software update. When the selected software update contains bundled software updates that are contained in the software update file, they are displayed in the **Bundle information** section. This tab does not display bundled software updates that are displayed in the **Content Information** tab, such as update files for different languages.  

####  <a name="BKMK_SupersedenceInformation"></a> Supersedence information  
On the **Supersedence Information** tab, you can view the following information about the supersedence of the software update:  

- **This update has been superseded by the following updates**: Specifies the software updates that supersede this update, which means that the updates listed are newer. In most cases, you will deploy one of the software updates that supersedes the software update. The software updates that are displayed in the list contain hyperlinks to webpages that provide more information about the software updates. When this update is not superseded, **None** is displayed.  

- **This update supersedes the following updates**: Specifies the software updates that are superseded by this software update, which means this software update is newer. In most cases, you will deploy this software update to replace the superseded software updates. The software updates that are displayed in the list contain hyperlinks to web pages that provide more information about the software updates. When this update does not supersede any other update, **None** is displayed.  

###  <a name="BKMK_SoftwareUpdatesSettings"></a> Configure software updates settings  
In the properties, you can configure software update settings for one or more software updates. You can configure most software update settings only at the central administration site or stand-alone primary site. The following sections will help you to configure settings for software updates.  

####  <a name="BKMK_SetMaxRunTime"></a> Set maximum run time  
In the **Maximum Run Time** tab, set the maximum amount of time a software update is allotted to complete on client computers. If the update takes longer than the maximum run-time value, Configuration Manager creates a status message and stops the software updates installation. You can configure this setting only on the central administration site or a stand-alone primary site.  

Configuration Manager also uses this setting to determine whether to initiate the software update installation within a configured maintenance window. If the maximum run-time value is greater than the available remaining time in the maintenance window, the software updates installation is postponed until the start of the next maintenance window. When there are multiple software updates to be installed on a client computer with a configured maintenance window (timeframe), the software update with the lowest maximum run time installs first, then the software update with the next lowest maximum run time installs next, and so on. Before it installs each software update, the client verifies that the available maintenance window will provide enough time to install the software update. After a software update starts installing, it will continue to install even if the installation goes beyond the end of the maintenance window. For more information about maintenance windows, see the [How to use maintenance windows](../../core/clients/manage/collections/use-maintenance-windows.md).  

On the **Maximum Run Time** tab, you can view and configure the following settings:  

- **Maximum run time**: Specifies the maximum number of minutes allotted for a software update installation to complete before the installation is stopped by Configuration Manager. This setting is also used to determine whether there is enough available time remaining to install the update before the end of a maintenance window. The default setting is 60 minutes for service packs. For other software update types, the default is 10 minutes if you did a fresh install of Configuration Manager version 1511 or higher and 5 minutes when you upgraded from a previous version. Values can range from 5 to 9999 minutes.  

> [!IMPORTANT]  
>  Be sure to set the maximum run time value smaller than the configured maintenance window time or increase the maintenance window time to a value greater than the maximum run time. Otherwise, the software update installation will never initiate.  

####  <a name="BKMK_SetCustomSeverity"></a> Set custom severity  
In the properties for a software update, you can use the **Custom Severity** tab to configure custom severity values for the software updates. This may be necessary if the predefined severity values do not meet your needs. The custom values are listed in the **Custom Severity** column in the Configuration Manager console. You can sort the software updates by the defined custom severity values and can also create queries and reports that can filter on these values. You can configure this setting only on the central administration site or stand-alone primary site.  

You can configure the following settings on the **Custom Severity** tab.  

- **Custom severity**: Sets a custom severity value for the software updates. Select **Critical**, **Important**, **Moderate**, or **Low** from the list. By default, the custom severity value is empty.

## CRL checking for software updates
By default, the certificate revocation list (CRL) is not checked when verifying the signature on Configuration Manager software updates. Checking the CRL each time a certificate is used offers more security against using a certificate that has been revoked, but it introduces a connection delay and incurs additional processing on the computer performing the CRL check.  

If used, CRL checking must be enabled on the Configuration Manager consoles that process software updates.  

#### To enable CRL checking  
On the computer performing the CRL check, from the product DVD, run the following from a command prompt: **\SMSSETUP\BIN\X64\\**<*language*>**\UpdDwnldCfg.exe /checkrevocation**.  

For example, for English (US) run **\SMSSETUP\BIN\X64\00000409\UpdDwnldCfg.exe /checkrevocation**