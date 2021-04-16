---
title: Release notes
titleSuffix: Configuration Manager
description: Learn about urgent issues that aren't yet fixed in the product or covered in a Microsoft Support knowledge base article.
ms.date: 04/05/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: troubleshooting
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
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

- [What's new in version 2103](../../../plan-design/changes/whats-new-in-version-2103.md)
- [What's new in version 2010](../../../plan-design/changes/whats-new-in-version-2010.md)
- [What's new in version 2006](../../../plan-design/changes/whats-new-in-version-2006.md)
- [What's new in version 2002](../../../plan-design/changes/whats-new-in-version-2002.md)

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

    Due to this issue, this action applies to all members of the collection, not just the selected client.

    > [!NOTE]
    > This issue doesn't apply to the **Start CMPivot** or **Run Script** options.

To work around this issue, install the following hotfix: [Client notifications sent to all collection members in Configuration Manager current branch, version 2010](https://support.microsoft.com/help/4594177).

Alternatively, use the **Devices** node. Find the device in the list and start the action from there.

> [!NOTE]
> This issue also applies to the [Invoke-CMClientAction](/powershell/module/configurationmanager/invoke-cmclientaction) PowerShell cmdlet and other SDK methods, if you don't include a collection object or ID.

## Set up and upgrade

### Client automatic upgrade happens immediately for all clients

<!-- 6040412 -->

*Applies to version 1910*

If your site uses [automatic client upgrade](../../../clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade), when you update the site to version 1910, all clients immediately upgrade after the site updates successfully. The only randomization is when clients receive the policy, which by default is every hour. For a large site with many clients, this behavior can consume a significant amount of network traffic and stress distribution points.

For more information on affected versions, see [Client update for Configuration Manager current branch, version 1910](https://support.microsoft.com/help/4538166).

### Site server in passive mode doesn't update configuration.mof

<!-- 5787848 -->

*Applies to version 1910*

If your site includes a [site server in passive mode](../configure/site-server-high-availability.md), you may lose inventory customizations when you update the site. The site doesn't currently synchronize the configuration.mof when you fail over the site servers.

To work around this issue, manually back up and restore the site's configuration.mof.

## Role based administration

### Security scopes for certain folders don't replicate from CAS to primary sites
<!--6306759-->
*Applies to version 1910*

After upgrade to version 1910, [security scopes for folders](../configure/configure-role-based-administration.md#bkmk_config-folder) in user collections and device collections don't get replicated from the CAS to primary sites.

## Application management

### Unable to get certificate for PowerShell error when deploying Microsoft Edge, version 77 and later
<!--5769384-->
*Applies to: version 1910*

If you are running the Configuration Manager console on an OS where the language is Swedish, Hungarian, or Japanese, you'll receive the following error when deploying Microsoft Edge, version 77 and later:

`Unable to get certificate for Powershell`

This error occurs because a `scripts` folder doesn't exist under the `AdminConsole\bin` directory for Swedish, Hungarian, or Japanese languages. The scripts folder is localized in these OS languages.

To work around this issue, create a folder called `scripts` in the `AdminConsole\bin` directory. Copy the files from your localized folder to the newly created `scripts` folder. Deploy Microsoft Edge, version 77 and later once the files have been copied.

## OS deployment

### Task sequences can't run over CMG

*Applies to: version 2002*

There are two instances in which task sequences can't run on a device that communicates via a cloud management gateway (CMG):

- You configure the site for Enhanced HTTP and the management point is HTTP.<!-- 6358851 -->

    To work around this issue, update to version 2006. Alternatively, configure the management point for HTTPS.

- You installed and registered the client with a bulk registration token for authentication.<!-- 6377921 -->

    To work around this issue, update to version 2006. Alternatively, use one of the following authentication methods:

  - Pre-register the device on the internal network
  - Configure the device with a client authentication certificate
  - Join the device to Azure AD

## Software updates

### Security roles are missing for phased deployments

<!--3479337, SCCMDocs-pr issue 3095-->
*Applies to: versions 1810 and later*

The **OS Deployment Manager** built-in security role has permissions to [phased deployments](../../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md). The following roles are missing these permissions:  

- **Application Administrator**  
- **Application Deployment Manager**  
- **Software Update Manager**  

The **App Author** role may appear to have some permissions to phased deployments, but shouldn't be able to create deployments.

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

There is a new hierarchy setting that allows for only using the new style of [console extensions](../../manage/admin-console-extensions.md). If this setting is enabled, your old style extensions that aren't approved through the **Console Extensions** node will no longer be able to be used. The setting, **Only allow console extensions that are approved for the hierarchy**, is `enabled` by default if you installed from the [2103 baseline image](../../manage/updates.md#bkmk_Baselines). It will remain `disabled` by default, if you upgraded from a version prior to 2103.

If the setting was enabled in error, disabling the setting allows the old style extensions to be used again.
## Cloud services

### Azure service for US Government cloud shows as public cloud

<!-- 6036748 -->

*Applies to version 1910*

If you create a connection to an Azure service, and set the **Azure environment** to the government cloud, the properties of the connection show the environment as the Azure public cloud. This issue is only a display problem in the console, the service is in the government cloud. To confirm the configuration, run the following SQL query on the site database:

```SQL
Select Environment, Name, TenantID From AAD_Tenant_Ex
```

For the government cloud, the result of this query is `2` for the specific tenant.
