---
title: Troubleshoot MSfB integration
titleSuffix: Configuration Manager
description: Provides suggestions and resolutions to troubleshoot some of the most common problems with Microsoft Store for Business integration.
ms.date: 08/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 09929057-ecf2-4d49-aee0-709916932b14
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
---

# Troubleshoot the Microsoft Store for Business integration with Configuration Manager

This article provides key troubleshooting tips and fixes for some of the top issues that you may have with the Microsoft Store for Business (MSfB) integration with Configuration Manager.

For more information about using the Microsoft Store for Business with Configuration Manager, see [Manage apps from the Microsoft Store for Business with Configuration Manager](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business).

## Monitor

### Component status

In the Configuration Manager console, go to the **Monitoring** workspace, expand **System Status**, and select the **Component Status** node. Monitor status of the following components:

- SMS_BUSINESS_APP_PROCESS_MANAGER
- SMS_CLOUDCONNECTION

### Sync status

In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select the **Microsoft Store for Business** node. Check the **Last Sync Status** column.

### View synchronized apps

In the Configuration Manager console, go to the **Software Library** workspace, expand **Application Management**, and select the **License Information for Store Apps** node.


## Log files

### MSfBSyncWorker.log

This log file is located on the service connection point, under `\Logs` in the Configuration Manager installation directory. It records information about the communication with the cloud service. This information includes metadata, icons, packages, and license file retrieval.

