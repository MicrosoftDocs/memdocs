---
title: Troubleshoot MSfB integration
titleSuffix: Configuration Manager
description: Provides suggestions and resolutions to troubleshoot some of the most common problems with Microsoft Store for Business integration.
ms.date: 08/29/2019
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

This article provides key troubleshooting tips and fixes for some of the top issues that you may encounter with the Microsoft Store for Business (MSfB) integration with Configuration Manager.

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
<!-- add to log-files -->
This log file is located on the service connection point, under `\Logs` in the Configuration Manager installation directory. It records information about the communication with the cloud service. This information includes metadata, icons, packages, and license file retrieval.

#### Change log level
<!-- is this too detailed? -->
1. Edit \bin\x64\smsexec.exe.config
1. For source name="**MSfBSyncWorker**", change switchValue.

   See valid values (case sensitive):
   [TraceEventType Enum](https://docs.microsoft.com/dotnet/api/system.diagnostics.traceeventtype?redirectedfrom=MSDN&view=netframework-4.8)

1. Restart sms_executive required to pick up new log level. Note this will also kick off MSfB sync.

### SMS_CLOUDCONNECTION.log
<!-- add to log-files -->

This log file is located on the service connection point, under `\Logs` in the Configuration Manager installation directory. If the MSfBSyncWorker service isn't started, or repeatedly starts and stops, review the entries in this log file.

> [!NOTE]
> This log file is shared with other features.

### BusinessAppProcessWorker.log
<!-- add to log-files -->

This log file is located on the site server for the top-level site in the hierarchy. It's under `\Logs` in the Configuration Manager installation directory. It records information about the following processes:

- Insert the metadata information synced by the BusinessAppProcessWorker component into the database
- Process files in `\InstallDir\inboxes\businessappprocess.box`

#### Change log level
<!-- is this too detailed -->
1. Edit InstallDir\bin\x64\smsexec.exe.config.
1. For source name="**BusinessAppProcessWorker**", change switchValue. See valid values (case sensitive):

   [TraceEventType Enum](https://docs.microsoft.com/dotnet/api/system.diagnostics.traceeventtype?redirectedfrom=MSDN&view=netframework-4.8)

1. Restart sms_executive required to pick up new log level. Note this will also kick off MSfB sync.

### SMS_BUSINESS_APP_PROCESS_MANAGER.log

This log file is located on the site server for the top-level site in the hierarchy. It's under `\Logs` in the Configuration Manager installation directory. If the BusinessAppProcessWorker service isn't started, or repeatedly starts and stops, review the entries in this log file.



## Common issues

### Last sync status is failed

When the last sync status is failed. Check the following files for issues on the site system with the Service Connection Point installed to identify the symptom.

- Check the <InstallDir>\Logs\MSfBSyncWorker.log for errors.
- Check the <InstallDir>\Logs\SMS_CLOUDCONNECTION.log for status messages.

#### Symptom 1: Sync fails and MSfBSyncWorker.log has an authorization error

##### Cause

This can occur if the configured AAD application (ClientID) does not have permissions to manage the Microsoft Store for Business for this tenant.

##### Workaround

1. Browse to the MSfB web portal and log in as MSfB administrator.
1. Navigate to **Settings** -> **Management tools**.
1. If the application is not listed, select **Add a management tool**, then search and select the AAD application (by name) associated with the ClientID that Configuration Manager is configured to use for MSfB integration.
1. If the status does not show **Active**, then under the **Action** column, click **Activate**.
1. From Configuration Manager, retrigger a sync or wait for the next sync interval to occur.

#### Symptom 2: Sync fails and MSfBSyncWorker.log has an error that the secret key is invalid

##### Cause

This can occur if the Secret key entered in the configuration of MSfB has expired.

##### Resolution

1. From the Azure Active Directory portal, create a new secret key for the client.
1. In the Configuration Manager UI, navigate to **Administration** \ **Cloud Services** \ **Microsoft Store for Business**.
1. Select the AAD account and go to **Properties**.
1. Enter the new secret key.
1. Verify and apply changes.

#### Symptom 3: Sync fails and MSfBSyncWorker.log contains error getting application token

##### Cause

This can occur if the AAD application used during configuration of Microsoft Store for Business has been deleted from AAD.

##### Resolution

1. First, delete the existing AAD account for Microsoft Store for Business:

   1. Navigate to **Administration** \ **Cloud Services** \ **Microsoft Store for Business**.
   1. Select the existing account.
   1. Select **Delete**, then confirm.

1. Add the new AAD account for Microsoft Store for Business with properly set up AAD application.
1. Leave the **Microsoft Store for Business** node and return to the **Enable** button.
1. Select **Add Microsoft Store for Business Account**.

#### Symptom 4: Sync fails and MSfBSyncWorker.log contains error "Content location does not exist…"

##### Cause

This can occur if the configured share for syncing Microsoft Store for Business content does not exist or has incorrect permissions.

##### Workaround

1. If it does not already exist, create the share. To see what is configured:

   1. Go to **Administration** \ **Cloud Services** \ **Microsoft Store for Business**.
   1. Select **Account** \ **Properties**.
   1. Go to **Configuration** \ **Location** to store application content downloaded from the Microsoft Store for Business.

1. Check permissions on the share. Note that the **COMPUTER$** account where the SCP role is installed must have read and write permissions.
1. If you wish to reconfigure the location to a new location, you must delete the AAD account and re-add it with the new content location.

#### Symptom 5: Sync fails and MSfBSyncWorker.log contains error "Error occurred making http request calling 'GET' method"

##### Cause

This can occur if the sync of other applications took so long that the content URL received is expired.

##### Workaround

Retrying the sync should continue further each time, although it may take a several retries depending on how many offline applications you have, how big the packages are, and your network speed. You should see the error fewer times each subsequent attempt. If the number of errors does not decline, something else is happening.

> [!TIP]
> You can run "**Sync from Microsoft Store for Business**" in the Admin Console, **Administration** \ **Cloud Services** \ **Microsoft Store for Business** \ select **tenant**.

#### Symptom 6: Sync fails and MSfBSyncWorker.log contains error "Cannot write more bytes to the buffer…"

##### Cause

This can occur if the application's package is larger than 500MB. In Configuration Manager version 1610, only offline applications with packages that are less than 500MB in size are supported with automatic sync.

##### Workaround

While you cannot sync automatically, you can download the content and create the application manually:

1. From MSfBSynWorker.log, can get the failing application ID from this log line:

   *Error(s) syncing or downloading application ApplicationID from the Microsoft Store for Business.*

1. Sign in as the MSfB administrator and navigate to the application page in the Microsoft Store for Business web portal for the failing application. The URL should look something like this: **https://businessstore.microsoft.com/en-us/store/p/app/ApplicationID**
1. Click **Offline** if not already selected, then click the **Manage** button.
1. For all desired platforms, create a separate folder on your application content share.
1. Download the package to package folder.
1. Download the encoded license file as a .bin file to the package folder.
1. Download all required frameworks to the package folder.
1. In the Configuration Manager admin console, navigate to **Software Library** \ **Application Management** \ **Applications**.
1. Click **Create Application**.
1. Select **Manually specify the application information** and then click **Next**.
1. Populate **General Information** and **Application Catalog** as desired.
1. In the Deployment Types tab, create a Deployment Type for each downloaded platform (each folder in #4 above)
   
   1. Type: **Windows app package (*.appx, *.appxbundle)**.
   1. Point to the appx/appxbundle that represents the actual package (not required dependencies). On the **Import Information** page, once you see **Import succeeded**, confirm the details. There is a line starting with **License file:** that points to the .bin file. This is required for offline license to be properly absorbed and applied on clients. Also, under **Windows app dependencies:**, verify that all of the **required dependencies** are downloaded for this package.
   1. Complete wizard, filling in properties as desired.
    
### Sync doesn't occur as expected

When you click **Sync from Microsoft Store for Business**, and it does not trigger a new sync, or the sync is not occurring on daily basis, check the following files for issues to identify the specific symptom you encounter.

- Files on the top level site server (CAS or standalone primary)
  - \InstallDir\bin\x64\smsexec.exe.config
  - \InstallDir\Logs\ BusinessAppProcessWorker.log
  - \InstallDir\Logs\SMS_BUSINESS_APP_PROCESS_MANAGER.log
- Files on the site system with the Service Connection Point installed
  - \InstallDir\Logs\ MSfBSyncWorker.log
  - \InstallDir\Logs\SMS_CLOUDCONNECTION.log

#### Symptom 1: Clicking on "Sync from Microsoft Store for Business" does not trigger a sync

##### Cause

This can occur if syncs are triggered less than 10 minutes apart. Sync is not allowed more frequently than every 10 minutes.

##### Resolution

Wait for 10 minutes before requesting another sync.

#### Symptom 2: Sync not occurring on daily basis, MSfBSyncWorker fails to start

##### Cause

This can occur if the log level for MSfBSyncWorker is set incorrectly.

##### Resolution

1. Edit **\bin\x64\smsexec.exe.config**.
1. For source name= **MSfBSyncWorker**, update switchValue to a valid value.
1. Restart sms_executive. This is required to pick up the new log level.

   Note that this will also trigger a MSfB sync.

1. You should see the following line in **MSfBSyncWorker.log**:

   *Starting Microsoft Store for Business Sync Worker in component SMS_CLOUDCONNECTION*

#### Symptom 3: Sync not occurring on daily basis and System.NullReferenceException error in SMS_BUSINESS_APP_PROCESS_MANAGER.log

##### Cause

This can occur if the log level for BusinessAppProcessWorker is set incorrectly.

##### Resolution

1. Edit <*InstallDir*>\bin\x64\smsexec.exe.config.
1. For source name= **BusinessAppProcessWorker**, update switchValue to a valid value.
1. Restart sms_executive. This is required to pick up the new log level. Note this will also trigger a MSfB sync.
1. At this point you should no longer get the same exception in **SMS_BUSINESS_APP_PROCESS_MANAGER.log**.

#### Symptom 4: Sync not occurring on daily basis and "shutting down 2 workers" error in SMS_BUSINESS_APP_PROCESS_MANAGER.log

##### Cause

This can occur if MSfBSyncWorker is stopped by SMS_BUSINESS_APP_PROCESS_MANAGER.

##### Workaround

1. Restart sms_executive, or for less intrusive fix, complete #2 below.
1. Restart both components with MSfB workers together (stop both, then start both).
   1. Open the registry and navigate to

      **HKLM\SOFTWARE\Microsoft\SMS\COMPONENTS\SMS_EXECUTIVE\Threads\SMS_CLOUDCONNECTION**

   1. Set Requested Operation to **Stop**.
   1. Refresh to verify Current State = **Stopped**.
   1. Navigate to **HKLM\SOFTWARE\Microsoft\SMS\COMPONENTS\SMS_EXECUTIVE\Threads\SMS_BUSINESS_APP_PROCESS_MANAGER**.
   1. Set Requested Operation to **Stop**.
   1. Refresh to verify Current State = **Stopped**.
   1. In **SMS_CLOUDCONNECTION**, set Requested Operation to **Start**.
   1. In **SMS_BUSINESS_APP_PROCESS_MANAGER**, set Requested Operation to **Start**.

#### Symptom 5: Sync not occurring on daily basis and "shutting down 4 workers" error in SMS_BUSINESS_APP_PROCESS_MANAGER.log

##### Cause

This can occur if MSfBSyncWorker is stopped by SMS_BUSINESS_APP_PROCESS_MANAGER.

##### Workaround

1. start sms_executive, or for less intrusive fix, complete #2 below.
1. Restart both components with MSfB workers together (stop both, then start both)

   1. Open the registry and navigate to

      **HKLM\SOFTWARE\Microsoft\SMS\COMPONENTS\SMS_EXECUTIVE\Threads\SMS_CLOUDCONNECTION**

   1. Set Requested Operation to **Stop**.
   1. Refresh to verify Current State = **Stopped**.
   1. Navigate to **HKLM\SOFTWARE\Microsoft\SMS\COMPONENTS\SMS_EXECUTIVE\Threads\SMS_BUSINESS_APP_PROCESS_MANAGER**.
   1. Set Requested Operation to **Stop**.
   1. Refresh to verify Current State = **Stopped**.
   1. In **SMS_CLOUDCONNECTION**, set Requested Operation to **Start**.
   1. In **SMS_BUSINESS_APP_PROCESS_MANAGER**, set Requested Operation to **Start**.

### Language related issues

#### Symptom 1: Language selection changes are not being applied

##### Cause

This can occur if the language selection is cached and is not cleared after the property values are changed.

##### Workaround

To resolve this problem, restart the SMS_Executive service.

#### Symptom 2: Not all selected languages (including the default) are present for all license information

##### Cause

This can occur if the Microsoft Store for Business application represented by the license information does not contain localized data for language "X".

##### Workaround

To resolve this problem, the administrator can manually add any missing languages for created applications.

### Failed to install or create offline application

#### Symptom 1: Fail to create offline application: Content cannot be verified

##### Cause

This can occur if the synced content for the offline application has been corrupted or tampered with.

##### Workaround

To resolve this problem, trigger a new sync. When the sync completes, it should have redownloaded any corrupt content files.

#### Symptom 2: Fail to install application created from offline license information: Windows 10 supported versions

##### Cause

This can occur is the application is deployed to a client running a version of Windows prior to build 1511. Offline licensed apps from the Microsoft Store for Business are only supported on the Windows 10 November 2015 (1511) release and later.

##### Resolution

Install the latest version of Windows 10.


## Next steps

To find additional help, see [Find help for using Configuration Manager](/sccm/core/understand/find-help).

<!-- these videos are old...1604/1605, with LaCranda narrating! is there still benefit in linking to them?
- Here are also some videos to learn more about it:

  - [How to set up the required prerequisites in AAD and the Microsoft Store for Business portal](https://www.youtube.com/watch?v=fC1AQY42flQ)
  - [Choose languages to sync and create apps from app metadata for each Microsoft Store for Business, and how to create apps from app metadata](https://www.youtube.com/watch?v=VJs-475rfaI)
 -->