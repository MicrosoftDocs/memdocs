---
title: What's new in version 2002
titleSuffix: Configuration Manager
description: Get details about changes and new capabilities introduced in version 2002 of Configuration Manager current branch.
ms.date: 07/27/2020
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: conceptual
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ROBOTS: NOINDEX
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# What's new in version 2002 of Configuration Manager current branch

*Applies to: Configuration Manager (current branch)*

Update 2002 for Configuration Manager current branch is available as an in-console update. Apply this update on sites that run version 1810 or later. <!-- baseline only statement:-->When installing a new site, it's also available as a baseline version. This article summarizes the changes and new features in Configuration Manager, version 2002.

Always review the latest checklist for installing this update. For more information, see [Checklist for installing update 2002](../../servers/manage/checklist-for-installing-update-2002.md). After you update a site, also review the [Post-update checklist](../../servers/manage/checklist-for-installing-update-2002.md#post-update-checklist).

To take full advantage of new Configuration Manager features, after you update the site, also update clients to the latest version. While new functionality appears in the Configuration Manager console when you update the site and console, the complete scenario isn't functional until the client version is also the latest.

## <a name="bkmk_tenant"></a> Microsoft Intune tenant attach

### <a name="bkmk_attach"></a> Device sync and device actions
<!--3555758-->
The Microsoft Intune family of products is an integrated solution for managing all of your devices. Microsoft brings together Configuration Manager and Intune into a single console called **Microsoft Intune admin center**. Starting in this release you can upload your Configuration Manager devices to the cloud service and take actions from the **Devices** blade in the admin center.

For more information, see [Microsoft Intune tenant attach](../../../tenant-attach/device-sync-actions.md).

## <a name="bkmk_infra"></a> Site infrastructure

### Remove a central administration site
<!-- 3607277 -->

If your hierarchy consists of a central administration site (CAS) and a single child primary site, you can now remove the CAS. This action simplifies your Configuration Manager infrastructure to a single, standalone primary site. It removes the complexities of site-to-site replication, and focuses your management tasks to the single primary site.

For more information, see [Remove the CAS](../../servers/deploy/install/remove-central-administration-site.md).

### New management insight rules

This release includes the following management insight rules:

- Nine rules in the **Configuration Manager Assessment** group courtesy of Microsoft Premier Field Engineering. These rules are a sample of the many more checks that Microsoft Premier provides in the Services Hub.<!-- 3607758 -->

  - Active Directory Security Group Discovery is configured to run too frequently
  - Active Directory System Discovery is configured to run too frequently
  - Active Directory User Discovery is configured to run too frequently
  - Collections limited to All Systems or All Users
  - Heartbeat Discovery is disabled
  - Long running collection queries enabled for incremental updates
  - Reduce the number of applications and packages on distribution points
  - Secondary site installation issues
  - Update all sites to the same version

- Two additional rules in the **Cloud Services** group to help you configure your site for adding secure HTTPS communication:<!-- 6268489 -->

  - Sites that don't have proper HTTPS configuration
  - Devices not uploaded to Azure AD

For more information, see [Management insights](../../servers/manage/management-insights.md).

### Improvements to administration service

<!-- 5728365 -->

The administration service is a REST API for the SMS Provider. Previously, you had to implement one of the following dependencies:

- Enable Enhanced HTTP for the entire site
- Manually bind a PKI-based certificate to IIS on the server that hosts the SMS Provider role

Starting in this release, the administration service automatically uses the site's self-signed certificate. This change helps reduce the friction for easier use of the administration service. The site always generates this certificate. The Enhanced HTTP site setting to **Use Configuration Manager-generated certificates for HTTP site systems** only controls whether site systems use it or not. Now the administration service ignores this site setting, as it always uses the site's certificate even if no other site system is using Enhanced HTTP. You can still use a PKI-based server authentication certificate.

For more information, see the following new articles:

- [What is the administration service?](../../../develop/adminservice/overview.md)
- [How to set up the administration service](../../../develop/adminservice/set-up.md)

### Proxy support for Azure Active Directory discovery and group sync

<!-- 5913817 -->

The site system's proxy settings, including authentication, are now used by:

- Azure Active Directory (Azure AD) user discovery
- Azure AD user group discovery
- Synchronizing collection membership results to Azure Active Directory groups

For more information, see [Proxy server support](../network/proxy-server-support.md#other-features-that-use-the-proxy).

## <a name="bkmk_cloud"></a> Cloud-attached management

### Critical status message shows server connection errors to required endpoints

<!-- 5566763 -->

If the Configuration Manager site server fails to connect to required endpoints for a cloud service, it raises a critical status message ID 11488. When the site server can't connect to the service, the SMS_SERVICE_CONNECTOR component status changes to critical. View detailed status in the Component Status node of the Configuration Manager console.

### Token-based authentication for cloud management gateway

<!-- 5686290 -->

The cloud management gateway (CMG) supports many types of clients, but even with Enhanced HTTP, these clients require a client authentication certificate. This certificate requirement can be challenging to provision on internet-based clients that don't often connect to the internal network, aren't able to join Azure Active Directory (Azure AD), and don't have a method to install a PKI-issued certificate.

Configuration Manager extends its device support with the following methods:

- Register on the internal network for a unique token
- Create a bulk registration token for internet-based devices

For more information, see [Token-based authentication for CMG](../../clients/deploy/deploy-clients-cmg-token.md).

### Microsoft Configuration Manager cloud features

<!--5834830-->

When new cloud-based features are available in the Microsoft Intune admin center, or other attached cloud services for your on-premises Configuration Manager installation, you can now opt in to these new features in the Configuration Manager console. For more information on enabling features in the Configuration Manager console, see [Enable optional features from updates](../../servers/manage/optional-features.md).

## <a name="bkmk_da"></a> Desktop Analytics

For more information on the monthly changes to the Desktop Analytics cloud service, see [What's new in Desktop Analytics](../../../desktop-analytics/whats-new.md).

### Connection Health dashboard shows client connection issues

Use the Desktop Analytics Connection Health dashboard in Configuration Manager to monitor the clients' connectivity health. It now helps you to more easily identify client proxy configuration issues in two areas:

- **Endpoint connectivity checks**: If clients can't reach a required endpoint, you see a configuration alert in the dashboard. Drill down to see the endpoints to which clients can't connect because of proxy configuration issues.<!-- 4963230 -->

- **Connectivity status**: If your clients use a proxy server to access the Desktop Analytics cloud service, Configuration Manager now displays proxy authentication issues from clients. Drill down to see clients that are unable to enroll because of proxy authentication.<!-- 4963383 -->

For more information, see [Monitor connection health](../../../desktop-analytics/monitor-connection-health.md).

## <a name="bkmk_real"></a> Real-time management

### Improvements to CMPivot

<!-- 5870934 -->

We've made it easier to navigate CMPivot entities. You can now search CMPivot entities. New icons have also been added to easily differentiate the entities and the entity object types.

For more information, see [CMPivot](../../servers/manage/cmpivot-changes.md#bkmk_2002).

## <a name="bkmk_content"></a> Content management

### Exclude certain subnets for peer content download

<!-- 3555777 -->

Boundary groups include the following option for peer downloads: **During peer downloads, only use peers within the same subnet**. If you enable this option, the content location list from the management point only includes peer sources that are in the same subnet and boundary group as the client. Depending on the configuration of your network, you can now exclude certain subnets for matching. For example, you want to include a boundary but exclude a specific VPN subnet.

For more information, see [Boundary group options](../../servers/deploy/configure/boundary-group-options.md).

### Proxy support for Microsoft Connected Cache

<!-- 5856396 -->

If your environment uses an unauthenticated proxy server for internet access, now when you enable a Configuration Manager distribution point for Microsoft Connected Cache, it can communicate through the proxy. For more information, see [Microsoft Connected Cache](../hierarchy/microsoft-connected-cache.md).

## <a name="bkmk_client"></a> Client management

### Client log collection

<!-- 4226618 -->

You can now trigger a client device to upload its client logs to the site server by sending a client notification action from the Configuration Manager console.

For more information, see [Client notification](../../clients/manage/client-notification.md#client-diagnostics).

### Wake up a device from the central administration site

<!-- 6030715 -->

From the central administration site (CAS), in the Devices or Device Collections node, you can now use the client notification action to Wake Up devices. This action was previously only available from a primary site.

For more information, see [How to configure Wake on LAN](../../clients/deploy/configure-wake-on-lan.md#bkmk_wol-1810).

### Improvements to support for ARM64 devices

<!--5954175-->

The **All Windows 10 (ARM64)** platform is available in the list of supported OS versions on objects with requirement rules or applicability lists.

> [!NOTE]
> If you previously selected the top-level **Windows 10** platform, this action automatically selected both **All Windows 10 (64-bit)** and **All Windows 10 (32-bit)**. This new platform isn't automatically selected. If you want to add **All Windows 10 (ARM64)**, manually select it in the list.

For more information on Configuration Manager's support for ARM64 devices, see [Windows 10 on ARM64](../configs/support-for-windows-10.md#bkmk_arm64).

### Track configuration item remediations
<!--4261411-->
You can now **Track remediation history when supported** on your configuration item compliance rules. When this option is enabled, any remediation that occurs on the client for the configuration item generates a state message. The history is stored in the Configuration Manager database.

For more information on this setting, see [Create custom configuration items for Windows desktop and server computers managed with the Configuration Manager client](../../../compliance/deploy-use/create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-client.md#bkmk_track).

<!-- ## <a name="bkmk_comgmt"></a> Co-management -->

## <a name="bkmk_app"></a> Application management

### Microsoft Edge management dashboard

<!-- 3871913 -->

The Microsoft Edge management dashboard provides you insights on the usage of Microsoft Edge and other browsers. In this dashboard, you can:

- See how many of your devices have Microsoft Edge installed
- See how many clients have different versions of Microsoft Edge installed
- Have a view of the installed browsers across devices
- Have a view of preferred browser by device

From the Software Library workspace, click Microsoft Edge Management to see the dashboard. Change the collection for the graph data by clicking Browse and choosing another collection. By default your five largest collections are in the drop-down list. When you select a collection that isn't in the list, the newly selected collection takes the bottom spot on your drop-down list.

For more information, see [Microsoft Edge management](../../../apps/deploy-use/deploy-edge.md#bkmk_edge-dash).

### Improvements to Microsoft Edge management

<!-- 4561024 -->

You can now create a Microsoft Edge application that's set up to receive automatic updates rather than having automatic updates disabled. This change allows you to choose to manage updates for Microsoft Edge with Configuration Manager or allow Microsoft Edge to automatically update. When creating the application, select Allow Microsoft Edge to automatically update the version of the client on the end user's device on the Microsoft Edge Settings page.

For more information, see [Microsoft Edge management](../../../apps/deploy-use/deploy-edge.md#bkmk_autoupdate).

### Task sequence as an app model deployment type

<!-- 3555953 -->

You can now install complex applications using task sequences via the application model. Add a deployment type to an app that's a task sequence, either to install or uninstall the app. This feature provides the following behaviors:

- Display the app task sequence with an icon in Software Center. An icon makes it easier for users to find and identify the app task sequence.

- Define additional metadata for the app task sequence, including localized information

For more information, see [Create Windows applications](../../../apps/get-started/creating-windows-applications.md#bkmk_tsdt).

## <a name="bkmk_osd"></a> OS deployment

### Bootstrap a task sequence immediately after client registration

<!-- 5526972 -->

When you install and register a new Configuration Manager client, and also deploy a task sequence to it, it's difficult to determine how soon after registration it will run the task sequence. This release introduces a new client setup property that you can use to start a task sequence on a client after it successfully registers with the site.

For more information, see [About client installation properties - PROVISIONTS](../../clients/deploy/about-client-installation-properties.md#provisionts).

### Improvements to Check Readiness task sequence step

<!-- 6005561 -->

You can now verify more device properties in the **Check Readiness** task sequence step. Use this step in a task sequence to verify the target computer meets your prerequisite conditions.

- Architecture of current OS
- Minimum OS version
- Maximum OS version
- Minimum client version
- Language of current OS
- AC power plugged in
- Network adapter is connected and not wireless

For more information, see [Task sequence steps - Check Readiness](../../../osd/understand/task-sequence-steps.md#BKMK_CheckReadiness).

### Improvements to task sequence progress

<!-- 5932692 -->

The task sequence progress window now includes the following improvements:

- You can enable it to show the current step number, total number of steps, and percent completion
- Increased the width of the window to give you more space to better show the organization name in a single line

For more information, see [User experiences for OS deployment](../../../osd/understand/user-experience.md#task-sequence-progress).

### Improvements to OS deployment

This release includes the following improvements to OS deployment:

- The task sequence environment includes a new read-only variable, `_TSSecureBoot`.<!--5842295--> Use this variable to determine the state of secure boot on a UEFI-enabled device. For more information, see [_TSSecureBoot](../../../osd/understand/task-sequence-variables.md#TSSecureBoot).

- Set task sequence variables to configure the user context for the **Run Command Line** and **Run PowerShell Script** steps.<!-- 5573175 --> For more information, see [SMSTSRunCommandLineAsUser](../../../osd/understand/task-sequence-variables.md#SMSTSRunCommandLineAsUser) and [SMSTSRunPowerShellAsUser](../../../osd/understand/task-sequence-variables.md#SMSTSRunPowerShellAsUser).

- On the **Run PowerShell Script** step, you can now set the **Parameters** property to a variable.<!-- 5690481 --> For more information, see [Run PowerShell Script](../../../osd/understand/task-sequence-steps.md#BKMK_RunPowerShellScript).

- The Configuration Manager PXE responder now sends status messages to the site server. This change makes it easier to troubleshoot OS deployments that use this service.<!-- 5568051 -->

<!-- ## <a name="bkmk_userxp"></a> Software Center -->

## <a name="bkmk_sum"></a> Software updates

### Orchestration groups

<!-- 3098816 -->

Create an orchestration group to better control the deployment of software updates to devices. Many server administrators need to carefully manage updates for specific workloads, and automate behaviors in between.

An orchestration group gives you the flexibility to update devices based on a percentage, a specific number, or an explicit order. You can also run a PowerShell script before and after the devices run the update deployment.

Members of an orchestration group can be any Configuration Manager client, not just servers. The orchestration group rules apply to the devices for all software update deployments to any collection that contains an orchestration group member. Other deployment behaviors still apply. For example, maintenance windows and deployment schedules.

For more information, see [Orchestration groups](../../../sum/deploy-use/orchestration-groups.md).

### Evaluate software updates after a servicing stack update

<!-- 4639943 -->

Configuration Manager now detects if a servicing stack update (SSU) is part of an installation for multiple updates. When an SSU is detected, it's installed first. After install of the SSU, a software update evaluation cycle runs to install the remaining updates. This change allows a dependent cumulative update to be installed after the servicing stack update. The device doesn't need to restart between installs, and you don't need to create an additional maintenance window. SSUs are installed first only for non-user initiated installs. For instance, if a user initiates an installation for multiple updates from Software Center, the SSU might not be installed first.

For more information, see [Plan for software updates](../../../sum/plan-design/plan-for-software-updates.md#bkmk_ssu).

### Microsoft 365 updates for disconnected software update points

<!-- 4065163 -->

You can use a new tool to import Microsoft 365 updates from an internet-connected WSUS server into a disconnected Configuration Manager environment. Previously when you exported and imported metadata for software updated in disconnected environments, you were unable to deploy Microsoft 365 updates. Microsoft 365 updates require additional metadata downloaded from an Office API and the Office CDN, which isn't possible for disconnected environments.

For more information, see [Synchronize Microsoft 365 updates from a disconnected software update point](../../../sum/get-started/synchronize-office-updates-disconnected.md).

<!-- ## <a name="bkmk_o365"></a> Office management -->

## <a name="bkmk_protect"></a> Protection

### Expand Microsoft Defender for Endpoint onboarding
 
<!-- 5229962 -->
Configuration Manager has expanded its support for onboarding devices to Microsoft Defender for Endpoint. For more information, see [Microsoft Defender for Endpoint](../../../protect/deploy-use/defender-advanced-threat-protection.md).

### <a name="bkmk_atp"></a> Onboard Configuration Manager clients to Microsoft Defender for Endpoint via the Microsoft Intune admin center
<!--5691658-->
You can now deploy Microsoft Defender ATP Endpoint Detection and Response (EDR) onboarding policies to Configuration Manager managed clients. These clients don't require Azure AD or MDM enrollment, and the policy is targeted at ConfigMgr collections rather than Azure AD Groups.

This capability allows customers to manage both Intune MDM and Configuration Manager client EDR/ATP onboarding from a single management experience - the Microsoft Intune admin center. For more information, see [Endpoint detection and response policy for endpoint security in Intune](../../../../intune/protect/endpoint-security-edr-policy.md).

> [!Important]
> You'll need the hotfix rollup, [KB4563473](https://support.microsoft.com/help/4563473), installed in your environment for this feature.

### Improvements to BitLocker management

- The BitLocker management policy now includes additional settings, including policies for fixed and removable drives.<!-- 5925683 --> For more information, see [BitLocker settings reference](../../../protect/tech-ref/bitlocker/settings.md).

- In Configuration Manager current branch version 1910, to integrate the BitLocker recovery service you had to HTTPS-enable a management point. The HTTPS connection is necessary to encrypt the recovery keys across the network from the Configuration Manager client to the management point. Configuring the management point and all clients for HTTPS can be challenging for many customers.

    Starting in this version, the HTTPS requirement is for the IIS website that hosts the recovery service, not the entire management point role. This change relaxes the certificate requirements, and still encrypts the recovery keys in transit.<!-- 5925660 --> For more information, see [Encrypt recovery data over the network](../../../protect/deploy-use/bitlocker/encrypt-recovery-data-transit.md).

## <a name="bkmk_report"></a> Reporting

### Integrate with Power BI Report Server

<!-- 3721603 -->

You can now integrate Power BI Report Server with Configuration Manager reporting. This integration gives you modern visualization and better performance. It adds console support for Power BI reports similar to what already exists with SQL Server Reporting Services.

For more information, see [Integrate with Power BI Report Server](../../servers/manage/powerbi-report-server.md).

## <a name="bkmk_admin"></a> Configuration Manager console

### Show boundary groups for devices

<!--6521835-->

To help you better troubleshoot device behaviors with boundary groups, you can now view the boundary groups for specific devices. In the **Devices** node or when you show the members of a **Device Collection**, add the new **Boundary Group(s)** column to the list view.

For more information, see [Procedures for boundary groups](../../servers/deploy/configure/boundary-group-procedures.md#show-boundary-groups-for-devices).

### Send a smile improvements

<!-- 5891852 -->

When you Send a smile or Send a frown, a status message is created when the feedback is submitted. This improvement provides a record of:

- When the feedback was submitted
- Who submitted the feedback
- The feedback ID
- If the feedback submission was successful or not

A status message with an ID of 53900 is a successful submission and 53901 is a failed submission.

For more information, see [Product feedback](../../understand/product-feedback.md).

### Search all subfolders for configuration items and configuration baselines

<!--5891241-->

Similar to improvements in previous releases, you can now use the **All Subfolders** search option from the **Configuration Items** and **Configuration Baselines** nodes.

### Community hub

<!--3555935, 3555936-->

*(First introduced in June 2020)*

The IT admin community has developed a wealth of knowledge over the years. Rather than reinventing items like scripts and reports from scratch, we've built a Configuration Manager **Community hub** where you can share with each other. By leveraging the work of others, you can save hours of work. The Community hub fosters creativity by building on others' work and having other people build on yours. GitHub already has industry-wide processes and tools built for sharing. Now, the Community hub will leverage those tools directly in the Configuration Manager console as foundational pieces for driving this new community. For the initial release, the content made available in the Community hub will be uploaded only by Microsoft.

For more information, see [Community hub and GitHub](../../servers/manage/community-hub.md).

## <a name="bkmk_tools"></a> Tools

### OneTrace log groups

<!-- 5559993 -->

OneTrace now supports customizable log groups, similar to the feature in Support Center. Log groups allow you to open all log files for a single scenario. OneTrace currently includes groups for the following scenarios:

- Application management
- Compliance settings (also referred to as Desired Configuration Management)
- Software updates

For more information, see [Support Center OneTrace](../../support/support-center-onetrace.md).

### <a name="bkmk_extend"></a> Improvements to extend and migrate on-premises site to Microsoft Azure
<!--5665775, 6307931-->
The tool to extend and migrate on-premises site to Microsoft Azure now supports provisioning multiple site system roles on a single Azure virtual machine. You can add site system roles after the initial Azure virtual machine deployment has completed.

For more information, see [Extend and migrate on-premises site to Microsoft Azure](../../support/azure-migration-tool.md#add-site-roles-to-an-existing-vm).

## Other updates

Starting with this version, the following features are no longer [pre-release](../../servers/manage/pre-release-features.md):

- [Azure Active Directory user group discovery](../../servers/deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco)<!--3611956-->
- [Synchronize collection membership results to Azure Active Directory](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync)<!--3607475-->
- [CMPivot standalone](../../servers/manage/cmpivot.md#bkmk_standalone)<!--3555890/4692885-->
- [Client apps for co-managed devices](../../../comanage/workloads.md#client-apps) (previously known as *Mobile apps for co-managed devices*)<!-- 1357892/3600959 -->

For more information on changes to the Windows PowerShell cmdlets for Configuration Manager, see [PowerShell version 2002 release notes](/powershell/sccm/2002-release-notes).

For more information on changes to the administration service REST API, see [Administration service release notes](../../../develop/adminservice/release-notes.md#bkmk_2002).

Aside from new features, this release also includes additional changes such as bug fixes. For more information, see [Summary of changes in Configuration Manager current branch, version 2002](https://support.microsoft.com/help/4556203).

The following update rollup (4560496) is available in the console starting on July 15, 2020: [Update rollup for Microsoft Configuration Manager version 2002](https://support.microsoft.com/help/4560496).

### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4575339](https://support.microsoft.com/help/4575339) | Devices appear twice in Microsoft Configuration Manager admin center | July 23, 2020 | No |
| [4575774](https://support.microsoft.com/help/4575774) | New-CMTSStepPrestartCheck cmdlet fails in Configuration Manager, version 2002 | July 24, 2020 | No |
| [4576782](https://support.microsoft.com/help/4576782) | Application blade times out in Microsoft Intune admin center | August 11, 2020 | No |
| [4578123](https://support.microsoft.com/help/4578123) | CMPivot queries return unexpected results in Configuration Manager, version 2002 | August 24, 2020 | No |
| [4575783](https://support.microsoft.com/help/4575783) | Office updates fail to download in Configuration Manager current branch, version 2002 | November 11, 2020 | Yes |
<!--
> [!NOTE]
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](../../servers/manage/updates.md#bkmk_supersede).
-->

## Next steps

<!-- At this time, version 2002 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-2002.md#early-update-ring). -->

As of May 11, 2020, version 2002 is globally available for all customers to install.

When you're ready to install this version, see [Installing updates for Configuration Manager](../../servers/manage/updates.md) and [Checklist for installing update 2002](../../servers/manage/checklist-for-installing-update-2002.md).

> [!TIP]
> To install a new site, use a baseline version of Configuration Manager.
>
> Learn more about:
>
> - [Installing new sites](../../servers/deploy/install/installing-sites.md)
> - [Baseline and update versions](../../servers/manage/updates.md#bkmk_Baselines)

For known significant issues, see the [Release notes](../../servers/deploy/install/release-notes.md).

After you update a site, also review the [Post-update checklist](../../servers/manage/checklist-for-installing-update-2002.md#post-update-checklist).
