---
title: What's new in version 2107
titleSuffix: Configuration Manager
description: Get details about changes and new capabilities introduced in version 2107 of Configuration Manager current branch.
ms.date: 10/05/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# What's new in version 2107 of Configuration Manager current branch

*Applies to: Configuration Manager (current branch)*

Update 2107 for Configuration Manager current branch is available as an in-console update. Apply this update on sites that run version 2002 or later. <!-- baseline only statement: When installing a new site, it will also be available as a [baseline version](../../servers/manage/updates.md#bkmk_note1) soon after global availability.--> This article summarizes the changes and new features in Configuration Manager, version 2107.

> [!NOTE]
> To better align with other releases within Microsoft Endpoint Manager, starting this year the current branch version names will be 2103, 2107, and 2111. They will still release every four months, and release at the same time of the year.

Always review the latest checklist for installing this update. For more information, see [Checklist for installing update 2107](../../servers/manage/checklist-for-installing-update-2107.md). After you update a site, also review the [Post-update checklist](../../servers/manage/checklist-for-installing-update-2107.md#post-update-checklist).

To take full advantage of new Configuration Manager features, after you update the site, also update clients to the latest version. While new functionality appears in the Configuration Manager console when you update the site and console, the complete scenario isn't functional until the client version is also the latest.

## Cloud-attached management

### Cloud attach your environment during site update
<!-- 9563659,7958749-->

The Microsoft Intune family of products is an integrated solution for managing all of your devices. Cloud attach brings together Configuration Manager and Intune into a single console called **Microsoft Intune admin center**. Starting with this release, sites that aren't already onboarded to Microsoft Intune will be prompted to optionally cloud attach as part of the upgrade wizard. Environments are considered cloud attached if at least one of the following features are already enabled:

- [Tenant attach](../../../tenant-attach/device-sync-actions.md)
- [Co-management](../../../comanage/overview.md)
- [Endpoint analytics](../../../../analytics/enroll-configmgr.md)

For more information, see [Install in-console updates](../../servers/manage/install-in-console-updates.md).

### Convert a CMG to virtual machine scale set

<!--8959690-->

Starting in current branch version 2010, you could deploy the cloud management gateway (CMG) with a virtual machine scale set in Azure. This support was primarily to unblock customers with a Cloud Solution Provider (CSP) subscription.

In this release, any customer with a CMG that uses the classic cloud service deployment can convert to a virtual machine scale set. Microsoft recommends that new CMG deployments use a virtual machine scale set.

For more information, see [Plan for CMG: virtual machine scale set](../../clients/manage/cmg/plan-cloud-management-gateway.md#virtual-machine-scale-sets) and [Modify a CMG: Convert](../../clients/manage/cmg/modify-cloud-management-gateway.md#convert).

### Select VM size for CMG

<!--3555749-->

When you deploy a CMG with a virtual machine scale set, you can now choose the virtual machine (VM) size. The following three options are available:

- Lab (B2s)
- Standard (A2_v2). This size continues to be the default setting.
- Large (A4_v2)

This control gives you greater flexibility with your CMG deployment. You can adjust the size for test labs or if you support large environments. For example, the smaller **Lab** size is ideal for testing with a smaller number of clients at less cost. For production deployments, either use the default **Standard** size or add more capacity with the **Large** size.

For more information, see [Cost of CMG: Virtual machine scale set](../../clients/manage/cmg/cost.md#virtual-machine-scale-set).

### Tenant attach: BitLocker recovery keys

<!--6979225-->

Get BitLocker recovery keys for a tenant-attached device from the Microsoft Intune admin center. For example, a help desk technician who doesn't have access to Configuration Manager could use the web-based admin center to help an end user get a recovery key for their device.

For more information, see [Tenant attach: BitLocker recovery keys](../../../tenant-attach/bitlocker-recovery-keys.md).

### Tenant attach support for US Government cloud

<!-- 8353823 -->

United States Government customers can now use the following Microsoft Intune tenant attach features in the US Government cloud:

- Account onboarding
- Tenant sync to Intune
- Device sync to Intune
- Device actions in the Microsoft Intune admin center

For more information, see [Microsoft Intune tenant attach: Prerequisites](../../../tenant-attach/prerequisites.md).

### Renamed Co-management node to Cloud Attach
<!--10158821, 10115058-->
To better reflect the other cloud services that Configuration Manager offers, the **Co-management** node has been renamed to the **Cloud Attach** node. Other changes you may notice include the ribbon button being renamed from **Configure Co-management**  to **Configure Cloud Attach** and the **Co-management Configuration Wizard** was renamed to **Cloud Attach Configuration Wizard**.

For more information, see [Co-management](../../../comanage/overview.md), [Tenant attach](../../../tenant-attach/device-sync-actions.md), and [Endpoint analytics](../../../../analytics/enroll-configmgr.md).

## Desktop Analytics

### Support for the Windows diagnostic data processor configuration

<!-- 10220671 -->

Desktop Analytics now supports the new [Windows diagnostic data processor configuration](/windows/privacy/changes-to-windows-diagnostic-data-collection#new-windows-diagnostic-data-processor-configuration). This configuration provides you greater control of your Windows diagnostic data. Microsoft acts as a data processor, processing Windows diagnostic data for the controller.

For more information, see [What's new in Desktop Analytics](../../../desktop-analytics/whats-new.md).

## Site infrastructure

### Support for Windows Server 2022 and the ADK for Windows 11

<!-- 10200029 -->
Configuration Manager now supports Windows Server 2022 as site systems and clients. For more information, see the following articles:

- [Supported operating systems for site system servers](../configs/supported-operating-systems-for-site-system-servers.md)
- [Supported OS versions for clients](../configs/supported-operating-systems-for-clients-and-devices.md)
- [Upgrade on-premises infrastructure](../../servers/manage/upgrade-on-premises-infrastructure.md)

It also supports the Windows ADK for Windows 11 and Server 2022. For more information, see [Support for Windows ADK](../configs/support-for-windows-adk.md).

> [!TIP]
> Configuration Manager supports [Windows Insider builds](../configs/support-for-windows-11.md#support-for-windows-insider), which is a great way to test the latest version of Windows 11 with Configuration Manager version 2107.

### Microsoft .NET requirements

<!--10402814-->

Configuration Manager now requires Microsoft .NET Framework version 4.6.2 for site servers, specific site systems, clients, and the console. Before you run setup to install or update the site, first update .NET and restart the system. If possible in your environment, install the latest version of .NET version 4.8.

There's also a new [management insight](../../servers/manage/management-insights.md) to recommend site systems that don't yet have .NET version 4.8 or later.

For more information, see the following articles:

- [Site and site system prerequisites](../configs/site-and-site-system-prerequisites.md#net-version-requirements)
- [Prerequisites for deploying clients to Windows computers](../../clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md#more-details-about-microsoft-net)
- [Install the Configuration Manager console](../../servers/deploy/install/install-consoles.md#net-version-requirements)

### Updated Visual C++ prerequisite

<!--5170229-->

The Configuration Manager client and several server components require the Microsoft Visual C++ Redistributable component (`vcredist_x*.exe`). During Configuration Manager installation, if the VCRedist doesn't already exist, it automatically installs. Starting in this release, Configuration Manager now uses the Microsoft Visual C++ 2015-2019 redistributable version 14.28.29914.0. This version improves stability in Configuration Manager operations.

For more information on client and site system prerequisites, see the following articles:

- [Prerequisites for deploying clients to Windows computers](../../clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md#components-automatically-downloaded-during-installation)
- [Site and site system prerequisites](../configs/site-and-site-system-prerequisites.md)

### New prerequisite check for SQL Server 2012

<!--10092858-->

When you install or update the site, it now warns for the presence of SQL Server 2012. The [support lifecycle](/lifecycle/products/microsoft-sql-server-2012) for SQL Server 2012 ends on July 12, 2022. Plan to upgrade database servers in your environment, including SQL Server Express at secondary sites.

For more information, see [Removed and deprecated for site servers: SQL Server](deprecated/removed-and-deprecated-server.md#sql-server).

### External notifications

<!--9504414-->

In a complex IT environment, you may have an automation system like [Azure Logic Apps](/azure/logic-apps/logic-apps-overview). Customers use these systems to define and control automated workflows to integrate multiple systems. You could integrate Configuration Manager into a separate automation system through the product's SDK APIs. But this process can be complex and challenging for IT professionals without a software development background.

You can now enable the site to send notifications to an external system or application. This feature simplifies the process by using a web service-based method. You configure subscriptions to send these notifications. These notifications are in response to specific, defined events as they occur. For example, status message filter rules.

For more information, see [External notifications](../../servers/manage/external-notifications.md).

### Internet access requirements

<!--9791281,10237384-->

Before you update to version 2107, if you restrict internet access, confirm that the site system that hosts the service connection point role can communicate with the following internet endpoint: `configmgrbits.azureedge.net`. This endpoint was already required, but its use is expanded in this release. The site system can't download version 2107 or later unless your network allows traffic to this URL.

For more information, see [internet access requirements](../../plan-design/network/internet-endpoints.md#service-connection-point) for the service connection point.

## Real-time management

### Simplified CMPivot permissions requirements
<!--7898885-->
We've simplified the CMPivot permissions requirements. The new permissions are applicable for CMPivot standalone and CMPivot in the on-premises console. The following changes have been made:

- CMPivot no longer requires **SMS Scripts** read permission

  - The [SMS Provider](../hierarchy/plan-for-the-sms-provider.md) still requires this permission if the [administration service](../../../develop/adminservice/overview.md) falls back to it because of a 503 (Service Unavailable) error, as seen in the CMPivot.log.

- The **default scope** permission isn't required.

For more information, see [permissions for CMPivot](../../servers/manage/cmpivot.md#permissions).

### Improvements to CMPivot

<!--9966861-->
We've made the following improvements to CMPivot:

- Added a Key value to the [Registry entity](../../servers/manage/cmpivot-overview.md#bkmk_onprem_only)
- Added a new RegistryKey entity that returns all registry keys matching the given expression
- Added [maxif](/azure/data-explorer/kusto/query/maxif-aggfunction) and [minif](/azure/data-explorer/kusto/query/minif-aggfunction) aggregators that can be used with the [summarize operator](../../servers/manage/cmpivot-overview.md#table-operators)
- Improvements to query autocomplete suggestions in the query editor

For more information, see [Changes to CMPivot](../../servers/manage/cmpivot-changes.md#bkmk_2107) and [CMPivot overview](../../servers/manage/cmpivot-overview.md#bkmk_onprem_only).

## Client management

### Support for Windows 11

<!-- 10589866 -->

Starting with version 2107, Configuration Manager supports Windows 11. For more information, see [Support for Windows 11](../configs/support-for-windows-11.md).

### Custom properties for devices

<!--8939867-->

Many customers have other data that's external to Configuration Manager but useful for deployment targeting, collection building, and reporting. This data is typically non-technical in nature, not discoverable on the client, and comes from a single external source. For example, a central IT Infrastructure Library (ITIL) system or asset database, which has some of the following device attributes:

- Physical location
- Organizational priority
- Category
- Cost center
- Department

You can use the administration service to set this data on devices. The site stores the property's name and its value in the site database as the new **Device Custom Properties** class. You can then use the custom properties in Configuration Manager for reporting or to create collections.

For more information, see [Custom properties for devices](../../../develop/adminservice/custom-properties.md).

### Client encryption uses AES-256

<!--10129759-->

Starting in this release, when you enable the site to **Use encryption**, the client uses the **AES-256** algorithm. This setting requires clients to encrypt inventory data and state messages before it sends to the management point.

For more information, see [Cryptographic controls technical reference](../security/cryptographic-controls-technical-reference.md).

### Clients store Configuration Manager self-signed certificates in hardware TPM

<!--9217033-->

Configuration Manager uses self-signed certificates for client identity and to help protect communication between the client and site systems. When you update the site and clients to version 2107, the client stores its certificate from the site in a hardware-bound key storage provider (KSP). This KSP is typically the trusted platform module (TPM) at least version 2.0. The certificate is also marked non-exportable.

If the client also has a PKI-based certificate, it continues to use that certificate for TLS HTTPS communication. It uses its self-signed certificate for signing messages with the site.

For more information, see [Certificates overview](../security/certificates-overview.md#hardware-bound-key-storage-provider).

### Hardware inventory for client log settings

<!--5602449-->

You can now inventory client log file settings such as log levels and size. This behavior allows you to track settings that you change by the [Client Diagnostics](../../clients/manage/client-notification.md#client-diagnostics) actions. This new inventory class isn't enabled by default.

For more information, see [About log files](../hierarchy/about-log-files.md#hardware-inventory-for-client-log-settings).

### Support for macOS Big Sur

<!-- 8816608 -->

Configuration Manager now supports the macOS Big Sur version 11. For more information, see [Supported OS versions for clients and devices](../configs/supported-operating-systems-for-clients-and-devices.md#mac-computers).

## Software Center

### Support for enhanced HTTP

<!-- 9199146 -->

When you enable the site for [enhanced HTTP](../hierarchy/enhanced-http.md), Software Center and the Company Portal now prefer secure communication over HTTPS to get user-available applications from the management point.

For more information, see [Plan for Software Center](../../../apps/plan-design/plan-for-software-center.md) and [Use the Company Portal app on co-managed devices](../../../comanage/company-portal.md).

## Application management

### Implicit uninstall of applications

<!--3607457-->

Many customers have lots of collections because for every application they need at least two collections: one for install and another for uninstall. This practice adds overhead of managing more collections, and can reduce site performance for collection evaluation.

Starting in this release, you can enable an application deployment to support implicit uninstall. If a device is in a collection, the application installs. Then when you remove the device from the collection, the application uninstalls.

For more information, see [Uninstall applications](../../../apps/deploy-use/uninstall-applications.md).

## OS deployment

### Support layered keyboard driver during OS deployment

<!--9735002-->

This release adds support for layered keyboard drivers during OS deployment. This driver specifies other types of keyboards that are common with Japanese and Korean languages.

For more information, see [Task sequence steps - Apply OS Image](../../../osd/understand/task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).

## Protection

### Audit mode for potentially unwanted applications
<!--9249870-->

An **Audit** option for [potentially unwanted applications (PUA)](/microsoft-365/security/defender-endpoint/detect-block-potentially-unwanted-apps-microsoft-defender-antivirus) was added in the **Antimalware policy** settings. Use PUA protection in audit mode to detect potentially unwanted applications without blocking them. PUA protection in audit mode is useful if your company is conducting an internal software security compliance check and you'd like to avoid any false positives.

For more information, see [real-time protection settings](../../../protect/deploy-use/endpoint-antimalware-policies.md#real-time-protection-settings).

## Software updates

### Run software updates evaluation from deployment status
<!--9012080 -->

You can now right-click and notify devices to run a software updates evaluation cycle from the [software update deployment status](../../../sum/deploy-use/monitor-software-updates.md#BKMK_SUDeployStatus). You can target a single device under the **Asset Details** pane or select a group of devices based on their deployment status.

For more information, see [Configuration Manager console changes and tips](../../servers/manage/admin-console-tips.md).

### Management insights rule for TLS/SSL software update points

<!--7470529-->

[Management insights](../../servers/manage/management-insights.md) has a new rule to detect if your software update points are [configured to use TLS/SSL](../../../sum/get-started/software-update-point-ssl.md). To review the **Configure software update points to use TLS/SSL** rule, go to **Administration** > **Management Insights** > **All Insights** > **Software Updates**.

For more information, see the [Management insights software updates group](../../servers/manage/management-insights.md#software-updates).

### List third-party update catalogs
<!--9989251-->
To help you find custom catalogs that you can import for third-party software updates, there's now a documentation page with links to catalog providers. Choose **More Catalogs** from the ribbon in the **Third-party software update catalogs** node. Right-clicking on **Third-Party Software Update Catalogs** node also displays a **More Catalogs** menu item.  Selecting **More Catalogs** opens a link to a documentation page containing a list of third-party software update catalog providers.

For more information, see [Third-party software updates](../../../sum/deploy-use/third-party-software-updates.md#bkmk_list-catalogs) and [list of third-party software update catalog providers](../../../sum/deploy-use/third-party-software-update-catalogs.md).

### Improvements for managing automatic deployment rules

The following items were added to help you better manage your automatic deployment rules (ADRs):

#### Deployment types for automatic deployment rules
<!--9900107, 7033498-->
You can now specify the deployment type for the software update deployment created by an ADR. Select **Required** to create a mandatory software update deployment or select **Available** to create an optional software update deployment.

For more information, see [Create an automatic deployment rule](../../../sum/deploy-use/automatically-deploy-software-updates.md#BKMK_CreateAutomaticDeploymentRule).

#### Updated Product parameter for New-CMSoftwareUpdateAutoDeploymentRule cmdlet
<!--9247522-->
The `-Product` parameter for `New-CMSoftwareUpdateAutoDeploymentRule` was updated. When there are multiple products with the same name, `-Product` now selects all of them.

#### Script to apply deployment package settings for automatic deployment rule
<!--3961933, 4396422-->
If you create an ADR with the **No deployment package** option, you're unable to go back and add one later. To help you resolve this issue, we've uploaded a script into [Community hub](../../servers/manage/community-hub.md).

For more information, see [Automatic deployment rules](../../../sum/deploy-use/automatically-deploy-software-updates.md#bkmk_script).


## Community hub

### Publish query to Community hub from CMPivot
<!--9965423-->
You can now publish a CMPivot query to the Community hub directly from the CMPivot window. Submitting your queries directly through CMPivot makes contributing to the Community hub easier.

For more information, see [Contribute to Community hub](../../servers/manage/community-hub-contribute.md#bkmk_publish) and [CMPivot](../../servers/manage/cmpivot.md#bkmk_publish).

### Support for console extensions in Community hub

When you use Configuration Manager version 2103 or later, you can now download console extensions from the [Community hub](../../servers/manage/community-hub.md) and have it applied to all consoles connected to a hierarchy. Manage the approval and installation of console extensions used in your environment from the **Console extensions** node.

For more information, see [Console extensions from Community hub](../../servers/manage/community-hub-extensions.md).

## Configuration Manager console

### Enhanced code editor
<!--8495588-->
Building on improvements in Configuration Manager 2010 for [syntax highlighting and code folding](../../servers/manage/admin-console-tips.md#bkmk_syntax), you can now edit scripts in an enhanced editor. The new editor supports syntax highlighting, code folding, word wrap, line numbers, and find and replace. The new editor is available in the console wherever scripts and queries can be viewed or edited.

For more information, see the [enhanced code editor](../../servers/manage/admin-console-tips.md#bkmk_code).

### Send product feedback from error windows

<!--4262917-->

Previously, if the Configuration Manager console reported an error in a separate window, you had to go back to the main console window to send feedback. In some cases, this action isn't possible with other console windows open.

Starting in this release, error messages include a link to **Report error to Microsoft**. This action opens the standard "send a frown" window to provide feedback. It automatically includes details about the user interface and the error to better help Microsoft engineers diagnose the error. Aside from making it easier to send a frown, it also lets you include the full context of the error message when you share a screenshot.

For more information, see [Product feedback](../../understand/product-feedback.md).

### Hierarchy approved console extensions don't require signing
<!--9761129-->
Starting in this release, you can choose to allow unsigned [hierarchy approved console extensions](../../servers/manage/admin-console-extensions.md). You may need to allow unsigned console extensions because of an unsigned internally developed extension, or for testing your own custom extension in a lab.

For more information, see [Allow unsigned console extensions in the hierarchy](../../servers/manage/admin-console-extensions.md#bkmk_allow-unsigned).

### Console improvements
<!--9575773-->
In this release we've made the following improvements to the Configuration Manager console:

- Status message shortcuts<!--8942963-->: Shortcuts to [status messages](../../servers/manage/use-status-system.md) were added to the **Administrative Users** node and the **Accounts** node. Select an account, then select **Show Status Messages**.

- Navigate to collection<!--9502958-->: You can now navigate to a collection from the **Collections** tab in the **Devices** node. Select **View Collection** from either the ribbon or the right-click menu in the tab.

- Added maintenance window column<!--9708594-->: A **Maintenance window** column was added to the **Collections** tab in the **Devices** node.

- Display assigned users<!--9709014-->: If a collection deletion fails because of scope assignment, the assigned users are displayed.

- You can now use the **All Subfolders** search option from the **Boot Images**, **Operating System Upgrade Packages**, and **Operating System Images** nodes. <!--8325332, 9506942, 9506938, 9506934-->

For more information about improvements to the console, see [Configuration Manager console changes and tips](../../servers/manage/admin-console-tips.md).

## Tools

### Improvements to Support Center
<!--8272488-->

Starting in this release, the **Content** view in the **Support Center Client Tools** has been renamed to **Deployments**.  From **Deployments**, you can review all of the deployments currently targeted to the device. The new view is grouped by **Category** and **Status**. The view can be sorted and filtered to help you find the deployments you're interested in. Select a deployment in the results pane to display more information in the details pane.

For more information, see [Support Center Client Tools user interface reference](../../support/support-center-ui-reference.md#deployment-view).

### Improvements to CMTrace

<!--9607363-->

This release includes multiple performance improvements to the CMTrace log viewer. If you have a copy of CMTrace in a non-default location, consider removing it and using a copy in one of the default paths. If it's in a custom location that meets your business requirements, then make sure you have a process to keep it up to date. A script is available in the Community Hub to help you locate and update versions of CMTrace to the latest version.

For more information, see [CMTrace](../../support/cmtrace.md).

### RBAViewer location change
<!--9573789-->
RBAViewer has moved from `<installdir>\tools\servertools\rbaviewer.exe`. It's now located in the Configuration Manager console directory. After you install the console, RBAViewer.exe will be in the same directory. The default location is `C:\Program Files (x86)\Microsoft Endpoint Manager\AdminConsole\bin\rbaviewer.exe`.

For more information, see [Configuration Manager tools](../../support/tools.md).

## Deprecated features

Learn about support changes before they're implemented in [removed and deprecated items](deprecated/removed-and-deprecated.md).

- The cloud-based distribution point (CDP) is deprecated. Starting in version 2107, you can't create new CDP instances. To provide content to internet-based devices, enable the CMG to distribute content.<!-- 10247883 -->

- The support lifecycle for SQL Server 2012 ends on July 12, 2022. Plan to upgrade database servers in your environment, including SQL Server Express at secondary sites.<!-- 10092858 -->

As [previously announced](deprecated/removed-and-deprecated-cmfeatures.md), version 2107 drops support for the following features:

- Log Analytics connector for Azure Monitor. This feature was called the _OMS Connector_ in the Azure Services node.<!-- 9649296 -->

## Other updates

Starting with this version, the following features are no longer [pre-release](../../servers/manage/pre-release-features.md):

- [Cloud management gateway (CMG) with virtual machine scale set](../../clients/manage/cmg/plan-cloud-management-gateway.md#virtual-machine-scale-sets) <!--3601040,8959690-->

For more information on changes to the Windows PowerShell cmdlets for Configuration Manager, see [version 2107 release notes](/powershell/sccm/2107-release-notes).

Aside from new features, this release also includes other changes such as bug fixes. For more information, see [Summary of changes in Configuration Manager current branch, version 2107](../../../hotfix/2107/10096997.md).


The following update rollup (11121541) is available in the console starting on October 27, 2021: [Update rollup for Configuration Manager current branch, version 2107](../../../hotfix/2107/11121541.md).


### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [12636660](../../../hotfix/2107/12636660.md) | Client update for Microsoft Endpoint Configuration Manager version 2107 | December 2, 2021 | No |

## Next steps

<!-- At this time, version 2107 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-2107.md#early-update-ring). -->

As of August 23, 2021, version 2107 is globally available for all customers to install.

When you're ready to install this version, see [Installing updates for Configuration Manager](../../servers/manage/updates.md) and [Checklist for installing update 2107](../../servers/manage/checklist-for-installing-update-2107.md).

> [!TIP]
> To install a new site, use a baseline version of Configuration Manager.
>
> Learn more about:
>
> - [Installing new sites](../../servers/deploy/install/installing-sites.md)
> - [Baseline and update versions](../../servers/manage/updates.md#bkmk_Baselines)

For known significant issues, see the [Release notes](../../servers/deploy/install/release-notes.md).

After you update a site, also review the [Post-update checklist](../../servers/manage/checklist-for-installing-update-2107.md#post-update-checklist).
