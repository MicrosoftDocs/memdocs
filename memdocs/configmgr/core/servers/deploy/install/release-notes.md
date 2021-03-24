---
title: Release notes
titleSuffix: Configuration Manager
description: Learn about urgent issues that aren't yet fixed in the product or covered in a Microsoft Support knowledge base article.
ms.date: 01/12/2021
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

- [What's new in version 2010](../../../plan-design/changes/whats-new-in-version-2010.md)
- [What's new in version 2006](../../../plan-design/changes/whats-new-in-version-2006.md)
- [What's new in version 2002](../../../plan-design/changes/whats-new-in-version-2002.md)
- [What's new in version 1910](../../../plan-design/changes/whats-new-in-version-1910.md)

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

### Site server in passive mode fails to update to version 2010

<!-- 8896585 -->

_Applies to version 2010 early update ring_

If you have a [highly available site server](../configure/site-server-high-availability.md), when you update to version 2010, the site server in passive mode fails to update. This issue is due to a change in the Microsoft Monitoring Agent (MMA) for Microsoft Defender Advanced Threat Protection. The required MMA files aren't copied to all necessary locations.

To work around this issue:

1. Go to the Configuration Manager installation directory on the site server. In the `.\CMUStaging\D5054056-F41C-4E61-90A7-4F135B76F806\Redist` folder, copy both **MMASetup-amd64.exe** and **MMASetup-i386.exe** to the `.\cd.latest\redist` folder.

1. If you have a management point role installed on another server, copy the following files to the following folders in the Configuration Manager installation folder on the site system server:

    1. Copy **MMASetup-amd64.exe** to the `.\sms\client\x64` folder.
    1. Copy **MMASetup-i386.exe** to the `.\sms\client\i386` folder.

1. Delete the file `inboxes\failovermgr.box\siteserver.pkg` on the site server.

1. Retry the update to version 2010.

> [!NOTE]
> This issue can also occur when you add a new site server in passive mode after updating to version 2010.

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

### Setup prerequisite warning on domain functional level on Server 2019

<!-- 4904376 -->

*Applies to version 1906*

When installing the update for version 1906 in an environment with domain controllers running Windows Server 2019, the prerequisite check for domain functional level returns the following warning:

`[Completed with warning]:Verify that the Active Directory domain functional level is Windows Server 2003 or later`

To work around this issue, ignore the warning.

### Azure AD user discovery and collection group sync don't work after site expansion

<!-- 4797313 -->
*Applies to version 1906*

After you configure either of the following features:

- Azure Active Directory user group discovery
- Synchronize collection membership results to Azure Active Directory groups

If you then expand a standalone primary site to a hierarchy with a central administration site, you'll see the following error in SMS_AZUREAD_DISCOVERY_AGENT.log:

`Could not obtain application secret for tenant xxxxx. If this is after a site expansion, please run "Renew Secret Key" from admin console.`

To work around this issue, renew the key associated with the app registration in Azure AD. For more information, see [Renew secret key](../configure/azure-services-wizard.md#bkmk_renew).

## Role based administration

### Only Full Administrator can delete collections
<!--8864728-->
*Applies to version 2010 early update ring*

When trying to delete a collection, there is a query to check for Automatic Deployment Rules (ADR) that are referencing the collection. If you don't have permissions on ADRs, you will be unable to perform the deletion.

To work around this issue, if you need to delete a collection, ensure you have full administrator permissions to do it. You can also grant **Read** permission to the **Software Update** object to your accounts, since that grants access to ADRs but note those accounts would be able to delete collections too.

### Security scopes for certain folders don't replicate from CAS to primary sites
<!--6306759-->
*Applies to version 1910*

After upgrade to version 1910, [security scopes for folders](../configure/configure-role-based-administration.md#bkmk_config-folder) in user collections and device collections don't get replicated from the CAS to primary sites.

## Application management

### Unable to get certificate for PowerShell error when deploying Microsoft Edge, version 77 and later
<!--5769384-->
*Applies to: Configuration Manager version 1910*

If you are running the Configuration Manager console on an OS where the language is Swedish, Hungarian, or Japanese, you'll receive the following error when deploying Microsoft Edge, version 77 and later:

`Unable to get certificate for Powershell`

This error occurs because a `scripts` folder doesn't exist under the `AdminConsole\bin` directory for Swedish, Hungarian, or Japanese languages. The scripts folder is localized in these OS languages.

To work around this issue, create a folder called `scripts` in the `AdminConsole\bin` directory. Copy the files from your localized folder to the newly created `scripts` folder. Deploy Microsoft Edge, version 77 and later once the files have been copied.

## OS deployment

### Client policy error when you deploy a task sequence

<!-- 7970134 -->

*Applies to: Configuration Manager version 2006 early update ring*

When you deploy a task sequence to a client, a required task sequence doesn’t install at the deadline, and an available task sequence doesn’t appear in Software Center. You see status message 10803 with a description similar to the following error message:

*The client failed to download policy. The data transfer service returned "BITS error: 'The server's response was not valid. The server was not following the defined protocol. (-2145386469).*

This issue occurs when you configure the management point for HTTPS, and the device uses Configuration Manager client version 1906 or earlier.

To work around this issue, update the Configuration Manager client on the device to version 1910 or later.

### Task sequences can't run over CMG

*Applies to: Configuration Manager version 2002*

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
*Applies to: Configuration Manager versions 1810 and later*

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

For more information, see [Create custom security roles](../configure/configure-role-based-administration.md#BKMK_CreateSecRole)

## Desktop Analytics

### <a name="dawin7-diagtrack"></a> An extended security update for Windows 7 causes them to show as **Unable to enroll**

<!-- 7283186 -->
_Applies to: Configuration Manager versions 2002 and earlier_

The April 2020 extended security update (ESU) for Windows 7 changed the minimum required version of the diagtrack.dll from 10586 to 10240. This change causes Windows 7 devices to show as **Unable to enroll** in the Desktop Analytics **Connection Health** dashboard. When you drill down to the device view for this status, the **DiagTrack service configuration** property displays the following state: `Connected User Experience and Telemetry (diagtrack.dll) component is outdated. Check requirements.`

No workaround is required for this issue. Don't uninstall the April ESU. If otherwise properly configured, the Windows 7 devices still report diagnostic data to the Desktop Analytics service, and still show in the portal.

### If you use hardware inventory for distributed views, you can't onboard to Desktop Analytics

<!-- 4950335 -->
*Applies to: Configuration Manager version 1902 with update rollup, and version 1906*

If you have a hierarchy, and enable **Hardware inventory** site data for [distributed views](../../../plan-design/hierarchy/database-replication.md#bkmk_distviews) on any site replication links, after you configure the Desktop Analytics connection in Configuration Manager you'll see the following error in M365UploadWorker.log:

`Unexpected exception 'System.Data.SqlClient.SqlException' Remote access is not supported for transaction isolation level "SNAPSHOT".:    at System.Data.SqlClient.SqlConnection.OnError(SqlException exception, Boolean breakConnection, Action'1 wrapCloseInAction)`

To work around this issue, disable **Hardware inventory** site data for distributed views on every site replication link.

## Cloud services

### Azure service for US Government cloud shows as public cloud

<!-- 6036748 -->

*Applies to version 1910*

If you create a connection to an Azure service, and set the **Azure environment** to the government cloud, the properties of the connection show the environment as the Azure public cloud. This issue is only a display problem in the console, the service is in the government cloud. To confirm the configuration, run the following SQL query on the site database:

```SQL
Select Environment, Name, TenantID From AAD_Tenant_Ex
```

For the government cloud, the result of this query is `2` for the specific tenant.

### Can't download content from a cloud management gateway enabled for TLS 1.2

<!-- 5771680 -->

*Applies to version 1906, 1910 early update ring*

If you enable a cloud management gateway (CMG) to **function as a cloud distribution point and serve content from Azure storage** and **Enforce TLS 1.2**, you may see content downloads fail.

The following errors show in the DataTransferService.log on the client:

``` log
Request to https://cmg1.contoso.com:443/downloadrestservice.svc/getcontentxmlsecure?pid=CMG00013&cid=CMG00013&tid=GUID:3fb5cf5d-28a5-4460-ab39-9184ca214369&iss=CMDP.IAAS2.CONTOSO.COM&alg=1.2.840.113549.1.1.11&st=2019-11-19T01:44:04&et=2019-11-19T09:44:04 failed with 400
Successfully queued event on HTTP/HTTPS failure for server 'cmg1.contoso.com'.
Error sending DAV request. HTTP code 400, status 'Bad Request'
GetDirectoryList_HTTP('https://cmg1.contoso.com:443/downloadrestservice.svc/getcontentxmlsecure?pid=CMG00013&cid=CMG00013&tid=GUID:3fb5cf5d-28a5-4460-ab39-9184ca214369&iss=CMDP.IAAS2.CONTOSO.COM&alg=1.2.840.113549.1.1.11&st=2019-11-19T01:44:04&et=2019-11-19T09:44:04') failed with code 0x87d0027e.​
Error retrieving manifest (0x87d0027e).
```

The following errors show in the CMGContentService.log on the server:

``` log
ERROR: Exception processing request. Microsoft.WindowsAzure.Storage.StorageException: The underlying connection was closed: An unexpected error occurred on a receive. ---> System.Net.WebException: The underlying connection was closed: An unexpected error occurred on a receive. ---> System.ComponentModel.Win32Exception: The client and server cannot communicate, because they do not possess a common algorithm...
```

To work around this issue:

- Update the site to the globally available version of 1910, released on December 20, 2019. (If you previously updated to the 1910 early update ring, you need to update to this build when it's available.)

- Alternatively, use a traditional [cloud distribution point](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md). That role doesn't enforce TLS 1.2, but is compatible with clients that require TLS 1.2.

## Protection

### BitLocker management appears in version 1906

*Applies to version 1906*

<!-- 5984688 -->

After November 21, 2019, if you update to version 1906 from version 1902 or earlier, the BitLocker management feature will be turned on and available. This feature is an optional feature starting in version 1910. It's unsupported in version 1906. If you try to use it in version 1906, you may experience unexpected results. If you don't use the feature, there's no impact.

To use the [BitLocker management feature](../../../../protect/plan-design/bitlocker-management.md), update to version 1910.

<!--
## Backup and recovery

## Client deployment and upgrade
-->
