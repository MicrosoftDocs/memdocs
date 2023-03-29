---
# required metadata
title: View reporting details for organizational messages | Microsoft Intune  
description: View the reporting details for existing organizational messages in the Microsoft Intune admin center.          
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 03/20/2023
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

# View reporting details for organizational messages  

*Applies to Windows 11*  

> [!IMPORTANT]
> This feature is in public preview. For more information, see [Public preview in Microsoft Intune](../fundamentals/public-preview.md).  

View the details of your organizational messages in the Microsoft Intune admin center.  

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Go to **Tenant administration** > **Organizational messages (preview)**.
3. Select the **Message** tab to see a list of all existing messages and message details.  

Available details include:  

 * **Message type**: Shows whether the message is for the taskbar, notification area, or Get Started app. Select the hyperlink to see your message, schedule, and assignment settings.    
 * **Message theme**: Shows the theme you chose for the message.     
 * **Date created**:  Shows the date and time you created the message.   
 * **Status** Shows the status of the message, which includes: 
    * **Active**: The message is currently being shown to users according to your schedule.  
    * **Pending**: The message has not been scheduled yet and is currently in progress.
    * **Scheduled**: The message isn't currently being shown to users but has been scheduled.     
    * **Canceled**: The message was canceled and is no longer scheduled to go out to users.  
    * **Completed**: The message was sent out during the scheduled time and is done being shown.  
    * **Failed**: The message failed to schedule due to a service error.  
 * **Start date**: Shows the start date for the message.  
 * **End date** Shows the end date for the message.  
 * **Times shown**: Shows an estimate of the total number of times the message has been shown to users in the past 180 days.   
 * **Times clicked**: Shows an estimate of the total number of times users clicked the message in the past 180 days.   
 * **Click-through rate**: Shows how often, in percentage, that users clicked the message when shown. This data is determined by dividing times clicked by times shown.   

For frequently asked questions, known issues, and limitations, see [Overview of organizational messages](organizational-messages-overview.md).  


