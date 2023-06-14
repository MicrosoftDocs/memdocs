---
title: Release notes
titleSuffix: Configuration Manager
description: Learn about urgent issues that aren't yet fixed in the product or covered in a Microsoft Support knowledge base article.
ms.date: 03/28/2023
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: troubleshooting
author: banreet
ms.author: banreetkaur
manager: sunitashaw
ms.localizationpriority: medium
ms.collection: tier3

---

# Release notes for Configuration Manager

*Applies to: Configuration Manager (current branch)*

With Configuration Manager, product release notes are limited to urgent issues. These issues aren't yet fixed in the product, or detailed in a [troubleshooting article](/troubleshoot/mem/configmgr/).

Feature-specific documentation includes information about known issues that affect core scenarios.

This article contains release notes for the current branch of Configuration Manager. For information on the technical preview branch, see [Technical Preview](../../../get-started/technical-preview.md).

For information about the new features introduced with different versions, see the following articles:

- [What's new in version 2303](../../../plan-design/changes/whats-new-in-version-2303.md)
- [What's new in version 2211](../../../plan-design/changes/whats-new-in-version-2211.md)
- [What's new in version 2207](../../../plan-design/changes/whats-new-in-version-2207.md)
- [What's new in version 2203](../../../plan-design/changes/whats-new-in-version-2203.md)
- [What's new in version 2111](../../../plan-design/changes/whats-new-in-version-2111.md)


> [!TIP]
> You can use RSS to be notified when this page is updated. For more information, see [How to use the docs](../../../../../use-docs.md#notifications).
<!-- > To get notified when this page is updated, copy and paste the following URL into your RSS feed reader:
> `https://learn.microsoft.com/api/search/rss?search=%22release+notes+-+Configuration+Manager%22&locale=en-us` -->

<!-- ## Client management -->

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

<!-- ## OS deployment -->

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

<!-- ## Cloud services -->

<!-- ## Role based administration -->

<!-- ## Application management -->

<!-- ## CMPivot -->
