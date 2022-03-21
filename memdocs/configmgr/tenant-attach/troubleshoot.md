---
title: Troubleshoot tenant attach and device actions
titleSuffix: Configuration Manager
description: Troubleshoot tenant attach and device actions for Configuration Manager.
ms.date: 09/09/2021
ms.topic: troubleshooting
ms.prod: configuration-manager
ms.technology: configmgr-core
manager: dougeby
author: mestew
ms.author: mstewart
ms.localizationpriority: high
---

# Troubleshooting tenant attach and device actions

*Applies to: Configuration Manager (current branch)*

Starting with Configuration Manager 2002, Configuration Manager clients can be synced to Microsoft Endpoint Manager admin center. Some client actions can be run from the Microsoft Endpoint Manager admin center on the synchronized clients.

The available actions are:
- Sync Machine Policy
- Sync User Policy
- App Evaluation Cycle


[![Device overview in Microsoft Endpoint Manager admin center](./media/3555758-device-overview-actions.png)](./media/3555758-device-overview-actions.png#lightbox)
  
When an admin runs an action from Microsoft Endpoint Manager admin center, the notification request is forwarded to Configuration Manager site, and from the site to the client.

## Log files

Use the following logs located on the service connection point:

- **CMGatewaySyncUploadWorker.log**
- **CMGatewayNotificationWorker.log**

Use the following logs located on the management point:

- **BgbServer.log**

Use the following logs located on the client:

- **CcmNotificationAgent.log**

## <a name="bkmk_review"></a> Review your upload

1. Open **CMGatewaySyncUploadWorker.log** from &lt;ConfigMgr install directory>\Logs.
1. The next sync time is noted by log entries similar to `Next run time will be at approximately: 02/28/2020 16:35:31`.
1. For device uploads, look for log entries similar to `Batching N records`. **N** is the number of changed devices uploaded since the last upload.
1. The upload occurs every 15 minutes for changes. Once changes are uploaded, it may take an additional 5 to 10 minutes for client changes to appear in **Microsoft Endpoint Manager admin center**.


## Configuration Manager components and log flow

- **SMS_SERVICE_CONNECTOR**: Uses the Gateway Notification Worker for processing the notification from Microsoft Endpoint Manager admin center.
- **SMS_NOTIFICATION_SERVER**: Gets the notification and creates a client notification.
- **BgbAgent**: The client gets task and runs the requested action.

### SMS_SERVICE_CONNECTOR

When an action is initiated from the Microsoft Endpoint Manager admin center, **CMGatewayNotificationWorker.log** processes the request.  

```text
Received new notification. Validating basic notification details...
Validating device action message content...
Authorized to perform client action. TemplateID: RequestMachinePolicy TenantId: a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2 AADUserID:     a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2
Forwarded BGB remote task. TemplateID: 1 TaskGuid: a43dd1b3-a006-4604-b012-5529380b3b6f TaskParam: TargetDeviceIDs: 1  
```
 
1. A notification is received from Microsoft Endpoint Manager admin center.

   ```text
   Received new notification. Validating basic notification details..
   ```

1. User and device actions are validated.

   ```text
   Validating device action message content... 
   Authorized to perform client action. TemplateID: RequestMachinePolicy TenantId: a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2 AADUserID:     a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2
   ```

1. The remote task is forwarded to the SMS_NOTIFICATION_SERVER.

    ```text
   Forwarded BGB remote task. TemplateID: 1 TaskGuid: a43dd1b3-a006-4604-b012-5529380b3b6f TaskParam: TargetDeviceIDs: 1  
    ```


### SMS_NOTIFICATION_SERVER

Once the message is sent to the SMS_NOTIFICATION_SERVER, a task is sent from the management point to the corresponding client. You'll see the below in the **BgbServer.log**, which is on the management point:

```text
Get one push message from database.
Starting to send push task (PushID: 7 TaskID: 8 TaskGUID: A43DD1B3-A006-4604-B012-5529380B3B6F TaskType: 1 TaskParam: ) to 1 clients  with throttling (strategy: 1 param: 42)
```

### BgbAgent

The last step occurs on the client and can be seen in the **CcmNotificationAgent.log**. Once the task is received, it will request scheduler to perform the action. When the action is performed, you'll see a confirmation message:

```text
Receive task from server with pushid=7, taskid=8, taskguid=A43DD1B3-A006-4604-B012-5529380B3B6F, tasktype=1 and taskParam=

Send Task response message <BgbResponseMessage TimeStamp="2020-01-21T15:43:43Z"><PushID>8</PushID><TaskID>9</TaskID><ReturnCode>1</ReturnCode></BgbResponseMessage> successfully.
```

## Common issues

### <a name="bkmk_noauth"></a> Unauthorized to perform client action

If the admin doesn't have the required permissions in Configuration Manager, you'll see an `Unauthorized` response in the **CMGatewayNotificationWorker.log**.

```text
Received new notification. Validating basic notification details..
Validating device action message content...
Unauthorized to perform client action. TemplateID: RequestMachinePolicy TenantId: a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2 AADUserID: 3a1e89e6-e190-4615-9d38-a208b0eb1c78
```  

Ensure the user running the action from the Microsoft Endpoint Manager admin center has the required permissions on Configuration Manager site. For more information, see [Microsoft Endpoint Manager tenant attach prerequisites](device-sync-actions.md#prerequisites).



## Known issues

### Data synchronization failures

<!-- 10877392 -->

If you have issues viewing the tenant attach details in the Microsoft Endpoint Manager admin center, it may be because of an issue with the hierarchy onboarding configuration. This issue can be caused by onboarding a hierarchy that's already onboarded.

You can also detect this issue from entries in the **GenericUploadWorker.log** and **CMGatewayNotificationWorker.log** files. For more information, see [Example errors in log files that require resetting the tenant attach configuration](#example-errors-in-log-files-that-require-resetting-the-tenant-attach-configuration).

#### Workaround for data synchronization failures

To reset the tenant attach configuration:

1. Offboard the hierarchy. For more information, see [Offboard from tenant attach](device-sync-actions.md#bkmk_offboard).

1. Wait at least two hours for the service to clean up the existing record.

1. Onboard the hierarchy again. For more information, see [Enable tenant attach](device-sync-actions.md).

#### Example errors in log files that require resetting the tenant attach configuration

##### Errors for AccountOnboardingInfo and DevicePost requests in GenericUploadWorker.log

```log
[OnboardScenario] Creating web request to: https://us.gateway.configmgr.manage.microsoft.com/api/gateway/AccountOnboardingInfo Method: POST Activity ID: ed2186a0-fb43-4cf1-84df-9283dd45a461 Timeout: 00:02:00
[OnboardScenario] Response from https://us.gateway.configmgr.manage.microsoft.com/api/gateway/AccountOnboardingInfo is: 400 (Bad Request)
Response status code: 400 (BadRequest) Activity ID: a579728b-eca0-4144-80ac-eea25ee5bcf6
Unexpected exception for worker GenericUploadWorker
Exception details:
[Critical][GenericUploadWorker][0][System.Net.WebException][0x80131509]
The remote server returned an error: (400) Bad Request.    at Microsoft.ConfigurationManager.ServiceConnector.ExtensionMethods.<GetResponseAsync>d__13.MoveNext()

[UploadDelta_HelpdeskUpload] Response from https://us.gateway.configmgr.manage.microsoft.com/api/gateway/DevicePost is: 401 (Unauthorized)
Response status code: 401 (Unauthorized) Activity ID: 6daac983-5f94-464e-b1bd-9b634a051d1d
[WebException]: Failed to upload data to 'https://us.gateway.configmgr.manage.microsoft.com/api/gateway/DevicePost'
Exception details:
[Warning][GenericUploadWorker][0][System.Net.WebException][0x80131509]
The remote server returned an error: (401) Unauthorized.    at Microsoft.ConfigurationManager.ServiceConnector.ExtensionMethods.<GetResponseAsync>d__13.MoveNext()
```

##### Errors for device actions in CMGatewayNotificationWorker.log

```log
[GetNotifications] Response from https://us.gateway.configmgr.manage.microsoft.com/api/gateway/Notification is: 401 (Unauthorized)
Response status code: 401 (Unauthorized) Activity ID: 4c536a72-fd7f-4d08-948a-3e65d2129e44
Web exception when getting new notification
Exception details:
[Warning][CMGatewayNotificationWorker][0][System.Net.WebException][0x80131509]
The remote server returned an error: (401) Unauthorized.    at Microsoft.ConfigurationManager.ServiceConnector.ExtensionMethods.<GetResponseAsync>d__13.MoveNext()
Response in the web exception: {"Message":"An error has occurred."}
```

### Specific devices don't synchronize

<!--7099564-->
It's possible that specific devices, which are Configuration Manager clients, won't be uploaded to the service.

**Impacted devices:**
If a device is a distribution point that uses the same PKI certificate for both the distribution point functionality and its client agent, then the device won't be included in the tenant attach device sync.

**Behavior:** When performing tenant attach during the on-boarding phase, a full sync is performed the first time. Subsequent sync cycles are delta synchronizations. Any update to the impacted devices will cause the device to be removed from the sync.

[!INCLUDE [Known issues shared across tenant attach features](includes/known-issues-shared.md)]

## Next steps

- [Troubleshoot ConfigMgr client details](troubleshoot-client-details.md)
- [Enable co-management](../comanage/overview.md) to get additional cloud-powered capabilities like conditional access.
