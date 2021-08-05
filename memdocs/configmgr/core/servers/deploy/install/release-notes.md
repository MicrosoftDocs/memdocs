---
title: Release notes
titleSuffix: Configuration Manager
description: Learn about urgent issues that aren't yet fixed in the product or covered in a Microsoft Support knowledge base article.
ms.date: 08/04/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: troubleshooting
author: mestew
ms.author: mstewart
manager: dougeby
---

# Release notes for Configuration Manager

*Applies to: Configuration Manager (current branch)*

With Configuration Manager, product release notes are limited to urgent issues. These issues aren't yet fixed in the product, or detailed in a Microsoft Support knowledge base article.

Feature-specific documentation includes information about known issues that affect core scenarios.

This article contains release notes for the current branch of Configuration Manager. For information on the technical preview branch, see [Technical Preview](../../../get-started/technical-preview.md).

For information about the new features introduced with different versions, see the following articles:

- [What's new in version 2107](../../../plan-design/changes/whats-new-in-version-2107.md)
- [What's new in version 2103](../../../plan-design/changes/whats-new-in-version-2103.md)
- [What's new in version 2010](../../../plan-design/changes/whats-new-in-version-2010.md)
- [What's new in version 2006](../../../plan-design/changes/whats-new-in-version-2006.md)

For information about the new features in Desktop Analytics, see [What's new in Desktop Analytics](../../../../desktop-analytics/whats-new.md).

> [!TIP]
> To get notified when this page is updated, copy and paste the following URL into your RSS feed reader:
> `https://docs.microsoft.com/api/search/rss?search=%22release+notes+-+Configuration+Manager%22&locale=en-us`

## Client management

### Client notification actions apply to entire collection

<!-- 9021554 -->

_Applies to version 2010_

When you use a [client notification](../../../clients/manage/client-notification.md) action on a device in a collection, the action applies to all devices in the collection.

For example:

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace, and select the **Device Collections** node.

1. Select a collection, and then choose the **Show Members** action.

1. Select a device in the collection. In the ribbon on the **Home** tab, select **Client Notification**, and choose an action such as **Restart**.

    Because of this issue, this action applies to all members of the collection, not just the selected client.

    > [!NOTE]
    > This issue doesn't apply to the **Start CMPivot** or **Run Script** options.

To work around this issue, install the following hotfix: [Client notifications sent to all collection members in Configuration Manager current branch, version 2010](https://support.microsoft.com/help/4594177).

You can also use the **Devices** node. Find the device in the list and start the action from there.

> [!NOTE]
> This issue also applies to the [Invoke-CMClientAction](/powershell/module/configurationmanager/invoke-cmclientaction) PowerShell cmdlet and other SDK methods, if you don't include a collection object or ID.

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

### Management point installation or update fails due to later Visual C++ version

<!-- 10518360 -->

_Applies to: version 2107 early update ring_

If the site system server has a version of the Visual C++ redistributable later than 14.28.29914, Configuration Manager setup will fail to install or update the management point role.

To work around this issue, temporarily uninstall the later version of Visual C++ redistributable. When you install Configuration Manager version 2107, it will install version 14.28.29914.

## OS deployment

### Task sequence and application policy issue

<!-- 10506770 -->

_Applies to: version 2107 early update ring_

If you have all of the following conditions:

- Task sequence _A_
  - Includes the **Install Application** step with app _X_
  - Deployed and made available to either type that includes **Configuration Manager clients**

- Task sequence _B_
  - Includes the **Install Application** step with the same app _X_
  - Deployed and made available to either **Only media and PXE** option

After you update to version 2107, if you make any change to app _X_, then task sequence _A_ will fail to run on clients that receive the deployment policy after the site update. The Configuration Manager client won't be able to get all of the policies for the task sequence and referenced applications. For clients that already had the deployment policy for task sequence _A_ before the site update, the task sequence will run, but clients won't have the revised application policy.

You can use the following SQL script to determine if your site has this issue:

```sql
select COUNT(*) from Policy where PolicyID like '%/VI%' 
  AND ((ISNULL(PolicyFlags, 0) & 4096 = 4096) 
  OR (ISNULL(PolicyFlags, 0) & 2048 = 2048))
```

If this query returns `0`, there's currently no issue. If the query returns a non-zero value, the issue only exists given the above conditions.

#### Workaround for task sequence and application policy issue in version 2107 early update ring

If you updated the site to version 2107, have already revised an app, and are in this state, then use the following workaround:

1. Edit task sequence _A_.
1. Remove app _X_ from every **Install Application** step in which it's referenced.
1. Save the task sequence.
1. Add app _X_ back to the task sequence as previously included.
1. Save the task sequence.

This process causes the site to update the policy with the correct flag.

Repeat this process for every revised app. You don't need to do it for every task sequence where the app is referenced, only once for each revised app.

Even after doing this process, if you revise an app that's referenced in the task sequence, repeat this process to correct the issue.

> [!NOTE]
> This workaround addresses the issue for clients that have not yet received the deployment policy. Clients that already have the deployment policy won't have the revised application policy.

### Task sequences can't run over CMG

*Applies to: version 2002*

There are two instances in which task sequences can't run on a device that communicates via a cloud management gateway (CMG):

- You configure the site for Enhanced HTTP and the management point is HTTP.<!-- 6358851 -->

    To work around this issue, update to version 2006. You can also configure the management point for HTTPS.

- You installed and registered the client with a bulk registration token for authentication.<!-- 6377921 -->

    To work around this issue, update to version 2006. You can also use one of the following authentication methods:

  - Pre-register the device on the internal network
  - Configure the device with a client authentication certificate
  - Join the device to Azure AD

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

## Desktop Analytics

### <a name="dawin7-diagtrack"></a> An extended security update for Windows 7 causes them to show as **Unable to enroll**

<!-- 7283186 -->
_Applies to: versions 2002 and earlier_

The April 2020 extended security update (ESU) for Windows 7 changed the minimum required version of the diagtrack.dll from 10586 to 10240. This change causes Windows 7 devices to show as **Unable to enroll** in the Desktop Analytics **Connection Health** dashboard. When you drill down to the device view for this status, the **DiagTrack service configuration** property displays the following state: `Connected User Experience and Telemetry (diagtrack.dll) component is outdated. Check requirements.`

No workaround is required for this issue. Don't uninstall the April ESU. If otherwise properly configured, the Windows 7 devices still report diagnostic data to the Desktop Analytics service, and still show in the portal.

## Configuration Manager console

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

There's a new hierarchy setting that allows for only using the new style of [console extensions](../../manage/admin-console-extensions.md). If this setting is enabled, you can't use any old style extensions that aren't approved through the **Console Extensions** node. The setting, **Only allow console extensions that are approved for the hierarchy**, is `enabled` by default if you installed from the [2103 baseline image](../../manage/updates.md#bkmk_Baselines). If you update the site from version 2010 or earlier, it is `disabled` by default.

If the setting was enabled in error, disabling the setting allows the old style extensions to be used again.

<!-- ## Cloud services -->

<!-- ## Role based administration -->

<!-- ## Application management -->

## CMPivot

### Favorite queries lose line breaks or are truncated

<!-- 10517223 -->

_Applies to: version 2107 early update ring_

After you update the site to version 2107, there are two issues with CMPivot queries that you saved as a favorite:

- When you edit the query, you may see unexpected characters like `\r` or `\t`. To work around this issue, remove the `\r` or `\t` characters, and then save the query.

- The query after the last comma (`,`) is removed. There's currently no workaround for this issue. Recreate the query.
