---
title: What's new in version 2207
titleSuffix: Configuration Manager
description: Get details about changes and new capabilities introduced in version 2207 of Configuration Manager current branch.
ms.date: 08/12/2022
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: paasin
ms.author: paasin
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: highpri
---

# What's new in version 2207 of Configuration Manager current branch

*Applies to: Configuration Manager (current branch)*

Update 2207 for Configuration Manager current branch is available as an in-console update. Apply this update on sites that run version 2103 or later. <!-- baseline only statement: When installing a new site, this version of Configuration Manager will also be available as a [baseline version](../../servers/manage/updates.md#bkmk_note1) soon after global availability of the in-console update.--> This article summarizes the changes and new features in Configuration Manager, version 2207.

Always review the latest checklist for installing this update. For more information, see [Checklist for installing update 2207](../../servers/manage/checklist-for-installing-update-2207.md). After you update a site, also review the [Post-update checklist](../../servers/manage/checklist-for-installing-update-2207.md#post-update-checklist).

To take full advantage of new Configuration Manager features, after you update the site, also update clients to the latest version. While new functionality appears in the Configuration Manager console when you update the site and console, the complete scenario isn't functional until the client version is also the latest.

## Cloud-attached management

### Enhanced security for Configuration Manager administration service
<!--12952905-->
We're introducing a new cloud application with limited access to the administration service. This feature allows cloud management gateway (CMG) to segment the admin privileges between a management point, and the administration service. This enables CMG to restrict access to the administration service. This feature gives admins granular access controls through which users can have access to the administration service and to enforce MFA if necessary.
 
For more information, see [Configure Azure services for use with Configuration Manager](../../servers/deploy/configure/azure-services-wizard.md).

### Simplified application deployment approval
<!--13351390#-->

An administrator can now approve or deny the request for deploying an application on a device from anywhere they have internet access by selecting a link in the email notification. This feature requires admins to manually add the CMG URL in the Azure Active Directory app as single page application redirect URI. 

For more information, see [Create an app registration in Azure AD for your app service app](/azure/app-service/configure-authentication-provider-aad#-create-an-app-registration-in-azure-ad-for-your-app-service-app).

<!--## Site infrastructure-->

### Include and prefer a cloud source for a management point in a default boundary group
<!--10674394-->
Until 2203 current branch, you didn’t have an option to prefer a CMG as a management point in a default boundary group. The clients falling back to a default boundary group could only communicate to non-cloud-based management points. 

When a site is initially installed, there's a default site boundary group created for each site, and all the clients use it by default until they're assigned to a custom boundary group.

Starting in Configuration Manager 2207, you can add options via PowerShell to include and prefer cloud sources. For instance, you can set the CMG as the preferred management point for the clients in the default boundary group.

For more information, see [
Default site boundary group behavior supports cloud source selection](../../../core/servers/deploy/configure/boundary-groups.md#default-site-boundary-group-behavior-supports-cloud-source-selection).

## Client management

### Granular control over compliance settings evaluation
<!--14120481-->
You can now define a **Script Execution Timeout (seconds)** when configuring client settings for compliance settings. The timeout value can be set from a minimum of 60 seconds to a maximum of 600 seconds. This new setting allows you more flexibility for configuration items when you need to run scripts that may exceed the default of 60 seconds.

For more information, see the [compliance settings group of client settings](../../clients/deploy/about-client-settings.md#compliance-settings).

<!--## Collections-->


 
<!-- ## Software Center -->

## Software updates

### Improved manageability of automatic deployment rules (ADRs)
<!--13507410-->

You'll now be able to organize ADRs with folders. This improvement helps you with better categorization and management of ADRs across your organizational hierarchy by having a structured view across your phased deployments. Folder can also be created with PowerShell cmdlets.

For more information, see [Process to create a folder for automatic deployment rules](../../../sum/deploy-use/automatically-deploy-software-updates.md#process-to-add-a-new-deployment-to-an-existing-adr).

### Enhanced control over monthly maintenance windows
<!--3601127#-->

Based upon your feedback, we have enhanced monthly maintenance windows scheduling. You can now set monthly maintenance window schedules to better align deployments with the release of monthly software updates by configuring offsets. For example, using an offset of two days after the second Tuesday of the month, sets the maintenance window for Thursday.

For more information, see [How to use maintenance windows in Configuration Manager](../../../core/clients/manage/collections/use-maintenance-windows.md). 

<!--## OS deployment-->


## Endpoint Protection

### Improved Microsoft Defender for Endpoint (MDE) onboarding for Windows Server 2012 R2 and Windows Server 2016 
<!--9265511-->
Configuration Manager version 2207 now supports automatic deployment of modern, unified Microsoft Defender for Endpoint for Windows Server 2012 R2 & 2016. Windows Server 2012 and 2016 devices that are targeted with Microsoft Defender for Endpoint onboarding policy will use the unified agent versus the existing Microsoft Monitoring Agent based solution, if configured through Client Settings.

For more information, see [Microsoft Defender for Endpoint onboarding](../../../protect/deploy-use/defender-advanced-threat-protection.md).

### Enhanced protection for untrusted environments
<!-- 14059872 -->

1. Windows Defender Application Guard is now called Microsoft Defender Application Guard in the console. 

1. The **General** settings page in the Microsoft Defender Application Guard now allows you to create policies within Configuration Manager to protect your employees using Microsoft Edge and isolated Windows environments. 

1. The **Application Behavior** settings page allows you to enable or disable cameras and microphones, along with certificate matching of the thumbprints to the isolated container. 

1. The following items were removed:
   - The Enterprise sites can load non-enterprise content, such as third-party plug-in settings, under the **Host interaction** page.
   - The file trust criteria policy, under the **File Management** page.
   
For more information, see [Create and deploy Microsoft Defender Application Guard policy](../../../protect/deploy-use/create-deploy-application-guard-policy.md#create-a-policy-and-to-browse-the-available-settings).

<!--## Application management-->



<!--## Community hub-->



## Configuration Manager console

### Improvements to the console

- When performing a search on any node in the console, the search bar will now include a **Path** criteria to show that subfolders in the node are included in the search. 
    
  - The path criteria is informational and can’t be edited.

  - By default, all subfolders will be searched when you perform a search in any node that contains subfolders. You can narrow down the search by selecting the “Current Node” option from the search toolbar. 

### Improvements to the dark theme

The dark theme has been available as a pre-release feature since 2203. In this release we've extended the dark theme to additional components such as buttons, context menus, and hyperlinks. Enable this pre-release feature to experience the dark theme.
  

<!--14908615-->

For more information, see [Console changes and tips](../../servers/manage/admin-console-tips.md#bkmk_2207).



<!--## Tools-->

<!--## Deprecated features

Learn about support changes before they're implemented in [removed and deprecated items](deprecated/removed-and-deprecated.md).

The following features are deprecated. You can still use them now, but Microsoft plans to end support in the future.



As previously announced, version 2207 drops support for the following features:
-->

## Other updates

<!--Starting with this version, the following features are no longer [pre-release](../../servers/manage/pre-release-features.md):
-->

For more information on changes to the Windows PowerShell cmdlets for Configuration Manager, see [version 2207 release notes](/powershell/sccm/2207-release-notes).

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


At this time, version 2207 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-2207.md#early-update-ring).


<!--As of April 26, 2022, version 2207 is globally available for all customers to install.-->

When you're ready to install this version, see [Installing updates for Configuration Manager](../../servers/manage/updates.md) and [Checklist for installing update 2207](../../servers/manage/checklist-for-installing-update-2207.md).

> [!TIP]
> To install a new site, use a baseline version of Configuration Manager.
>
> Learn more about:
>
> - [Installing new sites](../../servers/deploy/install/installing-sites.md)
> - [Baseline and update versions](../../servers/manage/updates.md#bkmk_Baselines)

For known significant issues, see the [Release notes](../../servers/deploy/install/release-notes.md).

After you update a site, also review the [Post-update checklist](../../servers/manage/checklist-for-installing-update-2207.md#post-update-checklist).
