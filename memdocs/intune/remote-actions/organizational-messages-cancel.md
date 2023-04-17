---
# required metadata
title: Cancel or delete organizational message | Microsoft Intune  
description: Cancel or delete an organizational message in the Microsoft Intune admin center.       
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/19/2023  
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology:
ms.assetid: 
# optional metadata

#ROBOTS:
#audience:

ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure 
ms.collection:
- tier2
- M365-identity-device-management
---

# Cancel or delete organizational messages      

*Applies to Windows 11*  

> [!IMPORTANT]
> This feature is in public preview. For more information, see [Public preview in Microsoft Intune](../fundamentals/public-preview.md).  

Cancel or delete an organizational message that you no longer need in Microsoft Intune.

## Cancel organizational message  
Cancel an active or scheduled organizational message. Cancelling stops active messages from being sent to additional surfaces and devices. It stops scheduled messages from being sent at all.  

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Go to **Tenant administration** > **Organizational messages (preview)**.  
2. Select the **Message** tab.  
3. Find your message in the table and scroll to the end of the row.   
3. Select the (**...**) context menu > **Cancel**.   

## Delete organizational message  
Delete an organizational message from Microsoft Intune. Deleted messages are removed from your inventory and are no longer visible in the admin center. You can delete a message anytime, regardless of its status. This action is permanent and can't be undone.  

Intune automatically cancels active messages after you delete them, and stops the delivery of future messages. Messages that were delivered and cached prior to deletion could still appear to users.   

This action requires the *Organizational Messages/Delete* permission. If you're not using one of the built-in Intune roles for organizational messages, be sure to assign the delete permission to the custom admin roles in your tenant that need it.  

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Go to **Tenant administration** > **Organizational messages (preview)**.  
2. Select the **Message** tab.  
3. Find your message in the table and scroll to the end of the row.   
3. Select the (**...**) context menu > **Delete**.   

For frequently asked questions, known issues, and limitations, see [Overview of organizational messages](organizational-messages-overview.md).  


