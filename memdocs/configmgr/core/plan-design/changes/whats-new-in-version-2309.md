---
title: What's new in version 2309
titleSuffix: Configuration Manager
description: Get details about changes and new capabilities introduced in version 2309 of Configuration Manager current branch.
ms.date: 11/15/2023
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

# What's new in version 2309 of Configuration Manager current branch

*Applies to: Configuration Manager (current branch)*

Update 2309 for Configuration Manager current branch is available as an in-console update. Apply this update on sites that run version 2207 or later. This article summarizes the changes and new features in Configuration Manager, version 2309.
                                                                                                                                                                                                                                                                                                                          
Always review the latest checklist for installing this update. For more information, see [Checklist for installing update 2309](../../servers/manage/checklist-for-installing-update-2309.md). After you update a site, also review the [Post-update checklist](../../servers/manage/checklist-for-installing-update-2309.md#post-update-checklist).

To take full advantage of new Configuration Manager features, after you update the site, also update clients to the latest version. While new functionality appears in the Configuration Manager console when you update the site and console, the complete scenario isn't functional until the client version is also the latest.

## Site infrastructure

### Introducing SQL ODBC driver support for Configuration Manager

Starting with Configuration Manager 2309 release, Configuration Manager requires the installation of the ODBC driver for SQL server 18.1.0 or later as a prerequisite. This prerequisite is required when you create a new site or update an existing one and on all remote roles.

> [!IMPORTANT]
> Microsoft ODBC Driver for SQL Server 18.1.0 or later needs to be installed on Site Servers and site system roles before upgrading to 2309 version.
> Do not uninstall SQL native client 11 until we call out in further communications. Configuration Manager doesn't manage the updates for the ODBC driver, ensure that this component is up to date.

For more information, see [SQL ODBC driver for the site server](../..//plan-design/configs/site-and-site-system-prerequisites.md#sql-odbc-driver-for-the-site-server)

### Option to schedule scripts' runtime

Starting in Configuration Manager current branch version 2309, you can now schedule scripts' runtime in UTC. The run Script Wizard now offers a scheduling option that enables administrators to schedule the execution of scripts. It provides a convenient way to automate the running of scripts on managed devices according to specified schedules.

:::image type="content" source="media/17668435-schedule-script.png" alt-text="A screenshot of the schedule script wizard.":::

For more information, see [Schedule scripts' runtime](../../../apps/deploy-use/create-deploy-scripts.md#schedule-scripts-runtime)

### External service notification Run details from Azure Logic application  

Starting in Configuration Manager current branch version 2309, when Azure Logic App generates notifications related to specific events, CM can now capture and display these notifications. This integration enables the monitoring of Azure Logic App notifications directly within the MCM console, providing a centralized location for tracking critical events, taking appropriate actions and maintains a high level of operational efficiency.

:::image type="content" source="media/17668438-external-service.png" alt-text="A screenshot of the run details of external service notification wizard.":::

For more information, see [External service notification](../../servers/manage/external-notifications.md#monitor-the-workflow).

### New Site Maintenance task “Delete Aged Task Execution Status Messages” is now available on primary servers to clean up data older than 30 days or configured number of days

Starting in Configuration Manager current branch version 2309, you can now enable this feature by utilizing the Site Maintenance Window or using PowerShell Commandlet. By default, it has been set to run on Saturday and delete the data older than 30 days. It does so by cleaning up [dbo].TaskExecutionStatus Table  

Example: 
PowerShell Commandlet: ```Set-CMSiteMaintenanceTask -Sitecode "XXX" -MaintenanceTaskName "Delete Aged Task Execution Status Messages" -DaysOfWeek Friday ```

For more information, see [Delete Aged Task Execution Status Messages](../../servers/manage/reference-for-maintenance-tasks.md#delete-aged-task-execution-status-messages).

## Software updates

### Update Orchestrator Service (USO) for Windows 11 22H2 or later with windows native reboot experience 

In Configuration Manager current branch version 2309, when installing software updates from Configuration Manager, administrators can now choose to use the **native Windows Update restart** experience.To use this feature, client devices must be running Windows build 22H2 or later. From the Computer Restart client device settings, ensure that Windows is selected as the restart experience. Branding information is included in the Windows restart notification for updates that require restart. 

For more information, see [Device restart notifications](../../clients/deploy/device-restart-notifications.md#device-restart-notifications-in-configuration-manager)

### Maintenance window creation using PS cmdlet 

We've extended the Offset parameter for **Maintenance windows**.The cmdlet New-CMMaintenanceWindow is used to create a maintenance window for a collection. Earlier the Offset parameter could be set only between 0 and 4. Now it has been extended between 0 to 7.

Example: 
PowerShell Commandlet: ``` New-CMSchedule -Start (Get-Date) -DayOfWeek Monday -WeekOrder Second -RecurCount 1 -OffSetDay 6 ```


## OS deployment

### OSD preferred MP option for PXE boot scenario  

Starting in Configuration Manager current branch version 2309, Preferred Management Point (MP) option will now allow **PXE clients** to communicate to an initial lookup MP and receive the list of MP(s) to be used for further communication. When the option is enabled, it allows an MP to redirect the PXE client to another MP, based on the client location in the site boundaries.

:::image type="content" source="media/2839966-osd-mp-pxe.png" alt-text="A screenshot of the management point option in console.":::

For more information, see [Install-and-configure-distribution-points](../../servers/deploy/configure/install-and-configure-distribution-points.md)

### Enable Bitlocker through ProvisionTS  

In Configuration Manager current branch version 2309, Escrowing recovery key to Config Manager Database is now supported using ProvisionTS. **ProvisionTS** is the task sequence that is executed at the time of provisioning. As a result device can escrow the key to Config Manager Database instantly.

For more information, see [Preprovision-bitlocker-in-windows-pe](../../../osd/deploy-use/preprovision-bitlocker-in-windows-pe.md)

### Windows 11 Edition Upgrade using CM Policy settings 

Starting in Configuration Manager current branch version 2309,administrator can now create a policy using edition upgrade in Configuration Manager to update the **Windows 11 edition**.   

:::image type="content" source="media/17668419-edition-upgrade-windows11.png" alt-text="A screenshot of the windows 11 edition upgrade wizard.":::

For more information, see [Upgrade Windows devices to a new edition](../../../compliance/deploy-use/upgrade-windows-version.md)

### Windows 11 Upgrade Readiness Dashboard 

Starting in Configuration Manager current branch version 2309, administrators can use this dashboard to devise their windows 11 upgrade strategy and discover the devices in the organization, which are ready for **Windows 11 Upgrade**. This Dashboard also provides a count by installed Feature update version and a view of all Windows devices inside the organization. Administrators can create a collection of Windows 11 ready for upgrading devices and roll out feature updates to them.

:::image type="content" source="media/17668425-windows11-dashboard.png" alt-text="A screenshot of UX of windows 11 readiness dashboard." lightbox="media/17668425-windows11-dashboard.png":::


For more information, see [Manage Windows 11 readiness dashboard](../../../osd/deploy-use/manage-windows-11-readiness-dashboard.md)

## Cloud-attached management

### New Cloud Management Gateway (CMG) creation via Console 

Starting in Configuration Manager current branch version 2309, we have enhanced security of **web (server) app** for the creation of CMG. For new CMG creation, users can select tenant and the app name using the Azure AD tenant name. After selecting tenant and app name the sign-in button appears, follow rest of the process as per the setup CMG.

:::image type="content" source="media/cmg-console-creation.png" alt-text="A screenshot of the cmg app creation via console.":::

>[!NOTE]
>Pre-existing CMG customers must update their web server app by navigating to Azure Active Directory Tenants node --> select the tenant --> select the server app --> click on "update application settings".

For more information, see [Configure Azure Active Directory for CMG](../../clients/manage/cmg/configure-azure-ad.md)

### New Cloud Management Gateway (CMG) creation via PowerShell 

You can now create CMG **web (server) app** via PowerShell cmdlet, you need to specify TenantID in the argument: 

PowerShell Commandlet:  ``` Set-UpdateServerApplication – 'TenantID' ```

If you try to create the CMG before updating RedirectUrl, you get an error "Your server Application needs to be updated".

PowerShell command: ``` Set-UpdateServerApplication ``` to update your App, and then try again to create CMG.

>[!NOTE] 
> For new customers, before creating CMG, create Azure AD web server app and execute the new PowerShell commandlet script.

For more information, see [New-CMCloudManagementGateway](/powershell/module/configurationmanager/new-cmcloudmanagementgateway)

## Deprecated features

Learn about support changes before they're implemented in [removed and deprecated items](deprecated/removed-and-deprecated.md).

 - Configured resource access policies will block Configuration Manager 2403 upgrade, remove existing policies and move the slider to Intune. Please action before January 2024, read the [FAQ](../../../../configmgr/protect/plan-design/resource-access-deprecation-faq.yml).

For more information, see [Removed and deprecated features for Configuration Manager](deprecated/removed-and-deprecated-cmfeatures.md).

## Other updates

For more information on changes to the Windows PowerShell cmdlets for Configuration Manager, see [version 2309 release notes](/powershell/sccm/2309-release-notes).

## Next steps
<!--At this time, version 2309 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-2309.md#early-update-ring).-->

As of November 1, 2023, version 2309 is globally available for all customers to install.

>[!NOTE] 
> For exisiting Fast ring current branch 2309 customers, you will see Slow ring upgrade package in console. Install 2309 Slow ring package to be in production current branch.

When you're ready to install this version, see [Installing updates for Configuration Manager](../../servers/manage/updates.md) and [Checklist for installing update 2309](../../servers/manage/checklist-for-installing-update-2309.md).

> [!TIP]
> To install a new site, use a baseline version of Configuration Manager.
>
> Learn more about:
>
> - [Installing new sites](../../servers/deploy/install/installing-sites.md)
> - [Baseline and update versions](../../servers/manage/updates.md#bkmk_Baselines)

For known significant issues, see the [Release notes](../../servers/deploy/install/release-notes.md).

After you update a site, also review the [Post-update checklist](../../servers/manage/checklist-for-installing-update-2309.md#post-update-checklist).
