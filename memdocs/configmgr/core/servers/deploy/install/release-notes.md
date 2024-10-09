---
title: Release notes
titleSuffix: Configuration Manager
description: Learn about urgent issues that aren't yet fixed in the product or covered in a Microsoft Support knowledge base article.
ms.date: 10/04/2024
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: conceptual
author: PalikaSingh
ms.author: palsi
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---


# Release notes for Configuration Manager

*Applies to: Configuration Manager (current branch)*

With Configuration Manager, product release notes are limited to urgent issues. These issues aren't yet fixed in the product, or detailed in a [troubleshooting article](/troubleshoot/mem/configmgr/).

Feature-specific documentation includes information about known issues that affect core scenarios.

This article contains release notes for the current branch of Configuration Manager. For information on the technical preview branch, see [Technical Preview](../../../get-started/technical-preview.md).

For information about the new features introduced with different versions, see the following articles:

- [What's new in version 2403](../../../plan-design/changes/whats-new-in-version-2403.md)
- [What's new in version 2309](../../../plan-design/changes/whats-new-in-version-2309.md)
- [What's new in version 2303](../../../plan-design/changes/whats-new-in-version-2303.md)
- [What's new in version 2211](../../../plan-design/changes/whats-new-in-version-2211.md)


> [!TIP]
> You can use RSS to be notified when this page is updated. For more information, see [How to use the docs](../../../../../use-docs.md#notifications).

<!-- > To get notified when this page is updated, copy and paste the following URL into your RSS feed reader:
> `https://learn.microsoft.com/api/search/rss?search=%22release+notes+-+Configuration+Manager%22&locale=en-us` -->

## Client management

### Clients are not able download content from CMG when branch cache is enabled
_Applies to: version 2403_

After enabling Branch Cache on primary sites, clients are unable to download apps and packages from the CMG. They typically manage to download only 20-30% of the content before the process gets stuck. In some cases, after downloading certain blocks of packages from the CMG, clients look for Branch Cache to retrieve the remaining content. However, none of the clients are able to download the complete content from the CMG, which prevents others from using Branch Cache to access it. The **CTM.log** on the client includes entries similar to the following:

```log
(CTM.log - CTMJob({63B4C4CE-2DC4-4062-93C7-E5019B3B6CE1}): CCTMJob::Start - State=DownloadingContentFromPeers)
CTM.log _- CTMJob({D21758B0-D895-474E-9695-1023A25A1770}): CCTMJob::_PerformDownloadWithOutBranchCache - Download failure using branchcache, fallback to regular download
```
To work around this issue, disable branch cache.

> [!NOTE]
>Clients are able to download Content from On-Premise DP when Branch Cache is Enabled.

## Endpoint Protection
### Security configurations removed from Intune
<!-- 27951696 -->
_Applies to: version 2309 with KB25858444 and later_

Microsoft Defender security configurations are no longer managed with Microsoft Intune after updating to Configuration Manager version 2403, or installing the [Update Rollup for 2309](../../../../hotfix/2309/25858444.md). 

The symptom is seen as a drop in the Microsoft Security Score values when viewed in Intune. This issue happens because security policy configuration data is incorrectly removed from clients after Configuration Manager clients are upgraded. 

An updated version of the Microsoft Security Client Policy Configuration Tool, ConfigSecurityPolicy.exe, is available to resolve the Endpoint Protection policy issue described in this note.

The updated tool, version 4.18.24040.4, is distributed with the April 2024 monthly Microsoft Defender platform update. At the time of this writing, the platform update is in the process of global distribution, and should be broadly available in all regions by May 17, 2024.   
Once the platform update is installed on affected clients, Endpoint Protection policies are reapplied from Intune within 8 hours. The "Manage Endpoint Protection client on client computers" setting in Configuration Manager can be changed back to "Yes" as required.
#### Additional references

- [Monthly platform and engine versions](/defender-endpoint/microsoft-defender-antivirus-updates#monthly-platform-and-engine-versions)
- [Microsoft Defender update for Windows operating system installation images](https://support.microsoft.com/topic/microsoft-defender-update-for-windows-operating-system-installation-images-1c89630b-61ff-00a1-04e2-2d1f3865450d).
- [Sync devices to get the latest policies and actions with Intune](/mem/intune/remote-actions/device-sync#sync-a-device)

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

## OS deployment

### PXE Responder is not installed correctly after upgrading to 2403 in untrusted domain
_Applies to: version 2403_

After upgrading to 2403, site servers serving as a PXE responder might see failures due to incorrect configuration of the registry keys. We can observe the below failures in **distmgr.log** indicating that the registry keys were not configured correctly.
 
```log
Failed to get OS platform for server DP2.CONTOSO2.COM.Either a permissions issue or the server is not supported OS SMS_DISTRIBUTION_MANAGER
CDistributionManager::SetDpRegistry failed; 0x80070005 SMS_DISTRIBUTION_MANAGER
``` 
This happened due to currently unexplained failures in platform architecture identification that were introduced during the addition of support for arm64 machines to serve as remote distribution points.

## Software updates

### Reset default value of superseding age in months for software updates
_Applies to: version 2303_

Removing SUP role in Admin Console does not reset the superseding age property in WMI. As a result, while reconfiguring the role, the previously configured value is shown in the configuration window. This property needs to be reset to default value on role removal. For more information, see [supersedence rules for installing a software update point.](../../../../sum/get-started/install-a-software-update-point.md)

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

### Intune RBAC for tenant attached devices
<!--13058986-->
*Applies to: version 2207*

***[Updated]***: There is a checkbox for a role-based access control (RBAC) setting in the [cloud attach configuration wizard](../../../../cloud-attach/enable.md) in the console. By default, Configuration Manager RBAC is enforced along with Intune RBAC when you're uploading your Configuration Manager devices to the cloud service. This checkbox is selected by default.

You can now configure Intune role-based access control (RBAC) when interacting with [tenant attached devices](../../../../tenant-attach/client-details.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json) from the Microsoft Intune admin center. For more information, see [Intune role-based access control for tenant-attached clients](../../../../cloud-attach/use-intune-rbac.md).

### Unable to open console because extension installation loops
<!--12868458-->
_Applies to: version 2111_

In certain circumstances, you'll be unable to open the console due to an extension installation loop. This issue occurs when two or more versions of a single extension were marked as [required for installation](../../manage/admin-console-extensions.md#require-installation-of-a-console-extension). This issue occurs for extensions imported through the wizard, from a PowerShell script, or through Community hub. If you use the **Make optional** setting before importing a new version of the extension, this issue doesn't occur.

When you encounter this issue, it initially appears as a normal console extension installation. After the extension finishes installing, you select **Close** to restart the Configuration Manager console. When the console restarts, you're prompted to install the console extension again. The extension installation will continue to loop and the Configuration Manager console doesn't fully open.

To both prevent and work around this issue, run the below SQL script on your CAS database and all of your primary site databases:

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
## Boundaries and Boundary groups

### Clients not belonging to any boundary group may fail to download due to SQL issue 
<!--22760249-->
*Applies to: version 2303, 2309 RTM*

 Consider ConfigMgr hierarchy with a remote MP and CMG and you deploy an app to a device collection. The Clients cannot download app, and reflect the below SQL permissions issue in **MP_Location.log**.

 ```log
    The SELECT permission was denied on the object 'vSMS_DefaultBoundaryGroup', database 'CM_xxx', schema 'dbo'.
 ```
 To work around the issue run the below SQL script on the SQL database on the primary sites where the MP reports.

```sql
    GRANT SELECT ON vSMS_DefaultBoundaryGroup To smsdbrole_MP
```
<!-- ## Cloud services -->

<!-- ## Role based administration -->

<!-- ## Application management -->

<!-- ## CMPivot -->
