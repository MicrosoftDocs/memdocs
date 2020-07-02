---
title: Troubleshoot device action
titleSuffix: Configuration Manager
description: "Troubleshoot device actions technical reference for Configuration Manager"
ms.date: 04/01/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 44c2eb8a-3ccc-471f-838b-55d7971bb79e
manager: dougeby
author: mestew
ms.author: mstewart
---

# Troubleshooting device actions for Configuration Manager devices

*Applies to: Configuration Manager (current branch)*

Starting with Configuration Manager 2002, Configuration Manager clients can be synced to Microsoft Endpoint Manager admin center. Some client actions can be run from the Microsoft Endpoint Manager admin center on the synchronized clients.

The available actions are:
- Sync Machine Policy
- Sync User Policy
- App Evaluation Cycle


[![Device overview in Microsoft Endpoint Manager admin center](./media/3555758-device-overview-actions.png)](./media/3555758-device-overview-actions.png#lightbox)
  
When an admin runs an action from Microsoft Endpoint Manager admin center, the notification request is forwarded to Configuration Manager site, and from the site to the client.

## Configuration Manager components

- **SMS_SERVICE_CONNECTOR**: Uses the Gateway Notification Worker for processing the notification from Microsoft Endpoint Manager admin center.
- **SMS_NOTIFICATION_SERVER**: Gets the notification and creates a client notification.
- **BgbAgent**: The client gets task and runs the requested action.

## SMS_SERVICE_CONNECTOR

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


## SMS_NOTIFICATION_SERVER

Once the message is sent to the SMS_NOTIFICATION_SERVER, a task is sent from the management point to the corresponding client. You'll see the below in the **BgbServer.log**, which is on the management point:

```text
Get one push message from database.
Starting to send push task (PushID: 7 TaskID: 8 TaskGUID: A43DD1B3-A006-4604-B012-5529380B3B6F TaskType: 1 TaskParam: ) to 1 clients  with throttling (strategy: 1 param: 42)
```

## BgbAgent

The last step occurs on the client and can be seen in the **CcmNotificationAgent.log**. Once the task is received, it will request scheduler to perform the action. When the action is performed, you'll see a confirmation message:

```text
Receive task from server with pushid=7, taskid=8, taskguid=A43DD1B3-A006-4604-B012-5529380B3B6F, tasktype=1 and taskParam=

Send Task response message <BgbResponseMessage TimeStamp="2020-01-21T15:43:43Z"><PushID>8</PushID><TaskID>9</TaskID><ReturnCode>1</ReturnCode></BgbResponseMessage> successfully.
```

## Common issues

If the admin doesn't have the required permissions in Configuration Manager, you'll see an `Unauthorized` response in the **CMGatewayNotificationWorker.log**.

```text
Received new notification. Validating basic notification details..
Validating device action message content...
Unauthorized to perform client action. TemplateID: RequestMachinePolicy TenantId: a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2 AADUserID: 3a1e89e6-e190-4615-9d38-a208b0eb1c78
```  

Ensure the user running the action from the Microsoft Endpoint Manager admin center has the required permissions on Configuration Manager site. For more information, see [Microsoft Endpoint Manager tenant attach prerequisites](device-sync-actions.md#prerequisites).

## Next steps

[Enable co-management](../comanage/overview.md) to get additional cloud-powered capabilities like conditional access.
