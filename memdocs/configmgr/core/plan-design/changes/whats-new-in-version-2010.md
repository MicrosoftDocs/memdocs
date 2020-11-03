---
title: What's new in version 2010
titleSuffix: Configuration Manager
description: Get details about changes and new capabilities introduced in version 2010 of Configuration Manager current branch.
ms.date: 11/20/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: eca60d1f-6970-4a2d-b170-35353d0d961c
author: mestew
ms.author: mstewart
manager: dougeby 
---

# What's new in version 2010 of Configuration Manager current branch

*Applies to: Configuration Manager (current branch)*

Update 2010 for Configuration Manager current branch is available as an in-console update. Apply this update on sites that run version 1906 or later. <!-- baseline only statement:When installing a new site, it's also available as a baseline version. -->This article summarizes the changes and new features in Configuration Manager, version 2010.

Always review the latest checklist for installing this update. For more information, see [Checklist for installing update 2010](../../servers/manage/checklist-for-installing-update-2010.md). After you update a site, also review the [Post-update checklist](../../servers/manage/checklist-for-installing-update-2010.md#post-update-checklist).

To take full advantage of new Configuration Manager features, after you update the site, also update clients to the latest version. While new functionality appears in the Configuration Manager console when you update the site and console, the complete scenario isn't functional until the client version is also the latest.

> [!TIP]
> To get notified when this page is updated, copy and paste the following URL into your RSS feed reader:
> `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+2010+-+Configuration+Manager%22&locale=en-us`

## Microsoft Endpoint Manager tenant attach


## Endpoint analytics


## Site infrastructure

### Monitor scenario health

<!--7699463-->

Configuration Manager is complicated to troubleshoot. It's especially complex to understand system latency and the backlog between components. Cloud service-attached features increase that complexity.

You can now use Configuration Manager to monitor the health of end-to-end scenarios. It simulates activities to expose performance metrics and failure points. These synthetic activities are similar to methods that Microsoft uses to monitor some components in its cloud services. Use this additional data to better understand timeframes for activities. If failures occur, it can help focus your investigation.

The first scenario in this release is for **SQL Server Service Broker**. The service broker is a required configuration for the site database. Many of the core subsystems in Configuration Manager use the service broker.

<!--7699511-->

You can now monitor the health of the fast channel used for client actions. If your environment is tenant attached with devices uploaded, this feature helps you see potential issues with client actions from the Microsoft Endpoint Manager admin center. You can also use this feature for on-premises client actions. For example, CMPivot, run scripts, and device wake-up.

### Report setup and upgrade failures to Microsoft
<!--5622909-->
 If the setup or update process fails to complete successfully, you can now report the error directly to Microsoft. If a failure occurs, the **Report update error to Microsoft** button is enabled. When you use the button, an interactive wizard opens allowing you to provide more information to us. In technical previews, this button is always enabled even when the setup completes successfully.

### Delete Aged Collected Diagnostic Files task
<!--6503308-->
You now have a new maintenance task available for cleaning up collected diagnostic files. **Delete Aged Collected Diagnostic Files** uses a default value of 14 days when looking for diagnostic files to clean up and doesn't affect regular collected files. The new maintenance task is enabled by default.

## Cloud-attached management

### Cloud management gateway with virtual machine scale set

<!--3601040-->

Cloud management gateway (CMG) deployments now use virtual machine scale sets in Azure. This change introduces support for Azure Cloud Solution Provider (CSP) subscriptions.

## Desktop Analytics

For more information on the monthly changes to the Desktop Analytics cloud service, see [What's new in Desktop Analytics](../../../desktop-analytics/whats-new.md).

### Desktop Analytics support for Windows 10 Enterprise LTSC

<!--6107649-->

The Windows 10 long-term servicing channel (LTSC) was designed for devices where the key requirement is that functionality and features don't change over time. This servicing model prevents Windows 10 Enterprise LTSC devices from receiving the usual feature updates. It provides only quality updates to make sure that device security stays up to date. Some customers want to shift from LTSC to the semi-annual servicing channel, to have access to new features, services, and other major changes. Starting in this release, you can now enroll LTSC devices to Desktop Analytics to evaluate in your deployment plans.

## Real-time management


## Client management

### Wake machine at deployment deadline using peer clients on the same remote subnet
<!--3734819-->

Wake on LAN (WoL) has always posed a problem in complex, subnetted networks. Good networking best practice reduces the size of broadcast domains to mitigate against the risk of broadcast traffic adversely affecting the network. The most common way to limiting network broadcast is by not allowing broadcast packets to be routed between subnets. Another option is to enable subnet directed broadcasts but most organizations don't allow the magic packet to traverse internal routers.

In version 1810, the introduction of peer wake up allowed an administrator to wake a device or collection of devices, on demand using the client notification channel. Overcoming the need for the server to be in the same broadcast domain as the client.

This latest improvement allows the Configuration Manager site to wake devices at the deadline of a deployment, using that same client notification channel. Instead of the site server issuing the magic packet directly, the site uses the client notification channel to find an online machine in the last known subnet of the target device(s) and instructs the online client to issue the WoL packet for the target device.

### Improved Windows Server restart experience for non-administrator accounts

<!--7821529-->

For a low-rights user on a device that runs Windows Server, by default they aren't assigned the user rights to restart Windows. When you target a deployment to this device, this user can't manually restart. For example, they can't restart Windows to install software updates.

Starting in this release, you can now control this behavior as needed. In the **Computer Restart** group of client settings, enable the following setting: **When a deployment requires a restart, allow low-rights users to restart a device running Windows Server**.

## Application management

### Improvements to available apps via CMG

<!--7033501-->
An internet-based, domain-joined device that isn't joined to Azure Active Directory (Azure AD) and communicates via a cloud management gateway (CMG) can now get apps deployed as available. The Active Directory domain user of the device needs a matching Azure AD identity. When the user starts Software Center, Windows prompts them to enter their Azure AD credentials. They can then see any available apps.

## OS deployment

### Deploy an OS over CMG using boot media

<!--3555923-->

Starting in current branch version 2006, the cloud management gateway (CMG) supports running a task sequence with a boot image when you start it from Software Center. With this release, you can now use boot media to reimage internet-based devices that connect through a CMG. This scenario helps you better support remote workers. If Windows won't start so that the user can access Software Center, you can now send them a USB drive to reinstall Windows.

### Deploy a task sequence to a user

<!--8018255-->

You can now deploy a non-OS deployment task sequence to a user-based collection. Use the task sequence deployment type of an application to install or uninstall it.

### Manage task sequence policy size

<!--6888853-->

Configuration Manager technical preview version 2004 included new management insight rules for OS deployment. These insights help you manage the policy size of task sequences. Large task sequences cause problems with client processing.

To further help manage the size of task sequences, starting in this release Configuration Manager restricts the following actions for a task sequence that's greater than 2 MB in size:<!-- there are three items that talk about TS size, combine into a single blurb. -->

### See task sequence size in the console

<!--7645732-->

This release continues to iterate on changes in technical preview version 2004 and version 2007 to help you manage the size of task sequences. When you view the list of task sequences in the Configuration Manager console, add the **Size (KB)** column. Use this column to identify large task sequences that can cause problems.

### Analyze SetupDiag errors for feature updates

<!--4385028-->

With the release of Windows 10, version 2004, the [SetupDiag](/windows/deployment/upgrade/setupdiag) diagnostic tool is included with Windows Setup. If there's an issue with the upgrade, SetupDiag automatically runs to determine the cause of the failure.

Configuration Manager now gathers and summarizes SetupDiag results from feature update deployments with Windows 10 servicing.

The **Windows 10 Servicing** dashboard in the **Software Library** workspace of the Configuration Manager console now includes a tile for **Collection Errors**:

### Improvements to OS deployment

This release includes the following improvements to OS deployment:

- After you update the site to version 2010, the Configuration Manager console shows the size in KB for all existing task sequences.<!--7799892--> Previously, the console showed a size of **0** for existing task sequences, which only updated when you modified the task sequence.

- It resolves a bug with boot image metadata on PXE-enabled distribution points that have multiple content library drives.<!--7068388--> This bug could cause the client to fail to download the boot image over TFTP.

- Starting in Configuration Manager version 1910, to improve the overall speed of the task sequence, you can activate the Windows power plan for **High Performance**. Starting in this technical preview release, you can now use this option on devices with [modern standby](/windows-hardware/design/device-experiences/modern-standby) and other devices that don't have that default power plan. Now when you use this task sequence option, it creates a temporary power plan that's similar to the default for **High Performance**. After the task sequence completes, it reverts to the original power plan, and deletes the temporary plan.<!--7721999 & 8177793-->

## Protection

### Expanded Windows Defender Application Control management
<!--7752243-->
Windows Defender Application Control enforces an explicit list of software allowed to run on devices. In this technical preview, we've expanded Windows Defender Application Control policies to support devices running Windows Server 2016 or later.

## Collections

### Collection query preview
<!--7380401-->
You can now preview the query results when you're creating or editing a query for collection membership. Preview the query results from the query statement properties dialog. When you select **Edit Query Statement**, select the green triangle on the query properties for the collection to show the **Query Results Preview** window. Select **Stop** if you want to stop a long running query.

### Collection evaluation view
<!--6251274-->
We've integrated the functionality of Collection Evaluation Viewer into the Configuration Manager console. This change provides administrators a central location to view and troubleshoot the collection evaluation process.

### View collection relationships

<!--3608121-->

You can now view dependency relationships between collections in a graphical format. It shows limiting, include, and exclude relationships.

## Configuration Manager console

### Product feedback

<!--3180826-->

The Configuration Manager console has a new wizard for sending feedback. The redesigned wizard improves the workflow with better guidance about how to submit good feedback.

:::image type="content" source="media/3180826-send-a-smile-2010.png" alt-text="Send a smile product feedback wizard" lightbox="media/3180826-send-a-smile-2010.png":::

There's also a new status message query, **Feedback sent to Microsoft**. Use this query to easily find feedback status messages.<!--6488450-->

For more information, see [Product feedback](../../understand/product-feedback.md).

### Import objects to current folder

<!--6601203-->

Based on your feedback, now when you import an object in the Configuration Manager console, it imports to the current folder. Previously, Configuration Manager always put imported objects in the root node. This new behavior applies to applications, packages, driver packages, and task sequences.

### Copy discovery data from the console

<!--6890051-->

You can now copy discovery data from devices and users in the console. Copy the details to the clipboard, or export them all to a file. These new actions make it easier for you to quickly get this data from the console. For example, copy the MAC address of a device before you reimage it.

### Fixed-width font now used in some console areas

<!--7632637-->

Various areas in the Configuration Manager console now use the fixed-width font Consolas. This font provides consistent spacing and makes it easier to read.

### Syntax highlighting for scripting languages
<!--7964912-->

To assist you when creating scripts and queries in the Configuration Manager console, you'll now see syntax highlighting and code folding, where available.

### Shortcuts to status messages

<!--8232705-->

You now have an easier way to view status messages for objects.

### Improvements to in-console notifications
<!--7410221-->
You now have an updated look and feel for in-console notifications. Notifications are more readable and the action link is easier to find. Additionally, the age of the notification is displayed to help you find the latest information. If you dismiss or snooze a notification, that action is now persistent for your user across consoles.

## Content management

### Improvements to client data sources dashboard

<!--7102084-->

The client data sources dashboard now offers an expanded selection of filters to view information about where clients get content.

### Improvements to the content library cleanup tool

<!--6887878-->

If you remove content from a distribution point while the site system is offline, an orphaned record can exist in WMI. Over time, this behavior can eventually lead to a warning status on the distribution point. To mitigate the issue in the past, you had to manually remove the orphaned entries from WMI. Making a mistake during this process could cause more severe issues with the server.

The content library cleanup tool in delete mode could remove orphaned files from the content library. It can now also remove orphaned content records from the WMI provider on a distribution point. Run the tool with the `/delete` parameter for both use cases.

## Software updates

### Enable user proxy for software update scans
<!--8379199-->
Beginning with the September 2020 cumulative update, HTTP-based WSUS servers will be secure by default. A client scanning for updates against an HTTP-based WSUS will no longer be allowed to leverage a user proxy by default. If you still require a user proxy despite the security trade-offs, a new software updates client setting is available to allow these connections. For more information, see [September 2020 changes to improve security for Windows devices scanning WSUS](https://go.microsoft.com/fwlink/?linkid=2144403).

### Notifications for devices no longer receiving updates
<!--7520646-->
To help you manage security risk in your environment, you'll be notified in-console about devices with operating systems that are past the end of support date and that are no longer eligible to receive security updates. Additionally, a new **Management Insights** rule was added to detect Windows 7, Windows Server 2008, and Windows Server 2008 R2 without [Extended Security Updates (ESU)](https://support.microsoft.com/help/4497181/lifecycle-faq-extended-security-updates).

## PowerShell

### Support for PowerShell version 7

<!--6023299-->

The Configuration Manager [PowerShell cmdlet library](/powershell/sccm/overview) now offers support for PowerShell 7.

### Improvements to cloud management gateway cmdlets

<!--6978300-->

With more customers managing remote devices now, this release includes several new and improved Windows PowerShell cmdlets for the cloud management gateway (CMG). You can use these cmdlets to automate the creation, configuration, and management of the CMG service and Azure Active Directory (Azure AD) requirements.


<!-- Unused sections in this release:
## Reporting
## User experience
## Office management
## Co-management
-->

<!-- ## Deprecated operating systems

Learn about support changes before they're implemented in [removed and deprecated items](deprecated/removed-and-deprecated.md).

As first announced in version 1906, version 2010 drops support for the following client OS versions:  

- Windows CE 7.0
- Windows 10 Mobile
- Windows 10 Mobile Enterprise
 -->

## Other updates

<!--
Starting with this version, the following features are no longer [pre-release](../../servers/manage/pre-release-features.md):

### Azure Active Directory user group discovery](../../servers/deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco)<!--3611956
-->

For more information on changes to the Windows PowerShell cmdlets for Configuration Manager, see [PowerShell version 2010 release notes](/powershell/sccm/2010-release-notes).

For more information on changes to the administration service REST API, see [Administration service release notes](../../../develop/adminservice/release-notes.md).

<!--
Aside from new features, this release also includes additional changes such as bug fixes. For more information, see [Summary of changes in Configuration Manager current branch, version 2010](https://support.microsoft.com/help/4578830).

The following update rollup (4517869) is available in the console starting on October 1, 2019: [Update rollup for Configuration Manager current branch, version 1906](https://support.microsoft.com/help/4517869).

### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4580678](https://support.microsoft.com/help/4580678) | Tenant attach rollup for Configuration Manager current branch, version 2010 | September 18, 2020 | Yes |
| [4584759](https://support.microsoft.com/help/4584759) | Clients report Desktop Analytics configuration errors in Configuration Manager, version 2010 | October 2, 2020 | Yes |
<!--
> [!NOTE]  
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](../../servers/manage/updates.md#bkmk_supersede).
-->

## Next steps

At this time, version 2010 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-2010.md#early-update-ring).

<!-- 
As of August 31, 2020, version 2010 is globally available for all customers to install.
 -->

When you're ready to install this version, see [Installing updates for Configuration Manager](../../servers/manage/updates.md) and [Checklist for installing update 2010](../../servers/manage/checklist-for-installing-update-2010.md).

> [!TIP]
> To install a new site, use a baseline version of Configuration Manager.
>
> Learn more about:
>
> - [Installing new sites](../../servers/deploy/install/installing-sites.md)
> - [Baseline and update versions](../../servers/manage/updates.md#bkmk_Baselines)

For known significant issues, see the [Release notes](../../servers/deploy/install/release-notes.md).

After you update a site, also review the [Post-update checklist](../../servers/manage/checklist-for-installing-update-2010.md#post-update-checklist).
