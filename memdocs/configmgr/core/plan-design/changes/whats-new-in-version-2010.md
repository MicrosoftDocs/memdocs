---
title: What's new in version 2010
titleSuffix: Configuration Manager
description: Get details about changes and new capabilities introduced in version 2010 of Configuration Manager current branch.
ms.date: 03/09/2021
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: whats-new
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ROBOTS: NOINDEX
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# What's new in version 2010 of Configuration Manager current branch

*Applies to: Configuration Manager (current branch)*

Update 2010 for Configuration Manager current branch is available as an in-console update. Apply this update on sites that run version 1906 or later. <!-- baseline only statement:When installing a new site, it's also available as a baseline version. -->This article summarizes the changes and new features in Configuration Manager, version 2010.

Always review the latest checklist for installing this update. For more information, see [Checklist for installing update 2010](../../servers/manage/checklist-for-installing-update-2010.md). After you update a site, also review the [Post-update checklist](../../servers/manage/checklist-for-installing-update-2010.md#post-update-checklist).

To take full advantage of new Configuration Manager features, after you update the site, also update clients to the latest version. While new functionality appears in the Configuration Manager console when you update the site and console, the complete scenario isn't functional until the client version is also the latest.

## Microsoft Intune tenant attach

### Troubleshooting portal lists a user's devices based on usage
<!--6974300-->
The troubleshooting portal in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) allows you to search for a user and view their associated devices. Starting in this release, tenant attached devices that are assigned user device affinity automatically based on usage will now be returned when searching for a user.

