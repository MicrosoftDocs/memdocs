---
title: Release notes
titleSuffix: Configuration Manager
description: Learn about urgent issues that aren't yet fixed in the product or covered in a Microsoft Support knowledge base article.
ms.date: 07/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
---

# Release notes for Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

With Configuration Manager, product release notes are limited to urgent issues. These issues aren't yet fixed in the product, or detailed in a Microsoft Support knowledge base article.  

Feature-specific documentation includes information about known issues that affect core scenarios.  

This article contains release notes for the current branch of Configuration Manager. For information on the technical preview branch, see [Technical Preview](/sccm/core/get-started/technical-preview)  

For information about the new features introduced with different versions, see the following articles:

- [What's new in version 1906](/sccm/core/plan-design/changes/whats-new-in-version-1906)  
- [What's new in version 1902](/sccm/core/plan-design/changes/whats-new-in-version-1902)
- [What's new in version 1810](/sccm/core/plan-design/changes/whats-new-in-version-1810)
- [What's new in version 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806)  

> [!Tip]  
> To get notified when this page is updated, copy and paste the following URL into your RSS feed reader: 
> `https://docs.microsoft.com/api/search/rss?search=%22release+notes+-+Configuration+Manager%22&locale=en-us`


## Set up and upgrade  

### Setup prerequisite warning on domain functional level on Server 2019

<!-- 4904376 -->

*Applies to version 1906*

When installing the update for version 1906 in an environment with domain controllers running Windows Server 2019, the prerequisite check for domain functional level returns the following warning:

`[Completed with warning]:Verify that the Active Directory domain functional level is Windows Server 2003 or later`

#### Workaround

Ignore the warning.

### Azure AD user discovery and collection group sync don't work after site expansion

<!-- 4797313 -->
*Applies to version 1906*

After you configure either of the following features:

- Azure Active Directory user group discovery
- Synchronize collection membership results to Azure Active Directory groups

If you then expand a standalone primary site to a hierarchy with a central administration site, you'll see the following error in SMS_AZUREAD_DISCOVERY_AGENT.log:

`Could not obtain application secret for tenant xxxxx. If this is after a site expansion, please run "Renew Secret Key" from admin console.`

#### Workaround

Renew the key associated with the app registration in Azure AD. For more information, see [Renew secret key](/sccm/core/servers/deploy/configure/azure-services-wizard#bkmk_renew).


### Setup command-line option JoinCEIP must be specified

<!--510806-->
*Applies to: Configuration Manager version 1802*

Starting in Configuration Manager version 1802, the Customer Experience Improvement Program (CEIP) feature is removed from the product. When [automating installation](/sccm/core/servers/deploy/install/command-line-options-for-setup) of a new site from a command-line or unattended script, setup returns an error that a required parameter is missing.

#### Workaround

While it has no effect on the outcome of the setup process, include the **JoinCEIP** parameter in your setup command line.

> [!Note]  
> The EnableSQM parameter for [console setup](/sccm/core/servers/deploy/install/install-consoles) is not required.

### Cloud service manager component stopped on site server in passive mode

<!--VSO 2858826, SCCMDocs issue 772-->
*Applies to: Configuration Manager version 1806*

If the [service connection point](/sccm/core/servers/deploy/configure/about-the-service-connection-point) is colocated with a [site server in passive mode](/sccm/core/servers/deploy/configure/site-server-high-availability), then deployment and monitoring of a [cloud management gateway](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway) doesn't start. The cloud service manager component (SMS_CLOUD_SERVICES_MANAGER) is in a stopped state.

#### Workaround

Move the service connection point role to another server.


<!-- ## Backup and recovery  -->

<!--## Client deployment and upgrade-->


## OS deployment

### After passive site server is promoted, the default boot image packages still have package source on the previous active server

<!--3453224, SCCMDocs-pr issue 3097-->
*Applies to: Configuration Manager version 1810*

If you have a site server in passive mode (server B), when you promote it to active, the content location for the default boot images continues to reference the previously active server (server A). If server A has a hardware failure, you can't update or change the default boot images.

#### Workaround

None


## Software updates

### Security roles are missing for phased deployments

<!--3479337, SCCMDocs-pr issue 3095-->
*Applies to: Configuration Manager versions 1810, 1902*

The **OS Deployment Manager** built-in security role has permissions to [phased deployments](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence). The following roles are missing these permissions:  

- **Application Administrator**  
- **Application Deployment Manager**  
- **Software Update Manager**  

The **App Author** role may appear to have some permissions to phased deployments, but shouldn't be able to create deployments.

A user with one these roles can start the Create Phased Deployment wizard, and can see phased deployments for an application or software update. They can't complete the wizard, or make any changes to an existing deployment.

#### Workaround

Create a custom security role. Copy an existing security role, and add the following permissions on the **Phased Deployment** object class:

- Create  
- Delete  
- Modify  
- Read  

For more information, see [Create custom security roles](/sccm/core/servers/deploy/configure/configure-role-based-administration#BKMK_CreateSecRole)

### Changing Office 365 client setting doesn't apply

<!--511551-->
*Applies to: Configuration Manager version 1802*  

Deploy a [client setting](/sccm/core/clients/deploy/about-client-settings#enable-management-of-the-office-365-client-agent) with **Enable Management of the Office 365 Client Agent** configured to `Yes`. Then change that setting to `No` or `Not Configured`. After updating policy on targeted clients, Office 365 updates are still managed by Configuration Manager.

#### Workaround

Change the following registry value to `0` and restart the **Microsoft Office Click-to-Run Service** (ClickToRunSvc):

```Registry
[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\office\16.0\Common\officeupdate]
"OfficeMgmtCOM"=dword:00000000
```

## Desktop Analytics

### If you use hardware inventory for distributed views, you can't onboard to Desktop Analytics

<!-- 4950335 -->
*Applies to: Configuration Manager version 1902 with update rollup, and version 1906*

If you have a hierarchy, and enable **Hardware inventory** site data for [distributed views](../../../plan-design/hierarchy/database-replication.md#bkmk_distviews) on any site replication links, after you configure the Desktop Analytics connection in Configuration Manager you'll see the following error in M365UploadWorker.log:

`Unexpected exception 'System.Data.SqlClient.SqlException' Remote access is not supported for transaction isolation level "SNAPSHOT".:    at System.Data.SqlClient.SqlConnection.OnError(SqlException exception, Boolean breakConnection, Action'1 wrapCloseInAction)`

#### Workaround

Disable **Hardware inventory** site data for distributed views on every site replication link.


### Console unexpectedly closes when removing collections

<!-- 4749443 -->
*Applies to: Configuration Manager version 1902 with update rollup*

After you connect the site to [Desktop Analytics](/sccm/desktop-analytics/connect-configmgr), you can **Select specific collections to synchronize with Desktop Analytics**. If you remove a collection and apply the changes, immediately adding a new collection causes an unhandled exception. The console unexpectedly closes.

#### Workaround

When you remove a collection, select **OK** to close the properties window. Then open the properties again to add a new collection on the **Desktop Analytics Connection** tab.

### Pilot status tile shows some devices as 'undefined'

<!-- 4547783 -->
*Applies to: Configuration Manager version 1902 with update rollup*

When you use the Configuration Manager console to monitor your pilot deployment status, pilot devices that are up-to-date on the target version of Windows for that deployment plan show as **undefined** in the Pilot status tile.  

These **undefined** devices are **up-to-date** with the target version of the OS for that deployment plan. No further action is necessary.


## Mobile device management  

### Validation for iOS app link sometimes fails on valid link

*Applies to: Configuration Manager version 1810 and earlier*

<!-- LSI 106004348 -->
When you create a new application of type **App Package for iOS from App Store**, the validator doesn't accept some valid URLs for the **Location**. Specifically, the iOS App Store doesn't require a value for the app name section of the URL. For example, both of the following links are valid and point to the same app, but the **Create Application Wizard** only accepts the first:

- `https://itunes.apple.com/us/app/app-name/id123456789?mt=8`
- `https://itunes.apple.com/us/app//id123456789?mt=8`

#### Workaround

When you create an iOS app that's missing the app name from the URL, add any value as if it were the app name to the URL. For example:

- `https://itunes.apple.com/us/app/any-string/id123456789?mt=8`

This action allows you to complete the wizard. The app is still successfully deployed to iOS devices. The string you add to the URL appears as the **Name** on the **General Information** tab in the wizard. It's also the app's label in the Company Portal.




<!-- ## Reports and monitoring    -->
<!-- ## Conditional access   -->

<!-- ## Endpoint Protection -->
