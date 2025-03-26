---
title: What's new in version 2303
titleSuffix: Configuration Manager
description: Get details about changes and new capabilities introduced in version 2303 of Configuration Manager current branch.
ms.date: 03/31/2023
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: whats-new
author: PalikaSingh
ms.author: palsi
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# What's new in version 2303 of Configuration Manager current branch

*Applies to: Configuration Manager (current branch)*

Update 2303 for Configuration Manager current branch is available as an in-console update. Apply this update on sites that run version 2111 or later. <!-- baseline only statement:--> When installing a new site, this version of Configuration Manager will also be available as a [baseline version](../../servers/manage/updates.md#bkmk_note1) soon after global availability of the in-console update. This article summarizes the changes and new features in Configuration Manager, version 2303.

Always review the latest checklist for installing this update. For more information, see [Checklist for installing update 2303](../../servers/manage/checklist-for-installing-update-2303.md). After you update a site, also review the [Post-update checklist](../../servers/manage/checklist-for-installing-update-2303.md#post-update-checklist).

To take full advantage of new Configuration Manager features, after you update the site, also update clients to the latest version. While new functionality appears in the Configuration Manager console when you update the site and console, the complete scenario isn't functional until the client version is also the latest.

## Microsoft Configuration Manager product branding 
<!--15885998-->
Starting with Configuration Manager version 2303 Microsoft Endpoint Configuration Manager is now Microsoft Configuration Manager. 
Microsoft Configuration Manager is an integrated solution for managing all your devices. Microsoft brings together Configuration Manager and Intune, without a complex migration, and with simplified licensing. Continue to use your existing Configuration Manager investments, while taking advantage of the power of the Microsoft cloud at your own pace. 

> [!TIP]
> Support center tool and client must be upgraded to latest version to move program files path to new Microsoft configuration Manager start menu path.

For more information, see [Microsoft Configuration Manager FAQ](../../understand/configuration-manager-faq.yml)

## Cloud-attached management
<!--14716797-->
### Improvements to Cloud Sync (Collections to Azure Active Directory Group Synchronization) feature
Starting with Configuration Manager version 2303 collection member sync status (Success, In Progress, Failed - with reason for failure) is available in the Collection Cloud Sync dashboard for the chosen collection on the bottom pane. Earlier with Configuration Manager version 2211, the scalability of this feature has been improved with better throttling and error handling. Additionally, dedicated dashboards for user collections and device collections are added in Monitoring workspace to show Cloud Sync status. The dashboard displays the Cloud Sync status per collection with the mapped Azure AD group, total member count, synced member count, status (success, failed, in progress) and last sync details. 

For more information, see [Synchronize collections to Azure Active Directory Group](../../clients/manage/collections/synchronize-collections-aad-group.md).

<!--13061435-->
### Endpoint Security reports in Intune admin center for Tenant Attached devices 
Starting with Configuration Manager version 2303, you can now opt for Endpoint Security reports in Intune admin center for tenant attached devices.   
Once you opt in, Unhealthy endpoints and Active malware operational reports under Endpoint security node in Intune admin center will start showing data from tenant attached devices. Also, Antivirus agent status and Detected malware organizational reports under Microsoft Defender Antivirus in Reports section will show data from tenant attached devices. 

For more information, see [Tenant attach - Create and deploy Antivirus policies from the admin center](../../../tenant-attach/deploy-antivirus-policy.md#bkmk_mdereports).

## Site infrastructure
<!--13022894-->

### Authorization failure message in admin service now shown in Status message viewer 

We have introduced audit messages about authorization failure in admin service. You can now view request details and status messages. These messages are shown in “All Status Message” at “Status Message Queries” in “Monitoring” ribbon. Previously these failures were logged in log files. 

With the new audit messages, we intend to avoid the inconvenience of log files rollback. Details about the user, resource access attempts and the number of attempts for all the authorized requests made by user in a day will now be available. We are also auditing read operations for HTTPS requests and for cloud-initiated operations. This helps admins to scope permission and roles of users while also determining if there are any malicious users. All unauthorized requests are aggregated for 24 hours before being sent to the status message viewer. 

For more information, see [Administration Service documentation](../../../develop/adminservice/overview.md).

### SQL Server 2022 version support added for Configuration Manager 

Starting with 2303, support is added for SQL server 2022 RTM version. 
You can use this version of SQL Server for the following sites: 
-	A central administration site 
-	A primary site 
-	A secondary site 

The following table identifies the recommended compatibility levels for Configuration Manager site databases:

|SQL Server version | Supported compatibility levels | Recommended level |
|----------------|--------------------|--------|
| SQL Server 2022 | 150, 140, 130, 120, 110 | 150 |

For more information, see [support-for-sql-server-versions](../../plan-design/configs/support-for-sql-server-versions.md).
<!--## Client management-->
<!--## Collections-->
<!--## Software Center-->
## Software updates

### Unified update platform (UUP) GA release 

The Unified Update Platform (UUP) servicing is finally here for all Windows 11, version 22H2 updates delivered via Windows Server Update Services (WSUS) and Configuration Manager! Starting March 28, on-premises Windows 11, version 22H2 devices will receive quality updates via the Unified Update Platform (UUP). For more information, see [What’s UUP? New update style!](https://techcommunity.microsoft.com/t5/windows-it-pro-blog/what-s-uup-new-update-style-coming-next-week/ba-p/3773065). 
The Unified Update Platform (UUP) is a single publishing, hosting, scan, and download model for OS quality and feature updates. It offers improved delivery technologies in response to IT admin requests for more seamless updates, more control over installation time, more battery life, and lighter download size.  

> [!NOTE]
>A one-time 10-GB download to distribution points with your first UUP update. UUP is becoming the default and only way to download quality updates. This means that you should plan for an extra 10GB download to distribution points (not endpoint clients) with the March 28th update. That's a one-time 10GB download for updates for Windows 11, version 22H2 per architecture (AMD64 and ARM64). 

### Update to the default value of supersedence age in months for software updates
<!--16441147-->
With Unified Update Platform (UUP) general availability release, the feature update and non-feature update supersedence should be greater than 3. For new software update role installations, we're updating this to 6, existing customers can review and update to 6.  
Update to the default value of supersedence age in months for software updates.  

#### Known issue

Update to the default value of supersedence age in months for software updates will not impact existing configurations. Removing SUP role in Admin Console does not reset the supersedence age property in WMI. As a result, while reconfiguring the role, the previously configured value is shown in the configuration window.  

### Enable Windows features introduced via Windows servicing that are off by default 
<!--16834520-->

The Commercial control for continuous innovation in Windows is now integrated with Configuration Manager 2303 release. [Commercial control for continuous innovation (Windows 11)](https://techcommunity.microsoft.com/t5/windows-it-pro-blog/commercial-control-for-continuous-innovation/ba-p/3737575)

For more information, see [client settings in Configuration Manager](../../clients/deploy/about-client-settings.md)

<!--## OS deployment-->

<!--## Endpoint Protection-->

<!--## Application management-->

<!--## Community hub-->

## Configuration Manager console

### Dark theme extended to delete secondary site wizard 
<!--15942599-->
The Configuration Manager console now extends the dark theme for the delete secondary site wizard. This wizard will also have a new look for the normal theme. This is part of the ongoing effort to make dark theme and overall admin console experience better. 

To use the theme, select the arrow from the top left of the ribbon, then choose the Switch console theme. Select Switch console theme again to return to the light theme. For more information, see [Dark theme for the console](../../servers/manage/admin-console.md#bkmk_dark).
  
<!--## Tools-->

## Deprecated features
<!--10901602-->

### Removed Community hub service and integration with ConfigMgr 
 
Removed Community Hub configuration from Hierarchy settings and Community Hub service integration. 
 Learn about support changes before they're implemented in [removed and deprecated items](deprecated/removed-and-deprecated-cmfeatures.md).
<!--The following features are deprecated. You can still use them now, but Microsoft plans to end support in the future.-->

## Other updates

### Maintenance window schedules
Offset for recurring monthly maintenance window schedules. Based upon your feedback, you can now offset monthly maintenance window schedules to better align deployments with the release of monthly security updates. For example, using a maximum offset of seven days after the second Tuesday of the month, sets the maintenance window for next Monday. 

### Removing Microsoft Store for Business and Education new config capability

As part of Microsoft Store for Business deprecation, we are making these changes to the customer experience with using this feature: 

- Removing a user's ability to create new Microsoft Store for Business in Configuration Manager. 

- Display a warning message box when user triggers a sync from Microsoft Store for Business. 

- Display a warning in the Create Application Wizard when user attempts to create a new app from Store license information. 

For more information, see [removed and deprecated items](deprecated/removed-and-deprecated-cmfeatures.md). 
<!--Starting with this version, the following features are no longer [pre-release](../../servers/manage/pre-release-features.md):
-->

<!--For more information on changes to the Windows PowerShell cmdlets for Configuration Manager, see [version 2207 release notes](/powershell/sccm/2207-release-notes).-->

<!--

The following update rollup (4517869) is available in the console starting on October 1, 2019: [Update rollup for Configuration Manager current branch, version 1906](https://support.microsoft.com/help/4517869).
-->

<!--
### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [9833643](../../../hotfix/2111/9833643.md) | Console update for Microsoft Endpoint Configuration Manager version 2111 | May 11, 2021 | No |
-->

## Next steps
<!-- At this time, version 2303 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-2303.md#early-update-ring).-->

 As of April 24, 2023, version 2303 is globally available for all customers to install.

When you're ready to install this version, see [Installing updates for Configuration Manager](../../servers/manage/updates.md) and [Checklist for installing update 2303](../../servers/manage/checklist-for-installing-update-2303.md).

> [!TIP]
> To install a new site, use a baseline version of Configuration Manager.
>
> Learn more about:
>
> - [Installing new sites](../../servers/deploy/install/installing-sites.md)
> - [Baseline and update versions](../../servers/manage/updates.md#bkmk_Baselines)

For known significant issues, see the [Release notes](../../servers/deploy/install/release-notes.md).

After you update a site, also review the [Post-update checklist](../../servers/manage/checklist-for-installing-update-2303.md#post-update-checklist).
