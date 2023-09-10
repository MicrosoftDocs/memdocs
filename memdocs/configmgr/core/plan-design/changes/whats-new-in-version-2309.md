---
title: What's new in version 2309
titleSuffix: Configuration Manager
description: Get details about changes and new capabilities introduced in version 2309 of Configuration Manager current branch.
ms.date: 08/25/2023
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: PalikaSingh
ms.author: palsi
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# What's new in version 2309 of Configuration Manager current branch

*Applies to: Configuration Manager (current branch)*

Update 2309 for Configuration Manager current branch is available as an in-console update. Apply this update on sites that run version 2203 or later. <!-- baseline only statement:--> When installing a new site, this version of Configuration Manager will also be available as a [baseline version](../../servers/manage/updates.md#bkmk_note1) soon after global availability of the in-console update. This article summarizes the changes and new features in Configuration Manager, version 2309.
                                                                                                                                                                                                                                                                                                                          
Always review the latest checklist for installing this update. For more information, see [Checklist for installing update 2303](../../servers/manage/checklist-for-installing-update-2303.md). After you update a site, also review the [Post-update checklist](../../servers/manage/checklist-for-installing-update-2303.md#post-update-checklist).

To take full advantage of new Configuration Manager features, after you update the site, also update clients to the latest version. While new functionality appears in the Configuration Manager console when you update the site and console, the complete scenario isn't functional until the client version is also the latest.

## Site infrastructure

### Introducing SQL ODBC driver support for Configuration Manager

Config Manager stores both Configuration and Reporting data in SQL Server Database. Components written in native code access this data in SQL Database by leveraging SQL Native Client 11 driver which has been deprecated. It needs to be replaced with the latest Microsoft ODBC Driver for SQL Server 18.1.0.

Feature requirements:
 - Remove the deprecated SQL Server Native Client 11.0 package in Config Manager..
 - Replace SNAC 11.0 with the latest Microsoft ODBC Driver for SQL Server (version 18.1.0).
 - Update code with hard dependency on SQL Server Native Client 11.0 to use Microsoft ODBC Driver instead.

### Option to schedule Scripts execution time

The Run Script Wizard now offers a scheduling option which enables administrators to schedule the execution of scripts. It provides a convenient way to automate the running of scripts on managed devices according to specified schedules.  

### Update Orchestrator Service (USO) for Windows 11 22H2 or later with windows native reboot experience 

To use this feature, client devices must be running Windows build 22H2 or later. From the Computer Restart client device settings, ensure that Windows is selected as the restart experience. When installing software updates from Configuration Manager, administrators can now choose to use the native Windows Update restart experience. Branding information will be included in the Windows restart notification for updates that require restart. 

### Windows 11 Edition Upgrade using CM Policy settings 

Administrator can now create a policy using edition upgrade in Configuration Manager to update the Windows 11 edition.   

### Windows 11 Upgrade Readiness Dashboard 

Administrators can use this dashboard to devise their windows 11 upgrade strategy and discover the devices in the organization which are ready for Windows 11 Upgrade.This Dashboard also provides a count by installed Feature update version and a view of all Windows devices inside the organization. Administrators can create a collection of Windows 11 ready for upgrading devices and roll out feature updates to them.  

### External service notification Run details from Azure Logic application.  

When Azure Logic Apps generate notifications or alerts related to specific events or conditions, CM can now capture and display these notifications within the console to the users. This integration enables the monitoring and management of Azure Logic App notifications directly within the MCM console, providing a centralized location for tracking critical events, taking appropriate actions and maintain a high level of operational efficiency.  

### Maintenance window creation using PS cmdlet 

Maintenance windows are recurring periods of time when the Configuration Manager client can run tasks. The cmdlet New-CMMaintenanceWindow is used to create a maintenance window for a collection. Earlier the Offset parameter could be set only between 0 and 4. Now it has been extended between 0 to 7. 

### OSD preferred MP option for PXE boot scenario  

Preferred Management Point (MP) option will now allow PXE clients to communicate to an initial lookup MP and receive the list of MP(s) to be used for further communication. When the option is enabled, it will allow an MP to redirect the *PXE client to another MP, based on the client location in the site boundaries.  

### CMG creation using 3rd PartyApp via Console  

We have deprecated the use of 1st party app for the creation of CMG. Now, CMG will use a 3rd party server app to get bearer tokens. 

### CMG creation using 3rd Party ServerApp via PowerShell  

To create CMG using 3rd party Server app via Powershell cmdlet, you need  to specify TenantID in the argument, as below:  
PowerShell Commandlet: Set-UpdateServerApplication – TenantID  
if existing (non-updated) Azure AD server app is used, please ensure that the sever app has RedirectUrl=”http://localhost” added in Azure Portal and in TableAAD_Application_EX in Database.  If you try to create the CMG before updating RedirectUrl, you will get an error-‘Your server Application needs to be updated. Please run this powershell command: "Set-UpdateServerApplication" to update your App, and then try again to create CMG.’  

Note: For new customers, before creating CMG please create Azure AD server app, that contains the RedirectUrl in your App.  
Example : Set-UpdateServerApplication – TenantID  
Once redirect URL and database settings are complete, you can execute the new Powershell commandlet script.  

### New Site Maintenance task “Delete Aged Task Execution Status Messages” is now available on primary servers to cleanup data older than 30 days or configured number of days

You can enable this feature by utilizing the Site Maintenance Window or using PowerShell Commandlet. By default, it has been set to run on Saturday and delete the data older than 30 days. It does so by cleaning up [dbo].TaskExecutionStatus Table  

Example : Set-CMSiteMaintenanceTask -Sitecode "XXX" -MaintenanceTaskName "Delete Aged Task Execution Status Messages" -DaysOfWeek Friday  

### Enable Bitlocker through ProvisionTS  

ProvisionTS is the task sequence which is executed at the time of provisioning. Escrowing recovery key to Config Manager Database is now supported using ProvisionTS. As a result, device can escrow the key to Config Manager Database instantly.  

### Attack Surface Reduction (ASR) capability now marks Server SKU as compliant only after enforcement.   

Prior to the ASR capability in Windows Server, ASR rules were marked compliant by default. As this rule setting becomes available to Server SKU, it will be enforced through Config Manager. Now the Server SKU will be marked as compliant for an ASR rule, only after enforcement of the rule.  

  



## Next steps
At this time, version 2309 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-2303.md#early-update-ring).

<!--  As of April 24, 2023, version 2303 is globally available for all customers to install.

When you're ready to install this version, see [Installing updates for Configuration Manager](../../servers/manage/updates.md) and [Checklist for installing update 2303](../../servers/manage/checklist-for-installing-update-2303.md).-->

> [!TIP]
> To install a new site, use a baseline version of Configuration Manager.
>
> Learn more about:
>
> - [Installing new sites](../../servers/deploy/install/installing-sites.md)
> - [Baseline and update versions](../../servers/manage/updates.md#bkmk_Baselines)

For known significant issues, see the [Release notes](../../servers/deploy/install/release-notes.md).

After you update a site, also review the [Post-update checklist](../../servers/manage/checklist-for-installing-update-2303.md#post-update-checklist).
