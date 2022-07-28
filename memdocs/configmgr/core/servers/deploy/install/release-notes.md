---
title: Release notes
titleSuffix: Configuration Manager
description: Learn about urgent issues that aren't yet fixed in the product or covered in a Microsoft Support knowledge base article.
ms.date: 08/01/2022
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: troubleshooting
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
---

# Release notes for Configuration Manager

*Applies to: Configuration Manager (current branch)*

With Configuration Manager, product release notes are limited to urgent issues. These issues aren't yet fixed in the product, or detailed in a [troubleshooting article](/troubleshoot/mem/configmgr/).

Feature-specific documentation includes information about known issues that affect core scenarios.

This article contains release notes for the current branch of Configuration Manager. For information on the technical preview branch, see [Technical Preview](../../../get-started/technical-preview.md).

For information about the new features introduced with different versions, see the following articles:

- [What's new in version 2207](../../../plan-design/changes/whats-new-in-version-2207.md)
- [What's new in version 2203](../../../plan-design/changes/whats-new-in-version-2203.md)
- [What's new in version 2111](../../../plan-design/changes/whats-new-in-version-2111.md)
- [What's new in version 2107](../../../plan-design/changes/whats-new-in-version-2107.md)
- [What's new in version 2103](../../../plan-design/changes/whats-new-in-version-2103.md)

> [!TIP]
> You can use RSS to be notified when this page is updated. For more information, see [How to use the docs](../../../../../use-docs.md#notifications).
<!-- > To get notified when this page is updated, copy and paste the following URL into your RSS feed reader:
> `https://docs.microsoft.com/api/search/rss?search=%22release+notes+-+Configuration+Manager%22&locale=en-us` -->

## Client management

### Some policies may not apply to upgraded clients

<!-- 10608021 -->
_Applies to version 2107 early update ring_

When you upgrade the client from versions 2010 or 2103 to version 2107, the following policies may not apply on some devices:

- Co-management policies on Windows 10 Enterprise multi-session devices such as Azure Virtual Desktop, and Windows 11 Insider Preview devices
- Desktop Analytics on any Windows version
- Windows Update for Business policies on Windows 10 x86 and ARM
- Microsoft Edge browser profiles on Windows 10 x64 and x86

> [!NOTE]
> The timing of how clients apply and evaluate these policies is non-deterministic. Even if you have these policies and these supported platforms, they may not immediately experience this issue.

When you look at the **Configurations** tab of the Configuration Manager control panel on the client, it will be blank.

This issue is fixed in the build of version 2107 that's now generally available for all customers. If you previously opted in to the early update ring, install the [Update for Microsoft Endpoint Configuration Manager version 2107, early update ring](../../../../hotfix/2107/10503003.md).

## Set up and upgrade

### Version 2107 update fails to download

<!--9791281,10237384-->
_Applies to: version 2107 and later_

The update for Configuration Manager version 2107 is available to download, but it fails to download. The **dmpdownloader.log** on the service connection point has entries similar to the following:

```log
Download large file with BITs
WARNING: EasySetupDownloadSinglePackage Failed with exception: The remote name could not be resolved: 'configmgrbits.azureedge.net'
WARNING: Retry in the next polling cycle
```

This failure happens because the service connection point can't communicate with the required internet endpoint, `configmgrbits.azureedge.net`. Confirm that the site system that hosts the service connection point role can communicate with this internet endpoint. It was already required, but its use is expanded in version 2107. The site system can't download version 2107 or later unless your network allows traffic to this URL.

For more information, see [internet access requirements](../../../plan-design/network/internet-endpoints.md#service-connection-point) for the service connection point.

### Management point installation or update fails because of later Visual C++ version

<!-- 10518360 -->

_Applies to: version 2107 early update ring_

If the site system server has a version of the Visual C++ redistributable later than 14.28.29914, Configuration Manager setup will fail to install or update the management point role.

To work around this issue, temporarily uninstall the later version of Visual C++ redistributable. When you install Configuration Manager version 2107, it will install version 14.28.29914.

## OS deployment

### Image servicing with Windows Server 2022

<!-- 11843519, MEMDocs#2108 -->

_Applies to: version 2107_

If you try to [apply software updates to an image](../../../../osd/get-started/manage-operating-system-images.md#apply-software-updates-to-an-image) for Windows Server 2022, no updates display as available to install.

This issue is caused by a change to the Windows update category for Server 2022.

To resolve this issue, install the [update rollup](../../../../hotfix/2107/11121541.md) for Configuration Manager version 2107.

### Task sequence and application policy issue

<!-- 10506770 -->

_Applies to: version 2107 early update ring installed between August 2, 2021 and August 6, 2021_

If you have all of the following conditions:

- Task sequence _A_
  - Includes the **Install Application** step with app _X_
  - Deployed and made available to either type that includes **Configuration Manager clients**

- Task sequence _B_
  - Includes the **Install Application** step with the same app _X_
  - Deployed and made available to either **Only media and PXE** option

After you update to version 2107, if you make any change to app _X_, then task sequence _A_ will fail to run on clients that receive the deployment policy after the site update. The Configuration Manager client can't get all of the policies for the task sequence and referenced applications. For clients that already had the deployment policy for task sequence _A_ before the site update, the task sequence will run, but clients won't have the revised application policy.

You can run the following SQL script on a primary site database to determine if your site has this issue:

```sql
select COUNT(*) from Policy where PolicyID like '%/VI%' 
  AND ((ISNULL(PolicyFlags, 0) & 4096 = 4096) 
  OR (ISNULL(PolicyFlags, 0) & 2048 = 2048))
```

If this query returns `0`, there's currently no issue. If the query returns a non-zero value, the issue only exists given the above conditions.

> [!NOTE]
> If there are many media and PXE task sequences that reference an application that you revise, the site will take longer to update these task sequence policies. During this time, some media and PXE task sequence deployments may fail. There's no workaround for this timing issue.

#### Workaround for task sequence and application policy issue in version 2107 early update ring

This issue is fixed in the build of version 2107 that's now generally available for all customers. If you previously opted in to the early update ring, install the [Update for Microsoft Endpoint Configuration Manager version 2107, early update ring](../../../../hotfix/2107/10503003.md).

For OS deployment task sequences to existing clients not with PXE, you may see entries similar to the following strings in the ExecMgr.log on the client:

```log
cannot load compressed XML policy
Failed to load policy from XML ''
Could not find the policy in WMI for Application ScopeId_88A86770-F44E-47C8-BF8D-3C1B8A5DF3AA/Application_b711f24c-f766-41e0-9c41-02313b2c8be3
Unable to find application policy for [advertisement: PR220005 appid: ScopeId_88A86770-F44E-47C8-BF8D-3C1B8A5DF3AA/Application_b711f24c-f766-41e0-9c41-02313b2c8be3]
Fail to initialize TS member info, error 0x87d02004
```

For this issue, after you install the update for version 2107 early update ring, run the following SQL query on the primary site to which the client is assigned:

```sql
select distinct ci.CI_ID from vSMS_ConfigurationItems ci
join CI_ConfigurationItemRelations_Flat cir on cir.ToCI_ID = ci.CI_ID and cir.RelationType = 11
join vSMS_ConfigurationItems intent_ci on intent_ci.CI_ID = cir.FromCI_ID
join policy p on p.PolicyID = intent_ci.ModelName+'/VI' and ((p.PolicyFlags & 0x800) > 0 or (p.PolicyFlags & 0x1000) > 0)
where ci.CIType_ID = 10 and ci.IsLatest = 1 and ci.IsTombstoned = 0
```

For each **CI_ID** that this query returns, create a 0-KB file named `<ci_id>.cit`. For example, `16777225.cit`. Move the file to the **policypv.box** directory on the primary site server. For example, `\\cmpri01.contoso.com\SMS_PR1\inboxes\policypv.box\`.

## Software updates

### Security roles are missing for phased deployments

<!--3479337, SCCMDocs-pr issue 3095-->

The **OS Deployment Manager** built-in security role has permissions to [phased deployments](../../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md). The following roles are missing these permissions:  

- **Application Administrator**  
- **Application Deployment Manager**  
- **Software Update Manager**  

The **App Author** role may appear to have some permissions to phased deployments, but can't create deployments.

A user with one these roles can start the Create Phased Deployment wizard, and can see phased deployments for an application or software update. They can't complete the wizard, or make any changes to an existing deployment.

To work around this issue, create a custom security role. Copy an existing security role, and add the following permissions on the **Phased Deployment** object class:

- Create  
- Delete  
- Modify  
- Read  

For more information, see [Create custom security roles](../configure/configure-role-based-administration.md#create-custom-security-roles)

## Configuration Manager console

### Intune RBAC for Tenant Attached devices is coming soon
<!--13058986-->
_Applies to: version 2207_

You will now see a checkbox for RBAC setting in the cloud attach configuration wizard on the console.
By default, SCCM RBAC will be enforced along with Intune RBAC when you are uploading your Configuration Manager devices to the cloud service. Hence, the checkbox will be checked by default. If you want to enforce only Intune RBAC, you can uncheck the box. The Intune RBAC enforcement will be applicable soon. For more information see, [Enable Microsoft Endpoint Manager tenant attach](../../../../../configmgr/tenant-attach/device-sync-actions.md)

### Unable to open console because extension installation loops
<!--12868458-->
_Applies to: version 2111_

In certain circumstances, you'll be unable to open the console due to an extension installation loop. This issue occurs when two or more versions of a single extension were marked as [required for installation](../../manage/admin-console-extensions.md#require-installation-of-a-console-extension). This issue occurs for extensions imported through the wizard, from a PowerShell script, or through Community hub. If you use the **Make optional** setting before importing a new version of the extension, this issue doesn't occur.

When you encounter this issue, it initially appears as a normal console extension installation. After the extension finishes installing, you select **Close** to restart the Configuration Manager console. When the console restarts, you're prompted to install the console extension again. The extension installation will continue to loop and the Configuration Manager console doesn't fully open.

To both prevent and workaround this issue, run the below SQL script on your CAS database and all of your primary site databases:

```sql
ALTER VIEW vSMS_ConsoleExtensionMetadata
AS
    WITH m AS(
       SELECT *,
           RN = ROW_NUMBER()OVER(PARTITION BY ID ORDER BY Version DESC)
       FROM ConsoleExtensionMetadata
    ) 
    SELECT 
        m.ID, 
        m.Name, 
        m.Description, 
        m.Author, 
        m.Version, 
        m.IsEnabled, 
        m.IsApproved, 
        m.CreatedTime, 
        m.CreatedBy, 
        m.UpdateTime, 
        m.IsTombstoned, 
        m.IsRequired, 
        m.IsSigned, 
        m.IsUnsignedAllowed, 
        CASE m.IsRequired 
            WHEN 0 THEN ''  
            ELSE  
            ( 
                SELECT top(1) author FROM ConsoleExtensionRevisionHistory h 
                WHERE m.ID=h.ExtensionId AND m.Version=h.Version AND h.Changes & 1=1 
                ORDER BY h.RevisionTime DESC 
            ) 
        END AS RequiredBy, 
        m.IsSetupDefined 
    FROM m
    WHERE RN = 1
GO
```

### Supported platform conditions don't update for some objects

<!-- 10247604,10425120 -->
_Applies to version 2107_

You can select supported platforms on many objects such as applications, task sequences, and configuration items. Starting in version 2107, these lists are updated to include categories for Windows 11. After you update the primary site to version 2107, there are different behaviors depending upon the type of object:

- Within 24 hours of updating the site, the supported platforms for the following objects will automatically update:
  - Packages and programs
  - Task sequences
  - Compliance settings, for example, endpoint protection

  In that initial 24-hour period, existing policies with Windows 10 conditions also apply to Windows 11. After the site updates the objects, they only apply to Windows 10. You can select Windows 11 as a supported platform at any time.

- You need to manually review and update the supported platforms for the following objects:
  - Applications
  - Configuration items
  - Objects referenced in a task sequence

  For these objects, existing policies with Windows 10 conditions also apply to Windows 11. You need to manually revise the supported platform list.

### Configuration Manager console settings aren't saved
<!--5452246-->
_Applies to version 2107_

When you install the 2107 version of the Configuration Manager console, settings such as column changes, window size, and searches aren't saved. When you first open the upgraded console, it will appear as if it was never previously installed on the device. Any console settings made after installing the 2107 version of the Configuration Manager console will persist when you reopen it.

### Console extensions
<!--3555909-->
*Applies to version 2103* 

There's a new hierarchy setting that allows for only using the new style of [console extensions](../../manage/admin-console-extensions.md). If this setting is enabled, you can't use any old style extensions that aren't approved through the **Console Extensions** node. The setting, **Only allow console extensions that are approved for the hierarchy**, is `enabled` by default if you installed from the [2103 baseline build](../../manage/updates.md#bkmk_Baselines). If you update the site from version 2010 or earlier, it's `disabled` by default.

If the setting was enabled in error, disabling the setting allows the old style extensions to be used again.

<!-- ## Cloud services -->

<!-- ## Role based administration -->

<!-- ## Application management -->

## CMPivot

### Favorite queries lose line breaks or are truncated

<!-- 10517223 -->

_Applies to: version 2107 early update ring_

After you update the site to version 2107, there are two issues with CMPivot queries that you saved as a favorite:

- When you edit the query, you may see unexpected characters like `\r` or `\t`.

- The query after the last comma (`,`) is removed.

This issue is fixed in the build of version 2107 that's now generally available for all customers. If you previously opted in to the early update ring, install the [Update for Microsoft Endpoint Configuration Manager version 2107, early update ring](../../../../hotfix/2107/10503003.md).