For more information, see [Tenant attach: ConfigMgr client details in the admin center](../../../tenant-attach/client-details.md#bkmk_list).

### Enhancements to applications in Microsoft Intune admin center
<!--7979972, 8227649-->

We've made improvements to applications for tenant attached devices. Administrators can now do the following actions for applications in the Microsoft Intune admin center:

- **Uninstall** an application
- **Repair** installation of an application
- **Re-evaluate** the application installation status
- **Reinstall** an application has replaced **Retry installation**

For more information, see [Tenant attach: Install an application from the admin center](../../../tenant-attach/applications.md#bkmk_repair).

## Cloud-attached management

### Cloud management gateway with virtual machine scale set for CSP

<!--3601040-->

Cloud management gateway (CMG) deployments can now use a virtual machine scale set in Azure to support Cloud Solution Provider (CSP) subscriptions. This feature is currently pre-release. At this time, it's intended only for CSP customers that don't already have a CMG in another subscription.

For more information, see [CMG topology design: virtual machine scale sets](../../clients/manage/cmg/plan-cloud-management-gateway.md#virtual-machine-scale-sets).

### Disable Azure AD authentication for onboarded tenants

<!--8537319-->

You can now disable Azure Active Directory (Azure AD) authentication for tenants not associated with users and devices. When you onboard Configuration Manager to Azure AD, it allows the site and clients to use modern authentication. Currently, Azure AD device authentication is enabled for all onboarded tenants, whether or not it has devices. For example, you have a separate tenant with a subscription that you use for compute resources to support a cloud management gateway. If there aren't users or devices associated with the tenant, disable Azure AD authentication.

For more information, see [Configure Azure services](../../servers/deploy/configure/azure-services-wizard.md#disable-authentication).

<!-- ### Additional options when creating app registrations in Azure Active Directory
<!--7153654--
You can now specify **Never** for the expiration of a secret key when creating Azure Active Directory app registrations. For more information about creating app registrations, see [Configure Azure Services](../../servers/deploy/configure/azure-services-wizard.md#create-server-application-dialog).

remove per MEMDocs#1530
 -->

### Validate internet access for the service connection point

<!--8565578-->

If you use Desktop Analytics or tenant attach, the service connection point now checks important internet endpoints. These checks help make sure that the cloud-connected services are available. It also helps you troubleshoot issues by quickly determining if network connectivity is a problem.

For more information, see [About the service connection point](../../servers/deploy/configure/about-the-service-connection-point.md#validate-internet-access).

## Desktop Analytics

For more information on the monthly changes to the Desktop Analytics cloud service, see [What's new in Desktop Analytics](../../../desktop-analytics/whats-new.md).

### Support for new Windows 10 diagnostic data levels

<!--6979470-->

Microsoft is increasing transparency by categorizing the diagnostic data that Windows 10 collects:

- **Basic** diagnostic data is recategorized as **Required**
- **Full** is recategorized as **Optional**

If you previously configured devices for **Enhanced** or **Enhanced (Limited)**, in an upcoming release of Windows 10, they'll use the **Required** level. This change may impact the functionality of Desktop Analytics.

For more information, see [Enable data sharing](../../../desktop-analytics/enable-data-sharing.md#support-for-new-windows-10-diagnostic-data-levels).

### Support for Windows 10 Enterprise LTSC 2019

<!--6107649-->

The Windows 10 long-term servicing channel (LTSC) was designed for devices where functionality and features don't change over time. This servicing model prevents Windows 10 Enterprise LTSC devices from receiving the usual feature updates. It provides only quality updates to make sure that device security stays up to date. Some customers want to shift from LTSC to the semi-annual servicing channel, to have access to new features, services, and other major changes. You can now use Configuration Manager to enroll LTSC devices to Desktop Analytics. Once you enroll these devices, you can evaluate them in your deployment plans.

For more information, see [Desktop Analytics prerequisites](../../../desktop-analytics/overview.md#prerequisites)

## Site infrastructure

### Monitor scenario health

You can now use Configuration Manager to monitor the health of end-to-end scenarios. Monitoring scenario health enhances awareness of system latency and component backlogs which are critical for cloud service-attached features. Configuration Manager simulates activities to expose performance metrics and failure points. These synthetic activities are similar to methods that Microsoft uses to monitor some components in its cloud services. Use this additional data to better understand timeframes for activities. If failures occur, it can help focus your investigation.

This release includes the following two scenarios:

- **SQL Server Service Broker**: The service broker is a required configuration for the site database. Many of the core subsystems in Configuration Manager use the service broker.<!--7699463-->

- **Client action health**: Monitor the health of the fast channel used for client actions. If your environment is tenant attached with devices uploaded, this feature helps you see potential issues with client actions from the Microsoft Intune admin center. You can also use this feature for on-premises client actions. For example, CMPivot, run scripts, and device wake-up.<!--7699511-->

For more information, see [Monitor scenario health](../../servers/manage/scenario-health.md).

### Report setup and upgrade failures to Microsoft
<!--5622909-->
If the setup or update process fails to complete successfully, you can now report the error directly to Microsoft. If a failure occurs, the **Report update error to Microsoft** button is enabled. When you use the button, an interactive wizard opens allowing you to provide more information to us. In technical previews, this button is always enabled even when the setup completes successfully.

For more information, see [Install in-console updates](../../servers/manage/post-in-console-updates.md#report-setup-and-upgrade-failures-to-microsoft).

### Delete Aged Collected Diagnostic Files task
<!--6503308-->
You now have a new maintenance task available for cleaning up collected diagnostic files. **Delete Aged Collected Diagnostic Files** uses a default value of 14 days when it looks for diagnostic files to clean up. This task doesn't affect regular collected files. The new maintenance task is enabled by default.

For more information, see the following articles:

- Client diagnostic section of the [Client notification](../../clients/manage/client-notification.md#cleanup-aged-client-diagnostic-files) article
- [Reference for maintenance tasks in Configuration Manager](../../servers/manage/reference-for-maintenance-tasks.md#delete-aged-collected-diagnostic-files).

### Improvements to the administration service

<!-- 8613105 -->

The Configuration Manager REST API, the administration service, requires a secure HTTPS connection. With the previous methods to enable HTTPS, enabling IIS on the SMS Provider was a prerequisite.

Starting in this release, you no longer need to enable IIS on the SMS Provider for the administration service. When you enable the site for enhanced HTTP, it creates a self-signed certificate for the SMS Provider, and automatically binds it without requiring IIS.

For more information, see [Prerequisites for the administration service](../../../develop/adminservice/overview.md#prerequisites).

### Improvements to the Azure migration tool

<!-- 7812857 -->

The tool to extend and migrate an on-premises site to Microsoft Azure now includes the following improvements:

- Support environments with virtual networks other than ExpressRoute
- Support a hierarchy
- Support a site with a collocated site database

For more information, see [Extend and migrate on-premises site to Microsoft Azure](../../support/azure-migration-tool.md).

## Client management

### Wake machine at deployment deadline using peer clients on the same remote subnet
<!--3734819-->

Wake on LAN (WoL) has always posed a problem in complex, subnetted networks. Good networking best practice reduces the size of broadcast domains to mitigate against the risk of broadcast traffic adversely affecting the network. The most common way to limiting network broadcast is by not allowing broadcast packets to be routed between subnets. Another option is to enable subnet directed broadcasts but most organizations don't allow the magic packet to traverse internal routers.

In version 1810, the introduction of peer wake-up allowed an administrator to wake a device or collection of devices, on demand using the client notification channel. Overcoming the need for the server to be in the same broadcast domain as the client.

This latest improvement allows the Configuration Manager site to wake devices at the deadline of a deployment. Instead of the site server issuing the magic packet directly, the site uses the client notification channel. It finds an online machine in the last known subnet of the target device. It then instructs the online client to issue the WoL packet for the target device.

For more information, see [How to configure Wake on LAN](../../clients/deploy/configure-wake-on-lan.md#bkmk_deadline).

### Improved Windows Server restart experience for non-administrator accounts

<!--7821529-->

For a low-rights user on a device that runs Windows Server, by default they aren't assigned the user rights to restart Windows. When you target a deployment to this device, this user can't manually restart. For example, they can't restart Windows to install software updates.

Starting in this release, you can now control this behavior as needed. In the **Computer Restart** group of client settings, enable the following setting: **When a deployment requires a restart, allow low-rights users to restart a device running Windows Server**.

For more information, see [Device restart notifications: Client settings](../../clients/deploy/device-restart-notifications.md#client-settings).

## Collections

### Collection query preview
<!--7380401-->
You can now preview the query results when you're creating or editing a query for collection membership. Preview the query results from the query statement properties dialog. When you select **Edit Query Statement**, select the green triangle on the query properties for the collection to show the **Query Results Preview** window. Select **Stop** if you want to stop a long running query.

For more information, see [Configure a query rule](../../clients/manage/collections/create-collections.md#bkmk-query).

### Collection evaluation view
<!--6251274-->
We've integrated the functionality of Collection Evaluation Viewer into the Configuration Manager console. This change provides administrators a central location to view and troubleshoot the collection evaluation process.

For more information, see [Collection evaluation view](../../clients/manage/collections/collection-evaluation-view.md).

### View collection relationships

<!--3608121-->

You can now view dependency relationships between collections in a graphical format. It shows limiting, include, and exclude relationships.

:::image type="content" source="media/3608121-view-dependent-relationships.png" alt-text="View collection dependency relationships in a graphical format" lightbox="media/3608121-view-dependent-relationships.png":::

If you want to change or delete collections, view the relationships to understand the impact of the proposed change. Before you create a deployment, look at the potential target collection for any include or exclude relationships that might affect the deployment.

For more information, see [How to manage collections](../../clients/manage/collections/manage-collections.md).

## Application management

### Improvements to available apps via CMG

<!--7033501-->
An internet-based, domain-joined device that isn't joined to Azure Active Directory (Azure AD) and communicates via a cloud management gateway (CMG) can now get apps deployed as available. The Active Directory domain user of the device needs a matching Azure AD identity. When the user starts Software Center, Windows prompts them to enter their Azure AD credentials. They can then see any available apps.

For more information, see [Prerequisites to deploy user-available applications](../../../apps/plan-design/prerequisites-deploy-user-available-apps.md).

## OS deployment

### Deploy an OS over CMG using bootable media

<!--3555923-->

Starting in current branch version 2006, the cloud management gateway (CMG) supported running a task sequence with a boot image when you start it from Software Center. With this release, you can now use bootable media to reimage internet-based devices that connect through a CMG. This scenario helps you better support remote workers. If Windows won't start so that the user can access Software Center, you can now send them a USB drive to reinstall Windows.

For more information on this scenario and other related scenarios, see the new article to [Deploy a task sequence over the internet](../../../osd/deploy-use/deploy-task-sequence-over-internet.md#deploy-an-os-over-cmg-using-bootable-media).

### Deploy a task sequence deployment type to a user collection

<!--8018255-->

You can now deploy an application with a task sequence deployment type to a user-based collection. A user-targeted deployment still runs in the context of the local System account.

For more information, see [Task sequence deployment type](../../../apps/get-started/creating-windows-applications.md#bkmk_tsdt).

### Manage task sequence size

Large task sequences cause problems with client processing. To further help manage the size of task sequences, this release continues to iterate on improvements.

- Starting in this release Configuration Manager restricts actions for a task sequence that's greater than 2 MB in size. For example, the task sequence editor will display an error if you try to save changes to a large task sequence.<!--6888853-->

- When you view the list of task sequences in the Configuration Manager console, add the **Size (KB)** column. Use this column to identify large task sequences that can cause problems.<!--7645732-->

For more information, see [Reduce the size of task sequence policy](../../../osd/deploy-use/reduce-task-sequence-policy-size.md).

### Analyze SetupDiag errors for feature updates

<!--4385028-->

With the release of Windows 10, version 2004, the [SetupDiag](/windows/deployment/upgrade/setupdiag) diagnostic tool is included with Windows Setup. If there's an issue with the upgrade, SetupDiag automatically runs to determine the cause of the failure. Configuration Manager now gathers and summarizes SetupDiag results from feature update deployments with Windows 10 servicing.

For more information, see [Manage Windows as a service](../../../osd/deploy-use/manage-windows-as-a-service.md#analyze-setupdiag-errors).

### Improvements to task sequence performance settings

<!--7721999 & 8177793-->
Starting in Configuration Manager version 1910, to improve the overall speed of the task sequence, you could activate the Windows power plan for **High Performance**. Starting in this release, you can now use this option on devices with [modern standby](/windows-hardware/design/device-experiences/modern-standby) and other devices that don't have that default power plan.

For more information, see [Task sequence performance](../../../osd/deploy-use/task-sequence-performance.md).

## Protection

### Improvements to BitLocker management

<!--6979223-->

You can now manage BitLocker policies and escrow recovery keys over a cloud management gateway (CMG). This change also provides support for BitLocker management via internet-based client management (IBCM). There's no change to the setup process for BitLocker management. This improvement supports domain-joined and hybrid domain-joined devices.

For more information, see [Plan for BitLocker management](../../../protect/plan-design/bitlocker-management.md).

### Expanded Windows Defender Application Control management
<!--7752243-->
Windows Defender Application Control enforces an explicit list of software allowed to run on devices. In this release, we've expanded Windows Defender Application Control policies to support devices running Windows Server 2019 or later.

For more information, see [Windows Defender Application Control management with Configuration Manager](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md#bkmk_os).

## Software updates

### Enable user proxy for software update scans
<!--8379199-->
Beginning with the September 2020 cumulative update, HTTP-based WSUS servers will be secure by default. By default, a client that scans for updates against an HTTP-based WSUS can't use a user proxy. If you still require a user proxy despite the security trade-offs, a new software updates client setting is available to allow these connections. For more information about the changes for scanning WSUS, see [September 2020 changes to improve security for Windows devices scanning WSUS](https://techcommunity.microsoft.com/t5/windows-it-pro-blog/changes-to-improve-security-for-windows-devices-scanning-wsus/ba-p/1645547). To make sure that the best security protocols are in place, use the TLS protocol. This protocol helps to [secure your software update infrastructure](../../../sum/get-started/software-update-point-ssl.md).

For more information about enabling a proxy for software update scans, see [Client settings for software updates](../../clients/deploy/about-client-settings.md#software-updates).

### Notifications for devices no longer receiving updates
<!--7520646-->
To help you manage security risk in your environment, you'll be notified in-console about devices with operating systems that are past the end of support date. These devices may no longer receive security updates. Additionally, a new **Management Insights** rule was added to detect Windows 7, Windows Server 2008, and Windows Server 2008 R2 without [Extended Security Updates (ESU)](https://support.microsoft.com/help/4497181/lifecycle-faq-extended-security-updates).

For more information, see [Management insights](../../servers/manage/management-insights.md#security) and [Console notifications](../../servers/manage/admin-console-notifications.md#bkmk_2010).

### Immediate distribution point fallback for clients downloading software update delta content
<!--8286432-->
There's a new client setting for software updates. If delta content is unavailable from distribution points in the current boundary group, you can allow immediate fallback to a neighbor or the site default boundary group distribution points. This setting is useful when using delta content for software updates since the timeout setting per download job is five minutes.

For more information, see [Client settings for software updates](../../clients/deploy/about-client-settings.md#software-updates).

## Configuration Manager console

### Categorize Community hub content
<!--8052494-->
Community hub content is grouped into a Microsoft, curated, or unreviewed category to allow admins to choose the types of content their environment displays. Admins can choose from the different categories of content that are provided in the Community hub to match their risk profile and their willingness to share and use content from those outside Microsoft and outside their own company.

For more information, see [Community hub](../../servers/manage/community-hub.md#bkmk_category).

### Community hub on Windows Server operating systems
<!--3555940, 8625943, 8717639 -->
You can now display the Community hub on Windows Server operating systems. The Configuration Manager console will notify you to install the console extension to enable Windows Server 2012 and later to load the Community hub.

For more information, see [Community hub](../../servers/manage/community-hub.md#bkmk_webview2).

### Product feedback

<!--3180826-->

The Configuration Manager console has a new wizard for sending feedback. The redesigned wizard improves the workflow with better guidance about how to submit good feedback.

:::image type="content" source="media/3180826-send-a-smile-2010.png" alt-text="Send a smile product feedback wizard" lightbox="media/3180826-send-a-smile-2010.png":::

There's also a new status message query, **Feedback sent to Microsoft**. Use this query to easily find feedback status messages.<!--6488450-->

For more information, see [Product feedback](../../understand/product-feedback.md).

### Improvements to in-console notifications
<!--7410221-->
You now have an updated look and feel for in-console notifications. Notifications are more readable and the action link is easier to find. Additionally, the age of the notification is displayed to help you find the latest information. If you dismiss or snooze a notification, that action is now persistent for your user across consoles.

For more information, see [Improvements to Configuration Manager console notifications](../../servers/manage/admin-console-notifications.md#bkmk_2010).

### Improvements to the Configuration Manager console

- You can now copy discovery data from devices and users in the console. Copy the details to the clipboard, or export them all to a file. These new actions make it easier for you to quickly get this data from the console. For example, copy the MAC address of a device before you reimage it.<!--6890051-->

- Various areas in the Configuration Manager console now use the fixed-width font Consolas. This font provides consistent spacing and makes it easier to read.<!--7632637-->

- You now have an easier way to view status messages for objects. Select an object in the Configuration Manager console, and then select **Show Status Messages** from the ribbon.<!--8232705-->

- Now when you import an object in the Configuration Manager console, it imports to the current folder. Previously, Configuration Manager always put imported objects in the root node. This new behavior applies to applications, packages, driver packages, and task sequences.<!--6601203-->

- To assist you when creating scripts and queries in the Configuration Manager console, you'll now see syntax highlighting and code folding, where available.<!--7964912-->

For more information, see [Configuration Manager console changes and tips](../../servers/manage/admin-console-tips.md).

## Content management

### Improvements to client data sources dashboard

<!--7102084-->

The client data sources dashboard now offers an expanded selection of filters to view information about where clients get content. These new filters include:

- Single boundary group
- All boundary groups
- Internet clients
- Clients not associated with a boundary group

The dashboard also includes a new tile for **Content downloads using fallback source**. This information helps you understand how often clients download content from an alternate source.

:::image type="content" source="media/7102084-client-data-sources.png" alt-text="Client data sources dashboard" lightbox="media/7102084-client-data-sources.png":::

For more information, see [Monitor content: Client Data Sources dashboard](../../servers/deploy/configure/monitor-content-you-have-distributed.md#client-data-sources-dashboard).

### Improvements to the content library cleanup tool

<!--6887878-->

If you remove content from a distribution point while the site system is offline, an orphaned record can exist in WMI. Over time, this behavior can eventually lead to a warning status on the distribution point. To mitigate the issue in the past, you had to manually remove the orphaned entries from WMI. The content library cleanup tool in delete mode can now remove these orphaned content records from WMI.

For more information, see the [Content library cleanup tool](../hierarchy/content-library-cleanup-tool.md).

## PowerShell

### Update PowerShell help

<!--7774961-->

You can now use the [Update-Help](/powershell/module/microsoft.powershell.core/update-help) cmdlet to get the latest information for the Configuration Manager PowerShell module. This content is the same as what's published for the [ConfigurationManager module](/powershell/module/configurationmanager/).

For more information, see [Configuration Manager PowerShell cmdlets: Update help](/powershell/sccm/overview#update-help).

> [!WARNING]
> Because of a change in how the updateable content is structured and published with the release of version 2103, don't use **Update-Help** on a version 2010 site. Update the site to version 2103, and then update the local help content.<!-- 8617455 -->
>
> For more information, see [PowerShell version 2103 release notes](/powershell/sccm/2103-release-notes#known-issue-with-updateable-powershell-help).

### Support for PowerShell version 7

<!--6023299-->

The Configuration Manager PowerShell cmdlet library now offers support for PowerShell 7. For more information, see [Get started with Configuration Manager cmdlets](/powershell/sccm/overview).

### Improvements to cloud management gateway cmdlets

<!--6978300-->

With more customers managing remote devices now, this release includes several new and improved Windows PowerShell cmdlets for the cloud management gateway (CMG). You can use these cmdlets to automate the creation, configuration, and management of the CMG service and Azure Active Directory (Azure AD) requirements.

For more information, see [Configuration Manager version 2010 PowerShell release notes](/powershell/sccm/2010-release-notes).

<!-- Unused sections in this release:
## Endpoint analytics
## Reporting
## User experience
## Office management
## Co-management
## Real-time management
-->

## Deprecated features

Learn about support changes before they're implemented in [removed and deprecated items](deprecated/removed-and-deprecated.md).

The following features are now deprecated:

- The [collection evaluation viewer](../../support/ceviewer.md)<!-- 8509484 -->
- [Connector for Azure Monitor](/azure/azure-monitor/platform/collect-sccm?context=%2fmem%2fconfigmgr%2fcore%2fcontext%2fcore-context)<!-- 8269855 -->

<!--
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

For more information on changes to the Windows PowerShell cmdlets for Configuration Manager, see [version 2010 release notes](/powershell/sccm/2010-release-notes).

<!-- For more information on changes to the administration service REST API, see [Administration service release notes](../../../develop/adminservice/release-notes.md). -->

Aside from new features, this release also includes additional changes such as bug fixes. For more information, see [Summary of changes in Configuration Manager current branch, version 2010](https://support.microsoft.com/help/4599442).

<!--
The following update rollup (4517869) is available in the console starting on October 1, 2019: [Update rollup for Configuration Manager current branch, version 1906](https://support.microsoft.com/help/4517869).
-->
### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4594177](https://support.microsoft.com/help/4594177) | Client notifications sent to all collection members in Configuration Manager current branch, version 2010 | January 12, 2021 | Yes |
| [4600089](https://support.microsoft.com/help/4600089)| Update Rollup for Microsoft Endpoint Configuration Manager current branch, version 2010 | March 8, 2021| Yes|

<!--
> [!NOTE]  
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](../../servers/manage/updates.md#bkmk_supersede).
-->

## Next steps

<!-- At this time, version 2010 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-2010.md#early-update-ring).
 -->

As of December 11, 2020, version 2010 is globally available for all customers to install.

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
