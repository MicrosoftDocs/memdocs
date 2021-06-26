---
title: Release notes
titleSuffix: Configuration Manager
description: Learn about urgent issues that aren't yet fixed in the product or covered in a Microsoft Support knowledge base article.
ms.date: 07/16/2021
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

This failure happens because the service connection point can't communicate with the required internet endpoint, `configmgrbits.azureedge.net`. Confirm that the site system that hosts the service connection point role can communicate with this internet endpoint. It was already required, but its use is expanded in version 2107. You can't update to version 2107 unless your network allows traffic to this URL.

For more information, see [internet access requirements](../../../plan-design/network/internet-endpoints.md#service-connection-point) for the service connection point.

## OS deployment

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

### Console extensions
<!--3555909-->
*Applies to version 2103* 

There's a new hierarchy setting that allows for only using the new style of [console extensions](../../manage/admin-console-extensions.md). If this setting is enabled, you can't use any old style extensions that aren't approved through the **Console Extensions** node. The setting, **Only allow console extensions that are approved for the hierarchy**, is `enabled` by default if you installed from the [2103 baseline image](../../manage/updates.md#bkmk_Baselines). If you update the site from version 2010 or earlier, it is `disabled` by default.

If the setting was enabled in error, disabling the setting allows the old style extensions to be used again.

<!-- ## Cloud services -->

<!-- ## Role based administration -->

<!-- ## Application management -->