To change the log level, change the `LoggingLevel` value to `0` in the `HKLM\SOFTWARE\Microsoft\SMS\Tracing\SMS_CLOUDCONNECTION` registry key. For more information, see [Configure logging options](/sccm/core/plan-design/hierarchy/about-log-files#bkmk_reg-site).

### SMS_CLOUDCONNECTION.log

This log file is located on the service connection point, under `\Logs` in the Configuration Manager installation directory. If the MSfBSyncWorker service isn't started, or repeatedly starts and stops, review the entries in this log file.

> [!NOTE]
> This log file is shared with other features.

### BusinessAppProcessWorker.log

This log file is located on the site server for the top-level site in the hierarchy. It's under `\Logs` in the Configuration Manager installation directory. It records information about the following processes:

- Insert the metadata information synced by the BusinessAppProcessWorker component into the database
- Process files in `\InstallDir\inboxes\businessappprocess.box`

### SMS_BUSINESS_APP_PROCESS_MANAGER.log

This log file is located on the site server for the top-level site in the hierarchy. It's under `\Logs` in the Configuration Manager installation directory. If the BusinessAppProcessWorker service isn't started, or repeatedly starts and stops, review the entries in this log file.



## Last sync failed

When the last sync status is *failed*, start by reviewing the following [log files](#log-files) to identify the symptom:

- MSfBSyncWorker.log
- SMS_CLOUDCONNECTION.log

Then look at one of the following sections for common issues:

- [Authorization error](#bkmk_fail-symptom1)
- [The secret key is invalid](#bkmk_fail-symptom2)
- [Error getting application token](#bkmk_fail-symptom3)
- [Content location does not exist](#bkmk_fail-symptom4)
- [Error occurred making http request calling 'GET' method](#bkmk_fail-symptom5)
- [Cannot write more bytes to the buffer](#bkmk_fail-symptom6)

### <a name="bkmk_fail-symptom1"></a> Authorization error

#### Cause

This issue can occur if the configured Azure Active Directory (Azure AD) application doesn't have permissions to manage the Microsoft Store for Business for this tenant.

#### Workaround

1. Open the [Microsoft Store for Business portal](https://www.microsoft.com/business-store), and sign in as an administrator.
1. Go to **Settings**, and select **Management tools**.
1. If the application isn't listed, select **Add a management tool**. Then search by name and select the Azure AD application associated with the same ClientID as Configuration Manager.
1. If the status doesn't show **Active**, then select **Activate** in the **Action** section.
1. In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select the **Microsoft Store for Business** node. Synchronize with the store, or wait for the next sync interval to occur.

> [!Tip]
> To find the ClientID in Configuration Manager:
>
> 1. In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select the **Azure Active Directory Tennts** node.
> 1. Select the tenant that you use for the Microsoft Store for Business integration.
> 1. In the results pane, find the matching application, and look at the **Client ID** column.

### <a name="bkmk_fail-symptom2"></a> The secret key is invalid

#### Cause

This issue can occur if the secret key has expired on the Azure AD app for the Microsoft Store for Business configuration.

#### Resolution

Renew the secret key for the Azure AD application. For more information, see [Renew secret key](/sccm/core/servers/deploy/configure/azure-services-wizard#bkmk_renew).

### <a name="bkmk_fail-symptom3"></a> Error getting application token

#### Cause

This issue can occur if the connected app no longer exists in Azure AD.

#### Resolution

Delete and recreate the connection to the Microsoft Store for Business.

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select the **Microsoft Store for Business** node.
1. Select the existing connection.
1. Select **Delete** in the ribbon.

Then recreate the connection. For more information, see the following articles:

- [Configure Azure Services](/sccm/core/servers/deploy/configure/azure-services-wizard)
- [Set up Microsoft Store for Business synchronization](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business#bkmk_setup)

### <a name="bkmk_fail-symptom4"></a> Content location does not exist

#### Cause

When you set up the Microsoft Store for Business connection, you specify a network share for storing synchronized content. This issue can occur if this share doesn't exist or has incorrect permissions.

To see the location that you configured:

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select the **Microsoft Store for Business** node.

1. Select the account and open its **Properties**.

1. Switch to the **Configuration** tab. The **Location** setting shows the network path to store application content downloaded from the Microsoft Store for Business.

#### Workaround

1. If it doesn't already exist, create the share.

1. Check NTFS permissions on the folder, and the permissions on the network share. Grant the computer account of the service connection point **Read** and **Write** permissions.

If you want to reconfigure the location, delete and recreate the connection with the new content location.

### <a name="bkmk_fail-symptom5"></a> Error occurred making http request calling 'GET' method

#### Cause

This issue can occur if the sync of applications from the store took so long that the content URL expired.

#### Workaround

Retry the sync process

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select the **Microsoft Store for Business** node.
1. Select the connection. In the ribbon, select **Sync from Microsoft Store for Business**.

With each time, it should continue further. It may take several retries depending on the following factors:

- The number of offline applications
- The size of the packages
- The network speed

With each attempt, you should see the error fewer times. If the number of errors doesn't reduce, there's another issue.

### <a name="bkmk_fail-symptom6"></a> Cannot write more bytes to the buffer

#### Cause

This issue can occur if the application's package is larger than 500 MB. Configuration Manager only supports automatic synchronization of offline applications with packages less than 500 MB.

#### Workaround

You can't automatically sync these apps, but you can download the content, and manually create the application:

1. Get the failing application ID from the following line in **MSfBSynWorker.log**:

    `Error(s) syncing or downloading application <ApplicationID> from the Microsoft Store for Business.`

1. Go to the [Microsoft Store for Business portal](https://www.microsoft.com/business-store), and sign in as a store administrator. Find the page for this application.

    > [!Tip]
    > The URL for the page is similar to: `https://businessstore.microsoft.com/en-us/store/p/app/ApplicationID`

    1. Select **Offline**, if it isn't already selected. Then select **Manage**.

    1. Create a separate folder on your application content share for all supported platforms.

    1. Download the package to the package folder.

    1. Download the encoded license file as a `.bin` file to the package folder.

    1. Download all required frameworks to the package folder.

1. In the Configuration Manager console, go to the **Software Library** workspace, expand **Application Management**, and select the **Applications** node.

1. [Create an application](/sccm/apps/deploy-use/create-applications), manually specifying the application information.

    1. Create a deployment type for each supported platform that you previously downloaded.

    1. Type: **Windows app package (\*.appx, \*.appxbundle)**

    1. Specify the appx/appxbundle for the actual app package, not a required dependency package.

Confirm the following details on the final **Import Information** page:

- **License file:** Specifies the `.bin` file. This license file is required for offline apps.
- **Windows app dependencies:** Verify that all of the required dependencies are downloaded for this package.


## Sync doesn't run

This section covers the following sync issues:

- You manually start the sync process, but it doesn't run
- The site doesn't automatically sync each day

Start by reviewing the following [log files](#log-files) to identify the symptom:

- BusinessAppProcessWorker.log
- SMS_BUSINESS_APP_PROCESS_MANAGER.log
- MSfBSyncWorker.log
- SMS_CLOUDCONNECTION.log

Then look at one of the following sections for common issues:

- [Manual sync doesn't start](#bkmk_sync-symptom1)
- [Automatic daily sync doesn't run and "shutting down # workers" error in SMS_BUSINESS_APP_PROCESS_MANAGER.log](#bkmk_sync-symptom2)

### <a name="bkmk_sync-symptom1"></a> Manual sync doesn't start

#### Cause

This issue can occur if you start a sync less than 10 minutes after the previous sync. You can't sync more frequently than every 10 minutes.

#### Resolution

Wait for at least 10 minutes before starting another sync.

### <a name="bkmk_sync-symptom2"></a> Automatic daily sync doesn't run and "shutting down # workers" error in SMS_BUSINESS_APP_PROCESS_MANAGER.log

#### Cause

This issue can occur if the SMS_BUSINESS_APP_PROCESS_MANAGER component stops the MSfBSyncWorker thread. The error may specify either `2` or `4` workers.

#### Workaround

Restart the **SMS_EXECUTIVE** service.

If you're not able to restart that main service, stop both components with MSfB workers, and then start both:

1. Open the Windows registry on the server that runs the service connection point

1. Go to `HKLM\SOFTWARE\Microsoft\SMS\COMPONENTS\SMS_EXECUTIVE\Threads\SMS_CLOUDCONNECTION`

    1. Set Requested Operation to **Stop**.

    1. Refresh to verify Current State = **Stopped**.

1. Go to `HKLM\SOFTWARE\Microsoft\SMS\COMPONENTS\SMS_EXECUTIVE\Threads\SMS_BUSINESS_APP_PROCESS_MANAGER`

    1. Set Requested Operation to **Stop**.

    1. Refresh to verify Current State = **Stopped**.

1. In **SMS_CLOUDCONNECTION**, set Requested Operation to **Start**.

1. In **SMS_BUSINESS_APP_PROCESS_MANAGER**, set Requested Operation to **Start**.


## Language-related issues

This section includes the following common issues:

- [Language selection changes aren't applied](#bkmk_lang-symptom1)
- [Not all selected languages are present for all license information](#bkmk_lang-symptom2)

### <a name="bkmk_lang-symptom1"></a> Language selection changes aren't applied

#### Cause

This issue can occur if the language selection is cached, and isn't cleared after the property values are changed.

#### Workaround

To resolve this problem, restart the **SMS_Executive** service.

### <a name="bkmk_lang-symptom2"></a> Not all selected languages are present for all license information

#### Cause

This issue can occur if the Microsoft Store for Business application's license information doesn't contain localized data for the specified language.

#### Workaround

Manually add any missing languages for created applications.


## Offline applications

This section includes the following common issues:

- [Fail to create offline application because content can't be verified](#bkmk_off-symptom1)
- [Fail to install application created from offline license information](#bkmk_off-symptom2)

### <a name="bkmk_off-symptom1"></a> Fail to create offline application because content can't be verified

#### Cause

This issue can occur if the synchronized content for the offline application is corrupt or modified.

#### Workaround

Start a new sync. When the sync completes, it should verify and download any incorrect content files.

### <a name="bkmk_off-symptom2"></a> Fail to install application created from offline license information

#### Cause

This issue can occur if you deploy the application to a client running a version of Windows 10 earlier than version 1511. Offline licensed apps from the Microsoft Store for Business are only supported on Windows 10 version 1511 and later.

#### Resolution

Install the latest version of Windows 10.


## Next steps

To find additional help, see [Find help for using Configuration Manager](/sccm/core/understand/find-help).

<!-- these videos are old...1604/1605, is there still benefit in linking to them?
- Here are also some videos to learn more about it:

  - [How to set up the required prerequisites in AAD and the Microsoft Store for Business portal](https://www.youtube.com/watch?v=fC1AQY42flQ)
  - [Choose languages to sync and create apps from app metadata for each Microsoft Store for Business, and how to create apps from app metadata](https://www.youtube.com/watch?v=VJs-475rfaI)
 -->