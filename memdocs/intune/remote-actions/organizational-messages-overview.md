---
# required metadata
title: Overview of organizational messages in Microsoft Intune | Microsoft Docs
description: Learn more about the features and capabilities of organizational messages.     
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 05/31/2023
ms.topic: conceptual
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

# Organizational messages in Microsoft Intune 

*Applies to Windows 11*   

Use organizational messages to send important messages to employees on Intune-managed Windows 11 devices.  Organizational messages can be used to communicate in remote and hybrid work scenarios and is intended to help employees:  

* Acclimate to new roles.  
* Learn more about their workplace.
* Stay informed of new and required updates and trainings.  

Organizational messages appear in highly visible places in Windows 11, including the Get Started app, notification area, and just above the taskbar. This article provides an overview of organizational messages, with known issues, limitations, and FAQs.  

## How it works   

Microsoft Intune provides you with pre-written messages in templates designed for the taskbar area, notification area, and Get Started app. You can add a custom destination URL in the message to link employees to additional resources or the next step in their onboarding process. You must include a logo so that employees recognize and know the message is from you.  

Messages are assigned to Azure AD users and scheduled in the admin center. After you create a message, you can track the delivery status and user engagement data for it, and cancel the message if it's no longer needed.   

## Message types  
You can create the following types of messages:  

* Taskbar messages: These messages appear just above the desktop taskbar. Taskbar messages are disruptive and good to use when you need to deliver an important notification, like a critical software update. A device user can dismiss the message, but it reappears at the frequency you configure in Intune until they go to the included URL.     

* Notification area messages: These messages appear in the Notification Center. They typically pop up and then disappear, and are good for linking employees to informational resources, such as new and available trainings or optional updates. The message reappears at the frequency you configure in Intune until the user goes to the included URL. The device user's Windows 11 Focus Assist settings may disrupt the visibility of notification area messages. 

* Get Started app messages: These messages appear in the Get Started app. The device user sees this message after they enroll their device, and then open the Get Started app. Use this type of message to welcome new employees and link them to resources like benefits information, essential employee trainings, device tips, policies, and support information. The message keeps showing up at the frequency you configure in Intune until the user goes to the included URL. 

## Prerequisites  
For all tenant, role, and policy requirements for organizational messages see [Prerequisites](organizational-messages-prerequisites.md).    

## Known issues and limitations  

Organizational messages have the following known issues and limitations:  

* Assigning messages to devices and mixed groups isn't supported. If an assigned group includes both users and devices, Intune will only send the message to the users. 
* If you recently onboarded your tenant to Azure AD, it can take 36 to 64 hours before you're able to use the organizational messages feature.
* When you create an organizational message for the Get Started app, Microsoft Intune automatically sets the delivery end date to 12/31/2035, which is shown in the profile summary. The message will be delivered to targeted groups until that date or until you cancel the message.  
* Message priority isn't supported. If you schedule multiple messages of the same type for the same time window, targeted employees will receive the messages in a random order.  
* We observed that sometimes after admins create a message and receive a success confirmation, a background task fails and limits functionality. The failure isn't communicated in the UI, and the status for the message still appears as **Scheduled**. You'll know this happened if the cancellation option and user engagement details are unavailable. 

## Frequently asked questions    
This section answers frequently asked questions (FAQ) for organizational messages.  

### Can I customize message text? 
No, we'll generate the message based on the theme you select. You can add a custom URL to the message to link people to more detailed information.   

### What do I need to do if I don’t have the correct permissions?  
Contact someone in your organization who is an Azure AD Global Administrator, Intune Administrator, or Intune Role Administrator and ask them to assign one of the following roles:  
 * Azure AD Global Administrator 
 * Intune Administrator 
 * Organizational messages manager (Microsoft Intune role) 
 * Organizational messages writer (Azure AD role)  

### Why do I need to update other policies before I create a message?  
The required policies described in [Prerequisites](organizational-messages-prerequisites.md) control access to the taskbar, notification area, and Get Started app. If the settings are blocked or not configured as described, employees will not receive the messages.   

### Can I control the order in which messages are delivered? 
You can schedule messages to arrive at different times on a device by selecting a unique delivery window for each message. If you schedule the same time for multiple messages, the messages will arrive in random order.  

### Where can I share an idea for organizational messages or suggest an improvement?  
In the Microsoft Intune admin center, select the **Feedback** icon that's next to your account name at the top of the page. Rate your experience and then describe your experience or idea. If you're okay with getting a response from Microsoft, select **Microsoft can email you about your feedback.**  

For other support options, see [How to get support in Microsoft Intune admin center](/mem/get-support).  

## Next steps  
Complete the [prerequisites for organizational messages](organizational-messages-prerequisites.md) to enable the feature in your tenant.     
