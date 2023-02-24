---
title: What's new in version 2006
titleSuffix: Configuration Manager
description: Get details about changes and new capabilities introduced in version 2006 of Configuration Manager current branch.
ms.date: 11/04/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ROBOTS: NOINDEX
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# What's new in version 2006 of Configuration Manager current branch

*Applies to: Configuration Manager (current branch)*

Update 2006 for Configuration Manager current branch is available as an in-console update. Apply this update on sites that run version 1810 or later. <!-- baseline only statement:When installing a new site, it's also available as a baseline version. -->This article summarizes the changes and new features in Configuration Manager, version 2006.

Always review the latest checklist for installing this update. For more information, see [Checklist for installing update 2006](../../servers/manage/checklist-for-installing-update-2006.md). After you update a site, also review the [Post-update checklist](../../servers/manage/checklist-for-installing-update-2006.md#post-update-checklist).

To take full advantage of new Configuration Manager features, after you update the site, also update clients to the latest version. While new functionality appears in the Configuration Manager console when you update the site and console, the complete scenario isn't functional until the client version is also the latest.

## <a name="bkmk_tenant"></a> Microsoft Intune tenant attach

### Scripts from the admin center
<!--IN7220536, CM6234688  -->
Bring the power of the Configuration Manager on-premises [Run scripts](../../../apps/deploy-use/create-deploy-scripts.md) feature to the Microsoft Intune admin center. Allow additional personas, like Helpdesk, to run PowerShell scripts from the cloud against an individual Configuration Manager managed device in real time. This gives all the traditional benefits of PowerShell scripts that have already been defined and approved by the Configuration Manager admin to this new environment. For more information, see [Tenant attach: Scripts from the admin center](../../../tenant-attach/scripts.md).

### <a name="bkmk_timeline"></a> Device timeline in the admin center
<!--7220536, CM7141381-->
When Configuration Manager synchronizes a device to Microsoft Intune through tenant attach, you'll be able to see a timeline of events. This timeline shows past activity on the device that can help you troubleshoot problems. For more information, see [Tenant attach: Device timeline in the admin center](../../../tenant-attach/timeline.md).

### <a name="bkmk_hinv"></a> Resource explorer in the admin center
<!--6479284-->
From the Microsoft Endpoint Management admin center, you can view hardware inventory for uploaded Configuration Manager devices by using resource explorer. For more information, see [Tenant attach: Resource explorer in the admin center](../../../tenant-attach/resource-explorer.md).

### <a name="bkmk_cmpivot"></a> CMPivot from the admin center
<!--6024392-->
Bring the power of CMPivot to the Microsoft Intune admin center. Allow additional personas, like Helpdesk, to be able to initiate real-time queries from the cloud against an individual ConfigMgr managed device and return the results back to the admin center. This gives all the traditional benefits of CMPivot, which allows IT Admins and other designated personas the ability to quickly assess the state of devices in their environment and take action.

For more information about CMPivot from the admin center, see [Tenant attach: Launch CMPivot from the admin center](../../../tenant-attach/cmpivot-start.md), [CMPivot overview](../../../tenant-attach/cmpivot-overview-attached.md), and [CMPivot sample scripts](../../../tenant-attach/cmpivot-samples-attached.md).

### <a name="bkmk_atp"></a> Microsoft Defender Antivirus policies in the Microsoft Intune admin center
<!--4812909-->
You can now create Microsoft Defender antivirus policies in the Microsoft Intune admin center and deploy them to Configuration Manager collections. For more information including detailed instructions and available settings, see the following articles:
- [Tenant attach: Onboard Configuration Manager clients to Microsoft Defender for Endpoint from the admin center (preview)](../../../tenant-attach/atp-onboard.md)
- [Tenant attach: Deploy endpoint security Antivirus policy from the admin center (preview)](../../../tenant-attach/deploy-antivirus-policy.md)
- [Settings for Microsoft Defender Antivirus policy for tenant attached devices in Microsoft Intune](../../../../intune/protect/antivirus-microsoft-defender-settings-windows-tenant-attach.md?toc=/mem/configmgr/tenant-attach/toc.json&bc=/mem/configmgr/tenant-attach/breadcrumb/toc.json).
- [Settings for Windows Security experience Antivirus policy for tenant attached devices](../../../../intune/protect/antivirus-windows-security-settings-windows-tenant-attach.md?toc=/mem/configmgr/tenant-attach/toc.json&bc=/mem/configmgr/tenant-attach/breadcrumb/toc.json)

### Install applications from the admin center
<!--7518897, 6024389-->
You can initiate an application install in real time for a tenant attached device from the Microsoft Intune admin center. Starting with Configuration Manager version 2006, the list of applications available for the device also includes applications deployed to the device's currently logged on user. For more information, see [Tenant attach: Install an application from the admin center](../../../tenant-attach/applications.md).  

### Import previously created Azure AD application during tenant attach onboarding
<!--6479246-->
During a new onboarding, an administrator can specify a previously created application during onboarding to tenant attach. For more information, see [Microsoft Intune tenant attach: Device sync and device actions](../../../tenant-attach/device-sync-actions.md#bkmk_aad_app).

## <a name="bkmk_ea"></a> Endpoint analytics

### Endpoint analytics data collection enabled by default
<!--7065447, 7741111-->
The **Enable Endpoint analytics data collection** client setting is now enabled by default. This setting allows your managed endpoints to send data, such as startup performance insights, to your Configuration Manager site server. This change affects local data collection only. Endpoint analytics data isn't uploaded to the Microsoft Intune admin center until you [enable data upload in Configuration Manager](../../../../analytics/enroll-configmgr.md#bkmk_cm_upload). The new default value applies to the default client settings and any custom client settings created after upgrading to version 2006.

- If you're upgrading from version 2002 to version 2006, existing custom client settings values are retained. The default value for **Enable Endpoint analytics data collection** in Configuration Manager version 2002 is **No**.
- If you're upgrading to version 2006 from Configuration Manager version 1910 or prior, any pre-existing custom client settings that contain the **Computer Agent** group of settings inherits the new default of **Yes** for **Enable Endpoint analytics data collection**.

For more information, see [Configure Endpoint analytics data collection in Configuration Manager](../../../../analytics/enroll-configmgr.md#bkmk_cm_upload).

## <a name="bkmk_infra"></a> Site infrastructure

### VPN boundary type

<!--7020519-->

To simplify managing remote clients, you can now create a new boundary type for VPNs. Previously, you had to create boundaries for VPN clients based on the IP address or subnet. This configuration could be challenging or not possible because of the subnet configuration or the VPN design.

Now when a client sends a location request, it includes additional information about its network configuration. Based on this information, the server determines whether the client is on a VPN.

For more information, see [Define boundaries](../../servers/deploy/configure/boundaries.md).

### Management insights to optimize for remote workers

<!--6982226-->

This release adds a new group of management insights, **Optimize for remote workers**. These insights help you create better experiences for remote workers and reduce load on your infrastructure. The insights in this release primarily focus on VPN:

- **Define VPN boundary groups**
- **Configure VPN connected clients to prefer cloud based content sources**
- **Disable peer to peer content sharing for VPN connected clients**

For more information, see [Management insights](../../servers/manage/management-insights.md).

### Improved support for Azure Virtual Desktop

<!--6527576-->

The **Windows 10 Enterprise multi-session** platform is available in the list of supported OS versions on objects with requirement rules or applicability lists.

For more information on Configuration Manager's support for Azure Virtual Desktop, see [Supported OS versions for clients and devices](../configs/supported-operating-systems-for-clients-and-devices.md#azure-virtual-desktop).

### Intranet clients can use a CMG software update point
<!--7102873-->
Intranet clients can now access a CMG software update point when it's assigned to a boundary group. For more information, see [Configure boundary groups](../../servers/deploy/configure/boundary-groups-software-update-points.md#intranet-clients-can-use-a-cmg-software-update-point).

## <a name="bkmk_cloud"></a> Cloud-attached management

### Use the Company Portal app on co-managed devices

<!--CMADO-3601237,INADO-4297660-->

The Company Portal app is now the cross-platform app portal experience for the Microsoft Intune family of products. By configuring co-managed devices to also use the Company Portal app, you can provide a consistent user experience on all devices.

For more information, see [Use the Company Portal app on co-managed devices](../../../comanage/company-portal.md).

### Use Microsoft Azure China 21Vianet for co-management
<!--7133238-->
You can now select the Azure China Cloud as your Azure environment when enabling co-management. For more information, see [How to enable co-management](../../../comanage/how-to-enable.md).

### Notification for Azure AD app secret key expiration

<!--6386392-->

If you configure Azure services to cloud-attach your site, the Configuration Manager console now displays notifications for the following circumstances:

- One or more Azure AD app secret keys will expire soon
- One or more Azure AD app secret keys have expired

For more information, see [Renew secret key](../../servers/deploy/configure/azure-services-wizard.md#bkmk_renew).

### Desktop Analytics

For more information on the monthly changes to the Desktop Analytics cloud service, see [What's new in Desktop Analytics](../../../desktop-analytics/whats-new.md).

#### Change to diagnostic data labels

<!-- 7363467 -->

To better align with the Desktop Analytics requirements for Windows diagnostic data, these settings have new labels:

| Version 2006 and later | Version 2002 and earlier |
|---------|---------|
| Required | Basic |
| Optional (limited) | Enhanced (Limited) |
| N/A | Enhanced |
| Optional | Full |

If you previously configured any devices at the **Enhanced** level, when you upgrade to version 2006, they'll revert to **Optional (limited)**. They will then send less data to Microsoft. This change shouldn't impact what you see in Desktop Analytics.

For more information, see [Enable data sharing for Desktop Analytics](../../../desktop-analytics/enable-data-sharing.md).

## <a name="bkmk_real"></a> Real-time management

### Improvements to CMPivot
<!--6518631-->
The following improvements have been made in CMPivot:

- CMPivot from the console and CMPivot standalone have been converged
- Run CMPivot from an individual device or multiple devices without having to select or create a collection
- From CMPivot query results, you can select an individual device or multiple devices then launch a separate CMPivot instance scoped to your selection.

For more information, see [CMPivot starting in version 2006](../../servers/manage/cmpivot-changes.md#bkmk_2006).

## <a name="bkmk_client"></a> Client management

### Install and upgrade the client on a metered connection

<!--6976145-->

Previously, if the device was connected to a metered network, new clients wouldn't install. Existing clients only upgraded if you allowed all client communication. For devices that are frequently roaming on a metered network, they would be unmanaged or on an older client version. Starting in this release, you can install and upgrade the client when you set the client setting **Client communication on metered internet connections** to **Allow** or **Limit**. With this setting, you can allow the client to stay current, but still manage the client communication on a metered network.

To define the behavior for a new client installation, there's a new ccmsetup parameter **/AllowMetered**. When you allow client communication on a metered network for ccmsetup, it downloads the content, registers with the site, and downloads the initial policy. Any further client communication follows the configuration of the client setting from that policy.

For more information, see the following articles:

- [About client settings](../../clients/deploy/about-client-settings.md#client-communication-on-metered-internet-connections)
- [About client installation parameters and properties](../../clients/deploy/about-client-installation-properties.md#allowmetered)

### Improvements to managing device restarts

<!--3601213-->

Configuration Manager provides many options to manage device restarts and restart notifications. You can now configure a client setting to prevent devices from automatically restarting when a deployment requires it. This setting gives you more control in unique situations. By default, the client setting **Configuration Manager can force a device to restart** is enabled, so Configuration Manager can still force devices to restart. This setting only applies to application, software update, and package deployments that require a restart.

For more information, see [device restart notifications](../../clients/deploy/device-restart-notifications.md).

## <a name="bkmk_app"></a> Application management

### Improvements to available apps via CMG

<!--6935376-->
This release fixes an issue with Software Center and Azure Active Directory (Azure AD) authentication. For a client detected as on the intranet but communicating via the cloud management gateway (CMG), previously Software Center would use Windows authentication. When it tried to get the list of user-available apps, it would fail. It now uses Azure Active Directory (Azure AD) identity for devices joined to Azure AD. These devices can be cloud-joined or hybrid-joined.

For more information, see [Prerequisites to deploy user-available apps](../../../apps/plan-design/prerequisites-deploy-user-available-apps.md).

### Microsoft 365 Apps for enterprise
<!--6298093-->
Office 365 ProPlus was renamed to Microsoft 365 Apps for enterprise on April 21, 2020. Starting in version 2006, the following changes have been made:

- The Configuration Manager console has been updated to use the new name.
  - This change also includes update channel names for Microsoft 365 Apps.
- A banner notification was added to the console to notify you if one or more automatic deployment rules reference obsolete channel names in the **Title** criteria for Microsoft 365 Apps updates.

For more information, see [Microsoft 365 Apps channel names](../../../sum/deploy-use/manage-office-365-proplus-updates.md#bkmk_channel) and [Microsoft 365 Apps readiness dashboard](../../../sum/deploy-use/office-365-dashboard.md#bkmk_readiness-dash).

## <a name="bkmk_osd"></a> OS deployment

### Task sequence media support for cloud-based content

<!--6209223-->

Task sequence media can now download cloud-based content. For example, you send a USB key to a user at a remote office to reimage their device. Or an office that has a local PXE server, but you want devices to prioritize cloud services as much as possible. Instead of further taxing the WAN to download large OS deployment content, boot media and PXE deployments can now get content from cloud-based sources. For example, a cloud management gateway (CMG) that you enable to share content.

> [!NOTE]
> The device still needs an intranet connection to the management point.

For more information, see [Bootable media support for cloud-based content](../../../osd/deploy-use/deploy-task-sequence-over-internet.md#bootable-media-support-for-cloud-based-content).

### Improvements to task sequences via CMG

This release includes the following improvements to deploy task sequences to devices that communicate via a cloud management gateway (CMG):

- Support for OS deployment<!--6997525-->: With a task sequence that uses a boot image to deploy an OS, you can deploy it to a device that communicates via CMG. The user needs to start the task sequence from Software Center. For more information, see [Supported configurations for CMG](../../clients/manage/cmg/supported-configurations.md).

- This release fixes the two known issues from Configuration Manager current branch version 2002.<!-- 6983320 --> You can now run a task sequence on a device that communicates via CMG in the following circumstances:

  - A workgroup device that you register with a [bulk registration token](../../clients/deploy/deploy-clients-cmg-token.md)

  - You configure the site for [Enhanced HTTP](../hierarchy/enhanced-http.md) and the management point is HTTP

### Improvements to BitLocker task sequence steps

<!--6995601-->

You can now specify the disk encryption mode on the **Enable BitLocker** and **Pre-provision BitLocker** task sequence steps. By default, the steps continue to use the default encryption method for the OS version.

The **Enable BitLocker** step also now includes a setting to **Skip this step for computers that do not have a TPM or when TPM is not enabled**. When you enable this setting, the step logs an error on a device without a TPM or a TPM that doesn't initialize, and the task sequence continues. This setting makes it easier to manage the task sequence behavior on devices that can't fully support BitLocker.

For more information, see [Task sequence steps](../../../osd/understand/task-sequence-steps.md).

### Management insight rules for OS deployment

<!--6982275-->

When the size of the task sequence policy exceeds 32 MB, the client fails to process the large policy. The client then fails to run the task sequence deployment. To help you manage the policy size of task sequences, this release includes the following management insights:

- **Large task sequences may contribute to exceeding maximum policy size**

- **Total policy size for task sequences exceeds policy limit**

> [!TIP]
> These rules are in a new group for **Operating System Deployment**. The existing rule for **Unused boot images** is now in this group too.

For more information, see [management insight](../../servers/manage/management-insights.md#operating-system-deployment).

### Improvements to OS deployment

This release includes the following additional improvements to OS deployment:

- Use a task sequence variable to specify the target of the [Format and Partition Disk](../../../osd/understand/task-sequence-steps.md#BKMK_FormatandPartitionDisk) step. This new variable option supports more complex task sequences with dynamic behaviors. For example, a custom script can detect the disk and set the variable based on the hardware type. Then you can use multiple instances of this step to configure different hardware types and partitions.<!--6610288-->

- The [Check Readiness](../../../osd/understand/task-sequence-steps.md#BKMK_CheckReadiness) step now includes a check to determine if the device uses UEFI. It also includes a new read-only task sequence variable, **_TS_CRUEFI**.<!--6452769-->

- If you enable the [task sequence progress window](../../../osd/understand/user-experience.md#task-sequence-progress) to show more detailed progress information, it now doesn't count enabled steps in a disabled group. This change helps make the progress estimate more precise.<!--6448412-->

- Previously, during a task sequence to upgrade a device to Windows 10, a command prompt window opened during one of the final Windows configuration phases. The window was on top of the Windows out-of-box experience (OOBE), and users could interact with it to disrupt the upgrade process. Now the SetupCompleteTemplate.cmd and SetupRollbackTemplate.cmd scripts from Configuration Manager include a change to hide this command prompt window.<!--2837795-->

- Some customers build custom task sequence interfaces using the **IProgressUI::ShowMessage** method, but it doesn't return a value for the user's response. This release adds the [IProgressUI::ShowMessageEx](../../../develop/reference/core/clients/client-classes/iprogressui--showmessageex-method.md) method. This new method is similar to the existing method, but also includes a new integer result variable, **pResult**.<!--6448458-->

## Protection

### CMG support for endpoint protection policies

<!--4773948-->

While the cloud management gateway (CMG) has supported endpoint protection policies, devices required access to on-premises domain controllers. Starting in this release, clients that communicate via a CMG can immediately apply endpoint protection policies without an active connection to Active Directory.

For more information, see [Supported configurations for CMG](../../clients/manage/cmg/supported-configurations.md).

### BitLocker management support for hierarchies

<!-- 5925693 -->

You can now install the BitLocker self-service portal and the administration and monitoring website at the central administration site.

For more information, see [Set up BitLocker portals](../../../protect/deploy-use/bitlocker/setup-websites.md).

## <a name="bkmk_admin"></a> Configuration Manager console

### Community hub and GitHub
<!--3555935, 3555936, deep link included 4224406-->

*(First introduced in June 2020)*

The IT admin community has developed a wealth of knowledge over the years. Rather than reinventing items like scripts and reports from scratch, we've built a Configuration Manager **Community hub** where you can share with each other. By leveraging the work of others, you can save hours of work. The Community hub fosters creativity by building on others' work and having other people build on yours. GitHub already has industry-wide processes and tools built for sharing. Now, the Community hub will leverage those tools directly in the Configuration Manager console as foundational pieces for driving this new community. For the initial release, the content made available in the Community hub will be uploaded only by Microsoft. 

For more information, see [Community hub and GitHub](../../servers/manage/community-hub.md).

### <a name="bkmk_deeplink"></a> Direct links to Community hub items
<!--4224406-->
You can easily navigate to and reference items in the Configuration Manager console Community hub node with a direct link. For more information, see [Direct links to Community hub items](../../servers/manage/community-hub.md#bkmk_deeplink).

### Notifications from Microsoft
<!--3953121-->
You can now choose to receive notifications from Microsoft in the Configuration Manager console. These notifications help you stay informed about new or updated features, changes to Configuration Manager and attached services, and issues that require action to remediate.

For more information, see [Configure a site to receive messages from Microsoft](../../servers/manage/admin-console-notifications.md#bkmk_msft).

### Power BI sample reports
<!--5679791-->

*(First introduced in June 2020)*

When you integrate Power BI Report Server with Configuration Manager reporting, there are now sample Power BI reports available. Download and install the following sample reports:

- Software Update Compliance Status
- Software Update Deployment Status

For more information, see [Install Power BI sample reports](../../servers/manage/powerbi-sample-reports.md).

<!-- Unused sections in this release:
## Reporting
## <a name="bkmk_userxp"></a> User experience
## <a name="bkmk_sum"></a> Software updates
## Office management
## <a name="bkmk_content"></a> Content management
## <a name="bkmk_comgmt"></a> Co-management
-->

## <a name="bkmk_deprecated"></a> Deprecated operating systems

Learn about support changes before they're implemented in [removed and deprecated items](deprecated/removed-and-deprecated.md).

As first announced in version 1906, version 2006 drops support for the following client OS versions:  

- Windows CE 7.0
- Windows 10 Mobile
- Windows 10 Mobile Enterprise

## Other updates

<!--
Starting with this version, the following features are no longer [pre-release](../../servers/manage/pre-release-features.md):

### Azure Active Directory user group discovery](../../servers/deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco)<!--3611956
-->

For more information on changes to the Windows PowerShell cmdlets for Configuration Manager, see [PowerShell version 2006 release notes](/powershell/sccm/2006-release-notes).

For more information on changes to the administration service REST API, see [Administration service release notes](../../../develop/adminservice/release-notes.md#bkmk_2006).

Aside from new features, this release also includes additional changes such as bug fixes. For more information, see [Summary of changes in Configuration Manager current branch, version 2006](https://support.microsoft.com/help/4578830).

The following revised update rollup (4575789) is available in the console starting on November 30, 2020: [Revised update rollup for Microsoft Endpoint Configuration Manager current branch, version 2006](https://support.microsoft.com/help/4575789). 

Note this revision supersedes the original release of KB 4578605 [Update rollup for Microsoft Configuration Manager version 2006](https://support.microsoft.com/help/4578605).

### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4580678](https://support.microsoft.com/help/4580678) | Tenant attach rollup for Configuration Manager current branch, version 2006 | September 18, 2020 | Yes |
| [4584759](https://support.microsoft.com/help/4584759) | Clients report Desktop Analytics configuration errors in Configuration Manager, version 2006 | October 2, 2020 | Yes |
| [4575786](https://support.microsoft.com/help/4575786) | Configuration Manager console terminates unexpectedly on Configuration Manager current branch, version 2006 | November 12, 2020 | Yes |
| [4575787](https://support.microsoft.com/help/4575787) | Co-management enrollment takes longer than expected for Configuration Manager clients | November 12, 2020 | No |
| [4575785](https://support.microsoft.com/help/4575785) | November 2020 Update for Asset Intelligence authentication certificate in Configuration Manager | November 18, 2020 | No |
| [4575790](https://support.microsoft.com/help/4575790) | Client setup is unable to download contents from a cloud distribution point in Configuration Manager current branch, version 2006 | November 20, 2020 | Yes |

## Next steps

<!-- At this time, version 2006 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-2006.md#early-update-ring). -->

As of August 31, 2020, version 2006 is globally available for all customers to install.

When you're ready to install this version, see [Installing updates for Configuration Manager](../../servers/manage/updates.md) and [Checklist for installing update 2006](../../servers/manage/checklist-for-installing-update-2006.md).

> [!TIP]
> To install a new site, use a baseline version of Configuration Manager.
>
> Learn more about:
>
> - [Installing new sites](../../servers/deploy/install/installing-sites.md)
> - [Baseline and update versions](../../servers/manage/updates.md#bkmk_Baselines)

For known significant issues, see the [Release notes](../../servers/deploy/install/release-notes.md).

After you update a site, also review the [Post-update checklist](../../servers/manage/checklist-for-installing-update-2006.md#post-update-checklist).
