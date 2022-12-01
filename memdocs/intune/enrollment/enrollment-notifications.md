---
# required metadata

title: Set up enrollment notifications in Intune
titleSuffix: Microsoft Intune
description: Set up enrollment notifications in Intune for employees or students. 
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/01/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: maholdaa  
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure 
ms.collection: M365-identity-device-management
---

# Set up enrollment notifications   

> [!IMPORTANT]
> This feature is in public preview. For more information, see [Public preview in Microsoft Intune](../fundamentals/public-preview.md).  

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Set up enrollment notifications in Microsoft Intune to notify employees of newly enrolled devices. You can create a custom message for employees and include information in the notification about how to report an unrecognized device. 

Intune delivers enrollment notifications via email or push notification. You can apply your tenant's branding and customization settings to email notifications. 

Enrollment notifications work on devices running:  

* Android  
* iOS/iPadOS
* macOS 
* Windows 10/11 

This article describes how to create enrollment notifications in the Microsoft Endpoint Manager admin center.  

## Example  
The following example image shows what an enrollment notification looks like to a device user.  

> [!div class="mx-imgBorder"] 
> ![Example image of an enrollment notification configured in Intune, notifying the recipient that a device named *Nia's iPhone" was enrolled, and includes HTML elements such as bolded font and a hyperlink, device details, contact information, and privacy statement.](./media/enrollment-notifications/enrollment-notification-message.png)  

## Prerequisites  
To create an enrollment notification, you must: 

* Be a Global Administrator or Intune Administrator. 
* [Configure branding and customization settings](../apps/company-portal-app.md) in **Tenant administration** > **Customization**.  

Enrollment notifications only work with user-driven enrollment methods.   

## You should know  
Email notifications appear in the user's inbox. Push notifications appear in the Intune Company Portal apps for iOS/iPadOS, macOS, and Android.  Enrollment push notifications aren't supported in the Company Portal for Windows, so they'll never appear there.  

## Create an enrollment notification  

> [!TIP]
> Use the built-in HTML editor to format and style email notifications. Intune supports the following HTML tags: `<a>`, `<strong>`, `<b>`, `<u>`, `<ol>`, `<ul>`, `<li>`, `<p>`, `<br>`, `<code>`, `<table>`, `<tbody>`, `<tr>`, `<td>`, `<thead>`, and`<th>`. It also supports the `href` attribute for hyperlinks.  

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. Go to **Devices** > **Enroll device** and select the platform you're creating notifications for. Your options:  
   * **Windows enrollment**  
   * **Apple enrollment**  
   * **Android enrollment**    
3. Select **Enrollment notifications (preview)**.  
4. Select **Create notification**. For Apple and Android notifications, select the OS platform you're configuring the notifications for. 

    Your options for Apple enrollment are:  
      * **iOS Notifications**  
      * **macOS Notifications**  

   Your options for Android enrollment are:  
      * **Android Enterprise Notifications**  
      * **Android device administrator Notifications**  
5. In **Basics**, configure the following settings:  
    * **Name**: Enter a descriptive name for the notification. Name your notifications so you can easily identify them later.  
    * **Description**: Enter a description for the notification. This setting is optional, but recommended.  
6. Select **Next**.  
7. In **Notification settings**, configure the notification messages. 

    The options for push notifications are:  
    * **Send Push Notification**: Flip the switch **On** to enable and create a push notification.
    * **Subject**: Enter the subject of the enrollment notification.  
    * **Message**: Enter your message, explaining the purpose of the notification. The character limit is 2000.  

    The options for email notifications are:  
      * **Send Email Notification**: Flip the switch **On** to enable and create an email notification.   
      * **Subject**: Enter the subject of the enrollment notification.  
      * **Message**: Enter your message. The character limit is 2000.  
      * **Raw HTML editor**: Flip the switch **On** to enable HTML formatting.  

    The options for branding and customization are:  

    * **Show company logo**: Flip the switch **On** to make your organization's logo visible in the email header. This option becomes available after you've configured Company Portal branding in your tenant.   
    * **Show device details**: Flip the switch **On** to make the following device details visible in the footer of the email:  
         * Device name  
         * Model  
         * OS  
         * OS version  
         * Serial number  
    * **Show company name**: Flip the switch **On** to make your organization's name visible in the footer of the email. The tenant value is automatically populated.  
    * **Show contact information**: Flip the switch **On** to show your organization's contact information. The tenant value is automatically populated.  
    * **Show Company portal website link**: Flip the switch **On** to show a link to the Company Portal website. The tenant value is automatically populated. 
8. Select **Next**. 
9. Optionally, assign a scope tag, like `US-NC IT Team` or `JohnGlenn_ITDepartment`, to limit management of the notification to specific IT groups. Then select **Next**.  
10. In **Assignments**, select the users or groups receiving the notification. 
11. Select **Next**. 
12. In **Review + create**, review the notification details, and then select **Create**.  

Enrollment notifications are sent out to assigned groups when enrollment is triggered. Return to **Enrollment notifications (preview)** to view and edit notifications, or change priority level. 
