---
title: What's new in version 1910
titleSuffix: Configuration Manager
description: Get details about changes and new capabilities introduced in version 1906 of Configuration Manager current branch.
ms.date: 11/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3e1ddb65-1193-46ce-a7c0-a48dfd9fd833
author: mestew
ms.author: mstewart
manager: dougeby 
ms.collection: M365-identity-device-management
---

# What's new in version 1910 of Configuration Manager current branch

*Applies to: Configuration Manager (current branch)*

Update 1910 for Configuration Manager current branch is available as an in-console update. Apply this update on sites that run version 1806 or later. <!-- baseline only statement:When installing a new site, it's also available as a baseline version.--> This article summarizes the changes and new features in Configuration Manager, version 1910.  

Always review the latest checklist for installing this update. For more information, see [Checklist for installing update 1910](/sccm/core/servers/manage/checklist-for-installing-update-1910). After you update a site, also review the [Post-update checklist](/sccm/core/servers/manage/checklist-for-installing-update-1910#post-update-checklist).

To take full advantage of new Configuration Manager features, after you update the site, also update clients to the latest version. While new functionality appears in the Configuration Manager console when you update the site and console, the complete scenario isn't functional until the client version is also the latest.

> [!Note]  
> This article currently lists all significant features in this version. However, not all sections yet link to updated content with further information on the new features. Keep checking this page regularly for updates. Changes are noted with the ***[Updated]*** tag. This note will be removed when the content is finalized.

> [!Tip]  
> To get notified when this page is updated, copy and paste the following URL into your RSS feed reader:
> `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+1910+-+Configuration+Manager%22&locale=en-us`

## <a name="bkmk_mem"></a> Microsoft Endpoint Configuration Manager

<!--4960084-->

Configuration Manager is now part of Microsoft Endpoint Manager.

![Microsoft Endpoint Configuration Manager](media/4960084-endpoint-manager-logo.png)

Microsoft Endpoint Manager is an integrated solution for managing all of your devices. Microsoft brings together Configuration Manager and Intune, without a complex migration, and with simplified licensing. Continue to leverage your existing Configuration Manager investments, while taking advantage of the power of the Microsoft cloud at your own pace.

The following Microsoft management solutions are all now part of the **Microsoft Endpoint Manager** brand:

- [Configuration Manager](https://docs.microsoft.com/configmgr)
- [Intune](https://docs.microsoft.com/intune)
- [Desktop Analytics](/configmgr/desktop-analytics/overview)
- [Autopilot](https://docs.microsoft.com/intune/enrollment/enrollment-autopilot)
- Other features in the [Device Management Admin Console](https://go.microsoft.com/fwlink/?linkid=2109094)

For more information, see the following posts from Brad Anderson, Microsoft corporate vice president for Microsoft 365:

- [Announcement blog post](https://aka.ms/cmannounce)
- [Vision paper](https://aka.ms/MEMVisionPaper)
- [Announcement summary video](https://youtu.be/GS7oNPInFuw)

### What things change in Configuration Manager with Microsoft Endpoint Manager?

In version 1910, aside from several string changes, Configuration Manager still functions the same. A few of the string changes may impact your use of the following components:

- **Configuration Manager console**: Find shortcuts to the console and the **Remote Control Viewer** under the Windows Start menu in the **Microsoft Endpoint** folder.

- **Software Center**: Find the Software Center shortcut under the Windows Start menu in the **Microsoft Endpoint Manager** folder.

![Microsoft Endpoint start menu icons](media/microsoft-endpoint-start-menu.png)

Make sure to update any internal documentation that you maintain to include these new locations.

> [!TIP]
> In Windows 10, when you open the Start menu, just start typing the name to find the icon. For example, `config` for the Configuration Manager console, and `software` for Software Center.

## <a name="bkmk_infra"></a> Site infrastructure

### Reclaim SEDO lock

<!--4786915-->

Starting in [current branch version 1906](/configmgr/core/plan-design/changes/whats-new-in-version-1906#reclaim-sedo-lock-for-task-sequences), you could clear your lock on a task sequence. Now you can clear your lock on any object in the Configuration Manager console.

For more information, see [Using the Configuration Manager console](/configmgr/core/servers/manage/admin-console#bkmk_sedo).

### Extend and migrate on-premises site to Microsoft Azure
<!--3556022-->

This new tool helps you to programmatically create Azure virtual machines (VMs) for Configuration Manager. It can install with default settings site roles like a passive site server, management points, and distribution points. Once you validate the new roles, use them as additional site systems for high availability. You can also remove the on-premises site system role and only keep the Azure VM role.

For more information, see [Extend and migrate on-premises site to Microsoft Azure](/sccm/core/support/azure-migration-tool).

<!-- ## <a name="bkmk_cloud"></a> Cloud-attached management -->

## <a name="bkmk_da"></a> Desktop Analytics

For more information on the monthly changes to the Desktop Analytics cloud service, see [What's new in Desktop Analytics](/configmgr/desktop-analytics/whats-new).

## <a name="bkmk_real"></a> Real-time management

### Optimizations to the CMPivot engine
<!--3197353-->
We've added some significant optimizations to the CMPivot engine that allows us to push more of the processing to the ConfigMgr client. The optimizations drastically reduce the network and server CPU load needed to run CMPivot queries. With these optimizations, we can now sift through gigabytes of client data in real time. For more information, see [Optimizations to the CMPivot engine](/sccm/core/servers/manage/cmpivot#bkmk_optimization).

### Additional CMPivot Entities and Enhancements
<!--5410930-->'
We've added a number of new CMPivot entities and entity enhancements to aid in troubleshooting and hunting. We've included the following entities to query:

- Windows event logs ([WinEvent](/sccm/core/servers/manage/cmpivot#bkmk_WinEvent))
- File content ([FileContent](/sccm/core/servers/manage/cmpivot#bkmk_File))
- Dlls loaded by processes ([ProcessModule](/sccm/core/servers/manage/cmpivot#bkmk_ProcessModule))
- Azure Active Directory information ([AADStatus](/sccm/core/servers/manage/cmpivot#bkmk_AadStatus))
- Endpoint protection status ([EPStatus](/sccm/core/servers/manage/cmpivot#bkmk_EPStatus))

This release also includes several [other enhancements](/sccm/core/servers/manage/cmpivot#bkmk_Other) to CMPivot. For more information, see [CMPivot starting in version 1910](/sccm/core/servers/manage/cmpivot#bkmk_cmpivot1910).

## <a name="bkmk_content"></a> Content management

### Microsoft Connected Cache support for Intune Win32 apps

<!--5032900-->

When you enable Microsoft Connected Cache on your Configuration Manager distribution points, they can now serve Microsoft Intune Win32 apps to co-managed clients.

> [!NOTE]
> Configuration Manager current branch version 1906 included [Delivery Optimization In-Network Cache](/configmgr/core/plan-design/hierarchy/delivery-optimization-in-network-cache), an application installed on Windows Server that's still in development. Starting in current branch version 1910, this feature is now called **Microsoft Connected Cache**.
>
> When you install Connected Cache on a Configuration Manager distribution point, it offloads Delivery Optimization service traffic to local sources. Connected Cache does this behavior by efficiently caching content at the byte range level.

## <a name="bkmk_client"></a> Client management

### Include custom configuration baselines as part of compliance policy assessment
<!--3608345-->

You can now add evaluation of custom configuration baselines as a compliance policy assessment rule. When you create or edit a configuration baseline, you have an option to **Evaluate this baseline as part of compliance policy assessment**. When adding or editing a compliance policy rule, you have a condition called **Include configured baselines in compliance policy assessment**.

 For a co-managed device and when Intune is configured to take ConfigMgr compliance assessment result as part of the overall compliance status that gets sent to Azure Active Directory and be used for conditional access to customers' Office 365 resources.

For more information, see [Include custom configuration baselines as part of compliance policy assessment](/sccm/compliance/deploy-use/create-configuration-baselines#bkmk_CAbaselines).

### Enable user policy for Windows 10 Enterprise multi-session

<!--4737447-->

Configuration Manager current branch version 1906 introduced support for [Windows Virtual Desktop](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices#windows-virtual-desktop). This Microsoft Azure environment supports several OS versions, some of which allow multiple concurrent active user sessions. For example, Windows 10 Enterprise multi-session.

If you require user policy on these multi-session devices, and accept any potential performance impact, you can now configure a client setting to enable user policy. In the **Client Policy** group, configure the following setting: **Enable user policy for multiple user sessions**.

For more information, see [How to configure client settings](/configmgr/core/clients/deploy/configure-client-settings).


<!-- ## <a name="bkmk_comgmt"></a> Co-management -->


## <a name="bkmk_app"></a> Application management

### Deploy Microsoft Edge, version 77 and later
<!--4561024-->
The all-new Microsoft Edge is ready for business. You can now deploy Microsoft Edge, version 77 and later to your users. Admins can pick the Beta or Dev channel, along with a version of the Microsoft Edge client to deploy.

For more information, see [Deploy Microsoft Edge, version 77 and later](/sccm/apps/deploy-use/deploy-edge).

### Improvements to application groups

<!--4760058-->

Starting in current branch version 1906, you can create a group of applications to send to a device collection as a single deployment. This release improves upon this feature:

- Users can **Uninstall** the app group in Software Center.

- You can deploy an app group to a **user collection**.

For more general information, see [Create application groups](/configmgr/apps/deploy-use/create-app-groups).


## <a name="bkmk_osd"></a> OS deployment

### Improvements to the task sequence editor

- **Search the task sequence editor**<!--4621085-->: If you have a large task sequence with many groups and steps, it can be difficult to find specific steps. You can now search in the task sequence editor. This action lets you more quickly locate steps in the task sequence.

- **Copy and paste task sequence conditions**<!--4621098-->: If you want to reuse the conditions from one task sequence step to another, you can now copy and paste conditions in the task sequence editor.

For more information, see the new article on how to [Use the task sequence editor](/configmgr/osd/understand/task-sequence-editor).

### Task sequence performance improvements - power plans

<!--3555926-->

You can now run a task sequence with the high performance power plan. This option improves the overall speed of the task sequence. It configures Windows to use its built-in high performance power plan, which delivers maximum performance at the expense of higher power consumption.

For more information, see [Performance improvements for power plans](/configmgr/osd/deploy-use/manage-task-sequences-to-automate-tasks#bkmk_perf).

### Task sequence download on demand over the internet

<!--3601238-->

You can use the task sequence to deploy Windows 10 in-place upgrade via cloud management gateway (CMG). However, it requires the deployment to download all content locally before starting the task sequence.

Starting in this release, the task sequence engine can download packages on-demand from a content-enabled CMG or a cloud distribution point. This change provides additional flexibility with your Windows 10 in-place upgrade deployments to internet-based devices.

For more information, see [Deploy Windows 10 in-place upgrade via CMG](/configmgr/osd/deploy-use/deploy-a-task-sequence#deploy-windows-10-in-place-upgrade-via-cmg).

### Improvements to OS deployment

This release includes the following improvements to OS deployment:

#### Boot image keyboard layout

<!--4910348-->

Configure the default keyboard layout for a boot image. On the **Customization** tab of a boot image, use the new option to **Set default keyboard layout in WinPE**. If you select a language other than en-us, Configuration Manager still includes en-us in the available input locales. On the device, the initial keyboard layout is the selected locale, but the user can switch the device to en-us if needed.

For more information, see [Manage boot images](/configmgr/osd/get-started/manage-boot-images#customization).

#### Import a single index of an OS upgrade package

<!--4931110-->

When importing an OS upgrade package, you can **Extract a specific image index from install.wim file of selected upgrade package**. This behavior is similar as with [OS images](/configmgr/osd/get-started/manage-operating-system-images#BKMK_AddOSImages), except it overwrites the existing install.wim in the OS upgrade package. It extracts the image index to a temporary location, and then moves it into the original source directory.

For more information, see [Manage OS upgrade packages](/configmgr/osd/get-started/manage-operating-system-upgrade-packages#BKMK_AddOSUpgradePkgs).

#### Output the results of a Run Command Line step to a variable during a task sequence

<!--user story 4977616/bug 4798352-->

The **Run Command Line** step now includes an option to **Output to task sequence variable**. When you enable this option, the task sequence saves the output from the command to a custom task sequence variable that you specify.

For more information, see [Run Command Line](/configmgr/osd/understand/task-sequence-steps#BKMK_RunCommandLine).

#### Improvements to task sequence debugger

This release includes the following improvements to the task sequence debugger:

- Use the new task sequence variable **TSDebugOnError** to automatically start the debugger when the task sequence returns an error.<!-- 5012536 -->

- If you create a breakpoint in the debugger, and then the task sequence restarts the computer, the debugger keeps the breakpoints after restart.<!-- 5012509 -->

For more information, see [Task sequence debugger](/configmgr/osd/deploy-use/debug-task-sequence) and [Task sequence variables - TSDebugOnError](/configmgr/osd/understand/task-sequence-variables#TSDebugOnError).

#### Improved language support in task sequence

<!--5411057, 5138936-->

This release adds control over language configuration during OS deployment. If you're already applying these language settings, this change can help you simplify your OS deployment task sequence. Instead of using multiple steps per language or separate scripts, use one instance per language of the built-in **Apply Windows Settings** step with a condition for that language.

Use the **Apply Windows Settings** task sequence step to configure the following new settings:

- Input locale (default keyboard layout)
- System locale
- UI language
- UI language fallback
- User locale

For more information, see [Apply Windows Settings](/configmgr/osd/understand/task-sequence-steps#BKMK_ApplyWindowsSettings).

#### New variable for Windows 10 in-place upgrade

<!--4680263-->

To address timing issues with the Window 10 in-place upgrade task sequence on high performance devices when Windows setup is complete, you can now set a new task sequence variable **SetupCompletePause**. When you assign a value in seconds to this variable, the Windows setup process delays that amount of time before it starts the task sequence. This timeout provides the Configuration Manager client additional time to initialize.

For more information, see [Task sequence variables - SetupCompletePause](/configmgr/osd/understand/task-sequence-variables#SetupCompletePause).

<!-- ## <a name="bkmk_userxp"></a> Software Center -->

## <a name="bkmk_sum"></a> Software updates

### Additional options for third-party update catalogs
<!--4469002-->
You now have more granular controls over synchronization of third party updates catalogs. Starting in Configuration Manager version 1910, you can configure the synchronization schedule for each catalog independently. When using catalogs that include categorized updates, you can configure synchronization to include only specific categories of updates to avoid synchronizing the entire catalog. With categorized catalogs, when you're confident you'll deploy a category, you can configure it to automatically download and publish to WSUS.

For more information, see [Enable third-party updates](/sccm/sum/deploy-use/third-party-software-updates#bkmk_1910).

### Use Delivery Optimization for all Windows updates
<!--4699118-->
Previously, Delivery Optimization could be leveraged only for express updates. With Configuration Manager version 1910, it’s now possible to use Delivery Optimization for the distribution of all Windows Update content for clients running Windows 10 version 1709 or later.

For more information, see [Optimize Windows 10 update delivery](/sccm/sum/deploy-use/optimize-windows-10-update-delivery#bkmk_DO-1910) and [Client settings for software updates](/sccm/core/clients/deploy/about-client-settings#software-updates).

### Additional software update filter for ADRs
<!--4852033-->
You can now use **Deployed** as an update filter for your automatic deployment rules. This filter helps identify new updates that may need to be deployed to your pilot or test collections.

For more information see [Automatically deploy software updates](/sccm/sum/deploy-use/automatically-deploy-software-updates#bkmk_adr-process)

## <a name="bkmk_o365"></a> Office management


### Office 365 ProPlus Pilot and Health Dashboard
<!--4488272, 4488301-->

The **Office 365 ProPlus Pilot and Health Dashboard** helps you plan, pilot, and perform your Office 365 ProPlus deployment. The dashboard provides health insights for devices with Office 365 ProPlus to help identify possible issues that may affect your deployment plans. The **Office 365 ProPlus Pilot and Health Dashboard** provides a recommendation for pilot devices based on add-in inventory. For more information, see [Office 365 ProPlus pilot and health dashboard](/sccm/sum/deploy-use/office-365-dashboard#bkmk_pilot).

## <a name="bkmk_protect"></a> Protection

### BitLocker management

<!--3601034-->

Configuration Manager now provides the following management capabilities for BitLocker Drive Encryption:

- Deploy the BitLocker client to managed Windows devices
- Manage device encryption polices
- Compliance reports
- Administration and monitoring website for key recovery
- A user self-service portal

For more information, see [Plan for BitLocker management](/configmgr/protect/plan-design/bitlocker-management).

## <a name="bkmk_admin"></a> Configuration Manager console

### View active consoles and message administrators through Console Connections
<!--4923997-->
We've made the following improvements to **Console Connections**:

- The ability to message other Configuration Manager administrators through Microsoft Teams.
- The **Last Console Heartbeat** column has replaced the **Last Connected Time** column.
  - An open console in the foreground sends a heartbeat every 10 minutes to help determine which console connections are currently active.

For more information, see [View recently connected consoles](/sccm/core/servers/manage/admin-console#bkmk_viewconnected) and [Message administrators](/sccm/core/servers/manage/admin-console#bkmk_message).

### Client diagnostics actions

<!--4433455-->

There are new device actions for **Client Diagnostics** in the Configuration Manager console:

- **Enable verbose logging**: Change the global log level for the CCM component to verbose, and enable debug logging.
- **Disable verbose logging**: Change the global log level to default, and disable debug logging.

For more information, see [Client diagnostics](/sccm/core/clients/manage/client-notification#client-diagnostics).

### Improvements to console search
<!--4640570-->

This release includes the following improvements to search in the Configuration Manager console:

- You can now use the **All Subfolders** search option from the **Driver Packages** and **Queries** nodes.<!--2841181,5424892-->

- When a search returns more than 1,000 results, now select the **OK** button on the notice bar to view more results.<!--4640570-->

## Other updates

For more information on changes to the Windows PowerShell cmdlets for Configuration Manager, see [PowerShell version 1910 release notes](https://docs.microsoft.com/powershell/sccm/1910-release-notes?view=sccm-ps).

<!--
As of this version, the following features are no longer pre-release:
- [SMS Provider administration service](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider#bkmk_admin-service)
- [Device Guard management](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager)

Aside from new features, this release also includes additional changes such as bug fixes. For more information, see [Summary of changes in Configuration Manager current branch, version 1906](https://support.microsoft.com/help/4514258).

The following update rollup (4517869) is available in the console starting on October 1, 2019: [Update rollup for Configuration Manager current branch, version 1906](https://support.microsoft.com/help/4517869).

-->

<!--
### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4487960](https://support.microsoft.com/help/4487960) | Microsoft Intune connector certificate does not renew in Configuration Manager | 18 January 2019 | Yes |

> [!Note]  
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](/sccm/core/servers/manage/updates#bkmk_supersede).
-->

## Next steps

At this time, version 1910 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](/sccm/core/servers/manage/checklist-for-installing-update-1910#early-update-ring).
<!--As of August 16, 2019, version 1906 is globally available for all customers to install.-->

When you're ready to install this version, see [Installing updates for Configuration Manager](/sccm/core/servers/manage/updates) and [Checklist for installing update 1910](/sccm/core/servers/manage/checklist-for-installing-update-1910).

> [!TIP]  
> To install a new site, use a baseline version of Configuration Manager.  
>
> Learn more about:
>
> - [Installing new sites](/sccm/core/servers/deploy/install/installing-sites)  
> - [Baseline and update versions](/sccm/core/servers/manage/updates#bkmk_Baselines)  

For known, significant issues, see the [Release notes](/sccm/core/servers/deploy/install/release-notes).

After you update a site, also review the [Post-update checklist](/sccm/core/servers/manage/checklist-for-installing-update-1910#post-update-checklist).
