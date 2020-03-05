---
title: What's new in version 2002
titleSuffix: Configuration Manager
description: Get details about changes and new capabilities introduced in version 2002 of Configuration Manager current branch.
ms.date: 03/20/2020
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: de718cdc-d0a9-47e2-9c99-8fa2cb25b5f8
author: mestew
ms.author: mstewart
manager: dougeby 
---

# What's new in version 2002 of Configuration Manager current branch

*Applies to: Configuration Manager (current branch)*

Update 2002 for Configuration Manager current branch is available as an in-console update. Apply this update on sites that run version 1806 or later. <!-- baseline only statement:-->When installing a new site, it's also available as a baseline version. This article summarizes the changes and new features in Configuration Manager, version 2002.

Always review the latest checklist for installing this update. For more information, see [Checklist for installing update 2002](/sccm/core/servers/manage/checklist-for-installing-update-2002). After you update a site, also review the [Post-update checklist](/sccm/core/servers/manage/checklist-for-installing-update-2002#post-update-checklist).

To take full advantage of new Configuration Manager features, after you update the site, also update clients to the latest version. While new functionality appears in the Configuration Manager console when you update the site and console, the complete scenario isn't functional until the client version is also the latest.

> [!TIP]
> To get notified when this page is updated, copy and paste the following URL into your RSS feed reader:
> `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+2002+-+Configuration+Manager%22&locale=en-us`

## <a name="bkmk_infra"></a> Site infrastructure

### Remove a central administration site

<!-- 3607277 -->

Lorem ipsum dolor sit amet, consectetuer adipiscing elit.

<!-- For more information, see [](). -->

### New management insight rules from Microsoft Services

<!-- 3607758 -->

This release includes additional management insight rules courtesy of Microsoft Premier Field Engineering. These rules are a sample of the many more checks that Microsoft Premier provides in the Services Hub.

<!-- For more information, see [Management insights](/configmgr/core/servers/manage/management-insights). -->

### Improvements to administration service

<!-- 5728365 -->

The administration service is a REST API for the SMS Provider. Previously, you had to implement one of the following dependencies:

- Enable Enhanced HTTP for the entire site
- Manually bind a PKI-based certificate to IIS on the server that hosts the SMS Provider role

Starting in this release, the administration service automatically uses the site's self-signed certificate. This change helps reduce the friction for easier use of the administration service. The site always generates this certificate. The Enhanced HTTP site setting to Use Configuration Manager-generated certificates for HTTP site systems only controls whether site systems use it or not. Now the administration service ignores this site setting, as it always uses the site's certificate even if no other site system is using Enhanced HTTP.

<!-- For more information, see [](). -->

### Proxy support for Azure Active Directory discovery and group sync

<!-- 5913817 -->

The site system's proxy settings, including authentication, are now used by:

- Azure Active Directory (Azure AD) user discovery
- Azure AD user group discovery
- Synchronizing collection membership results to Azure Active Directory groups

<!-- For more information, see [Proxy server support](/configmgr/core/plan-design/network/proxy-server-support). -->


## <a name="bkmk_cloud"></a> Cloud-attached management

### Critical status message shows server connection errors to required endpoints

<!-- 5566763 -->

If the Configuration Manager site server fails to connect to required endpoints for a cloud service, it raises a critical status message ID 11488. When the site server can't connect to the service, the SMS_SERVICE_CONNECTOR component status changes to critical. View detailed status in the Component Status node of the Configuration Manager console.

<!-- For more information, see [](). -->

### Token-based authentication for cloud management gateway

<!-- 5686290 -->

The cloud management gateway (CMG) supports many types of clients, but even with Enhanced HTTP, these clients require a client authentication certificate. This certificate requirement can be challenging to provision on internet-based clients that don't often connect to the internal network, aren't able to join Azure Active Directory (Azure AD), and don't have a method to install a PKI-issued certificate.

Configuration Manager extends its device support with the following methods:

- Register on the internal network for a unique token
- Create a bulk registration token for internet-based devices

<!-- For more information, see [](). -->

## <a name="bkmk_da"></a> Desktop Analytics

For more information on the monthly changes to the Desktop Analytics cloud service, see [What's new in Desktop Analytics](/configmgr/desktop-analytics/whats-new).

### Connection Health dashboard shows client connection issues

<!-- 4963230, 4963383 -->

Use the Desktop Analytics Connection Health dashboard in Configuration Manager to monitor the clients' connectivity health. It now helps you to more easily identify any client connectivity issues in two areas:

<!-- For more information, see [](). -->


## <a name="bkmk_real"></a> Real-time management

### Improvements to CMPivot

<!-- 5870934 -->

We've made it easier to navigate CMPivot entities. Starting in this technical preview, you can search CMPivot entities and see entity properties.

<!-- For more information, see [CMPivot](configmgr/core/servers/manage/cmpivot). -->


## <a name="bkmk_content"></a> Content management

### Exclude certain subnets for peer content download

<!-- 3555777 -->

Boundary groups include the following option for peer downloads: During peer downloads, only use peers within the same subnet. If you enable this option, the management point only includes in the content location list peer sources that are in the same subnet and boundary group as the client. For more information on this option, see Boundary group options for peer downloads.

Depending on the configuration of your network, you can now exclude certain subnets for matching. For example, you want to include a boundary but exclude a specific VPN subnet. By default, Configuration Manager excludes the default Teredo subnet (2001:0000:%).

<!-- For more information, see [Boundary group options](/configmgr/core/servers/deploy/configure/boundary-groups#bkmk_bgoptions). -->


## <a name="bkmk_client"></a> Client management

### Client log collection

<!-- 4226618 -->

You can now trigger a client device to upload its client logs to the site server by sending a client notification action from the Configuration Manager console.

<!-- For more information, see [Client notification](/configmgr/core/clients/manage/client-notification#client-diagnostics). -->

### Wake up a device from the central administration site

<!-- 6030715 -->

From the central administration site (CAS), in the Devices or Device Collections node, you can now use the client notification action to Wake Up devices. This action was previously only available from a primary site.

<!-- For more information, see [How to configure Wake on LAN](/configmgr/core/clients/deploy/configure-wake-on-lan#bkmk_wol-1810). -->


<!-- ## <a name="bkmk_comgmt"></a> Co-management -->


## <a name="bkmk_app"></a> Application management

### Microsoft Edge management dashboard

<!-- 3871913 -->

The Microsoft Edge management dashboard provides you insights on the usage of Microsoft Edge and other browsers. In this dashboard, you can:

- See how many of your devices have Microsoft Edge installed
- See how many clients have different versions of Microsoft Edge installed
- Have a view of the installed browsers across devices

From the Software Library workspace, click Microsoft Edge Management to see the dashboard. Change the collection for the graph data by clicking Browse and choosing another collection. By default your five largest collections are in the drop-down list. When you select a collection that isn't in the list, the newly selected collection takes the bottom spot on your drop-down list.

<!-- For more information, see [Microsoft Edge management](/configmgr/apps/deploy-use/deploy-edge). -->

### Improvements to Microsoft Edge management

<!-- 4561024 -->

You can now create a Microsoft Edge application that's set up to receive automatic updates rather than having automatic updates disabled. This change allows you to choose to manage updates for Microsoft Edge with Configuration Manager or allow Microsoft Edge to automatically update. When creating the application, select Allow Microsoft Edge to automatically update the version of the client on the end user's device on the Microsoft Edge Settings page.

<!-- For more information, see [Microsoft Edge management](/configmgr/apps/deploy-use/deploy-edge). -->

### Task sequence as an app model deployment type

<!-- 3555953 -->

You can now install complex applications using task sequences via the application model. Add a deployment type to an app that's a task sequence, either to install or uninstall the app. This feature provides the following behaviors:

- Deploy an app task sequence to a user collection

- Display the app task sequence with an icon in Software Center. An icon makes it easier for users to find and identify the app task sequence.

- Define additional metadata for the app task sequence, including localized information

<!-- For more information, see [](). -->


## <a name="bkmk_osd"></a> OS deployment

### Bootstrap a task sequence immediately after client registration

<!-- 5526972 -->

When you install and register a new Configuration Manager client, and also deploy a task sequence to it, it's difficult to determine how soon after registration it will run the task sequence. This release introduces a new client setup property that you can use to start a task sequence on a client after it successfully registers with the site.

<!-- For more information, see [](). -->

### Improvements to Check Readiness task sequence step

<!-- 6005561 -->

You can now verify more device properties in the Check Readiness task sequence step. Use this step in a task sequence to verify the target computer meets your prerequisite conditions.

- Architecture of current OS
- Minimum OS version
- Maximum OS version
- Minimum client version
- Language of current OS
- AC power plugged in
- Network adapter is connected and not wireless

<!-- For more information, see [Task sequence steps - Check Readiness](/configmgr/osd/understand/task-sequence-steps#BKMK_CheckReadiness). -->

### Improvements to task sequence progress

<!-- 5932692 -->

The task sequence progress window now includes the following improvements:

- Shows the current step number, total number of steps, and percent completion
- Increased the width of the window to give you more space to better show the organization name in a single line

<!-- For more information, see [](). -->


### Improvements to OS deployment

This release includes the following improvements to OS deployment:

- The task sequence environment includes a new read-only variable, `_TSSecureBoot`.<!--5842295--> Use this variable to determine the state of secure boot on a UEFI-enabled device. <!-- For more information, see [Task sequence variables](/configmgr/osd/understand/task-sequence-variables). -->

- You can now set task sequence variables to configure the user context that the [Run Command Line](/configmgr/osd/understand/task-sequence-steps#BKMK_RunCommandLine) and [Run PowerShell Script](/configmgr/osd/understand/task-sequence-steps#BKMK_RunPowerShellScript) steps use.<!-- 5573175 --> For example, now you don't need to configure the **Run Command Line** step with a placeholder account to use the [SMSTSRunCommandLineUserName](/configmgr/osd/understand/task-sequence-variables#SMSTSRunCommandLineUserName) and [SMSTSRunCommandLineUserPassword](/configmgr/osd/understand/task-sequence-variables#SMSTSRunCommandLineUserPassword) variables.<!-- For more information, see [Task sequence steps](/configmgr/osd/understand/task-sequence-steps). -->

- Set the [Run PowerShell Script](/configmgr/osd/understand/task-sequence-steps#BKMK_RunPowerShellScript) **Parameters** property to a variable.<!-- 5690481 --> <!-- For more information, see [Task sequence steps](/configmgr/osd/understand/task-sequence-steps). -->

- The Configuration Manager PXE responder now sends status messages to the site server. This change makes it easier to troubleshoot OS deployments that use this service.<!-- 5568051 --> <!-- For more information, see [](). -->


<!-- ## <a name="bkmk_userxp"></a> Software Center -->


## <a name="bkmk_sum"></a> Software updates

### Orchestration groups

<!-- 3098816 -->

Create an orchestration group to better control the deployment of software updates to devices. Many server administrators need to carefully manage updates for specific workloads, and automate behaviors in between.

An orchestration group gives you the flexibility to update devices based on a percentage, a specific number, or an explicit order. You can also run a PowerShell script before and after the devices run the update deployment.

Members of an orchestration group can be any Configuration Manager client, not just servers. The orchestration group rules apply to the devices for all software update deployments to any collection that contains an orchestration group member. Other deployment behaviors still apply. For example, maintenance windows and deployment schedules.

<!-- For more information, see [](). -->

### Evaluate software updates after a servicing stack update

<!-- 4639943 -->

Configuration Manager now detects if a servicing stack update (SSU) is part of an installation for multiple updates. When an SSU is detected, it's installed first. After install of the SSU, a software update evaluation cycle runs to install the remaining updates. This change allows a dependent cumulative update to be installed after the servicing stack update. The device doesn't need to restart between installs, and you don't need to create an additional maintenance window. SSUs are installed first only for non-user initiated installs. For instance, if a user initiates an installation for multiple updates from Software Center, the SSU might not be installed first.

For more information, see [Plan for software updates](/configmgr/sum/plan-design/plan-for-software-updates#bkmk_SSU).

### Office 365 updates for disconnected software update points

<!-- 4065163 -->

You can use a new tool to import Office 365 updates from an internet-connected WSUS server into a disconnected Configuration Manager environment. Previously when you exported and imported metadata for software updated in disconnected environments, you were unable to deploy Office 365 updates. Office 365 updates require additional metadata downloaded from an Office API and the Office CDN, which isn't possible for disconnected environments.

For more information, see [Synchronize Office 365 updates from a disconnected software update point](/configmgr/sum/get-started/synchronize-office-updates-disconnected).


<!-- ## <a name="bkmk_o365"></a> Office management -->


## <a name="bkmk_protect"></a> Protection

### Expand Microsoft Defender Advanced Threat Protection (ATP) onboarding

<!-- 5229962 -->

Configuration Manager now expands its support for onboarding devices to Microsoft Defender ATP.<!-- For more information, see [Microsoft Defender Advanced Threat Protection](/sccm/protect/deploy-use/windows-defender-advanced-threat-protection#onboard-devices). -->

### Improvements to BitLocker management

<!-- 5925683 -->

The BitLocker management policy now includes additional settings, including policies for fixed and removable drives.

<!-- For more information, see [](). -->


## <a name="bkmk_report"></a> Reporting

### Integrate with Power BI Report Server

<!-- 3721603 -->

You can now integrate Power BI Report Server with Configuration Manager reporting. This integration gives you modern visualization and better performance. It adds console support for Power BI reports similar to what already exists with SQL Server Reporting Services.

<!-- For more information, see [](). -->


## <a name="bkmk_admin"></a> Configuration Manager console

### Attach files to feedback

<!-- 3556011 -->

You can now choose to attach log and diagnostic files when you use Send a Frown in the Configuration Manager console to send feedback to Microsoft. This additional information can help us more quickly determine the cause of the problem. Files included with feedback are transmitted and stored using Microsoft Error Reporting (also known as Windows Error Reporting).

<!-- For more information, see [Product feedback](/configmgr/core/understand/find-help#product-feedback). -->

### Send a smile improvements

<!-- 5891852 -->

When you Send a smile or Send a frown, a status message is created when the feedback is submitted. This improvement provides a record of:

- When the feedback was submitted
- Who submitted the feedback
- The feedback ID
- If the feedback submission was successful or not

A status message with an ID of 53900 is a successful submission and 53901 is a failed submission.

<!-- For more information, see [Product feedback](/configmgr/core/understand/find-help#BKMK_1806Feedback). -->


## <a name="bkmk_tools"></a> Tools

### OneTrace log groups

<!-- 5559993 -->

OneTrace now supports customizable log groups, similar to the feature in Support Center. Log groups allow you to open all log files for a single scenario. OneTrace currently includes groups for the following scenarios:

- Application management
- Compliance settings (also referred to as Desired Configuration Management)
- Software updates

<!-- For more information, see [Support Center OneTrace](/configmgr/core/support/support-center-onetrace). -->


## Other updates

As of this version, the following features are no longer pre-release:

- [Client apps for co-managed devices](/configmgr/comanage/workloads#client-apps) (previously known as *Mobile apps for co-managed devices*)

For more information on changes to the Windows PowerShell cmdlets for Configuration Manager, see [PowerShell version 2002 release notes](https://docs.microsoft.com/powershell/sccm/2002-release-notes?view=sccm-ps).

<!--
Aside from new features, this release also includes additional changes such as bug fixes. For more information, see [Summary of changes in Configuration Manager current branch, version 2002](https://support.microsoft.com/help/nnnnn).

The following update rollup (4517869) is available in the console starting on October 1, 2019: [Update rollup for Configuration Manager current branch, version 1906](https://support.microsoft.com/help/4517869).

-->

<!--
### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4487960](https://support.microsoft.com/help/4487960) | Microsoft Intune connector certificate does not renew in Configuration Manager | 18 January 2019 | Yes |

> [!NOTE]  
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](/sccm/core/servers/manage/updates#bkmk_supersede).
-->

## Next steps

At this time, version 2002 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](/sccm/core/servers/manage/checklist-for-installing-update-2002#early-update-ring).
<!-- As of December 20, 2019, version 2002 is globally available for all customers to install. -->

When you're ready to install this version, see [Installing updates for Configuration Manager](/sccm/core/servers/manage/updates) and [Checklist for installing update 2002](/sccm/core/servers/manage/checklist-for-installing-update-2002).

> [!TIP]
> To install a new site, use a baseline version of Configuration Manager.
>
> Learn more about:
>
> - [Installing new sites](/sccm/core/servers/deploy/install/installing-sites) 
> - [Baseline and update versions](/sccm/core/servers/manage/updates#bkmk_Baselines) 

For known significant issues, see the [Release notes](/sccm/core/servers/deploy/install/release-notes).

After you update a site, also review the [Post-update checklist](/sccm/core/servers/manage/checklist-for-installing-update-2002#post-update-checklist).
