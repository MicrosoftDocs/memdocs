---
# required metadata
title: Create organizational messages | Microsoft Intune  
description: Create and manage organizational messages in the Microsoft Intune admin center.       
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 03/03/2023
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

# Create organizational messages  

*Applies to Windows 11*  

> [!IMPORTANT]
> This feature is in public preview. For more information, see [Public preview in Microsoft Intune](../fundamentals/public-preview.md).  

Create, edit, and monitor [organizational messages](organizational-messages-overview.md) in the Microsoft Intune admin center. You can send important messages and call-to-actions to employees on Windows 11 devices managed by Microsoft Intune. 

This article describes how to create the following types of organizational messages: 

 * Taskbar messages  
 * Notification area messages  
 * Get Started app messages  

## Before you create a message   
Complete these steps before creating a message.  
1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Go to  **Tenant administration** > **Organizational messages (preview)**. 
3. Spend some time in the **Overview** tab to learn about messaging options and prerequisites. 

For more information about the steps you need to take before you create a message, see [Prerequisites](organizational-messages-prerequisites.md).   

## Step 1: Create a message  

# [Taskbar](#tab/taskbar)  
Create and configure a message for the taskbar area.  
1. Go to the **Message** tab and select **Create**.  
2. For **Message type**, select **Taskbar**.   
3. For **Message theme**, select **Mandatory update**. This type of message prompts employees to install a mandatory update.   
4. Select **OK**.  
5. On the **Message** page, select **Add a logo**, and then choose an image file. For requirements, see [Logo requirements](organizational-messages-prerequisites.md#logo-requirements).  
6. (Optional) **Provide a link for the message**: To include a URL link in your message:  
   1. Enter your custom URL. Example: `www.contoso.com/SoftwareUpdate`     
   2. Select the full generated link to make sure it works.     
7. **Choose language to preview**: Select a language to preview the localized version of your message. The message is shown to employees in the [display language](https://support.microsoft.com/windows/manage-the-input-and-display-language-settings-in-windows-12a10cb4-8626-9b77-0ccb-5013e0c7c7a2) they've selected on their device. Organizational messages are supported in 15 languages. If the employee's preferred language isn't supported, the message will appear in their preferred fallback language.  
8. **Preview the message in dark theme**: Turn on the toggle to view how your message appears in dark theme. Check to make sure your logo shows up correctly in both light and dark theme.  
9. Select **Next: Schedule** to continue to scheduling options. 

# [Notification area](#tab/notification)  
Create and configure a message for the notification area.  
1. Go to the **Message** tab and select **Create**.  
2. For **Message type**, select **Notification area**.   
3. For **Message theme**, select the type of message you want to create. Your options:  

      * **Organizational HR training**: Prompt users to complete  HR training.   
     * **Organizational skills training**: Prompt users to complete skill-specific training. 
     * **Organizational training**: Prompt users to complete training provided by your organization.     
     * **Organizational update**: Prompt users to install an update from your organization.  
     * **Update browser**: Prompt users to update their browser.  
     * **Update device**: Prompt users to update their device.  

3. Select **OK**.  
4. On the **Message** page, select **Add a logo**, and then choose an image file. For requirements, see [Logo requirements](organizational-messages-prerequisites.md#logo-requirements).  
5. (Optional) **Provide a link for the message**: To include a URL link in your message:  
    1. Enter your custom URL. Example: `www.contoso.com/SoftwareUpdate`     
    2. Select the full generated link to make sure it works.  
6. **Choose language to preview**: Select a language to preview the localized version of your message. The message is shown to employees in the [display language](https://support.microsoft.com/windows/manage-the-input-and-display-language-settings-in-windows-12a10cb4-8626-9b77-0ccb-5013e0c7c7a2) they've selected on their device. Organizational messages are supported in 15 languages. If the employee's preferred language isn't supported, the message will appear in their preferred fallback language.  
7. **Preview the message in dark theme**: Turn on the toggle to view how your message appears in dark theme. Check to make sure your logo shows up correctly in both light and dark theme.   
8. Select **Next: Schedule** to continue to scheduling options.   

# [Get Started app](#tab/get-started)     
Create and configure a message for the Get Started app.  
1. Go to the **Message** tab and select **Create**.  
2. For **Message type**, select **Get Started app**.   
3. Select **OK**.  
4. On the **Message** page, select **Add a logo**, and then choose an image file. For requirements, see [Logo requirements](organizational-messages-prerequisites.md#logo-requirements).     
5. Choose **Select messages**. You must select two messages to show to users.   
     1. Select **Add your first message**. 
     2. Choose a theme for your message. Options include: 
        * **Review benefits**
        * **Review organization**
        * **Get started with device**
     3. **Provide a link for the message**: To include a URL link in your message:  
          1. Enter your custom URL. Example: `www.contoso.com/SoftwareUpdate`     
          2. Select the full generated link to make sure it works.     
     4. Select **OK**.  
     5. Select **Add your second message**. Options include: 
        * **Organizational training**
        * **Organization policies**
        * **Help resources**
        * **Update VPN**  
     6. Provide a link for the message like you did for the first one. Select the generated link to make sure it works. 
     7. Select **OK**.  
6. **Choose language to preview**: Select a language to preview the localized version of your message. The message is shown to employees in the [display language](https://support.microsoft.com/windows/manage-the-input-and-display-language-settings-in-windows-12a10cb4-8626-9b77-0ccb-5013e0c7c7a2) they've selected on their device. Organizational messages are supported in 15 languages. If the employee's preferred language isn't supported, the message will be shown to them in their preferred fallback language.  
7. **Preview the message in dark theme**: Turn on the toggle to view how your message appears in dark theme. Check to make sure your logo shows up correctly in both light and dark theme.   
8. Select **Next: Schedule** to continue to scheduling options.   
---  
## Step 2: Schedule a message  

# [Taskbar / Notification area](#tab/taskbar+notification) 
On the **Schedule** page, schedule the delivery of your message.  
1. Configure the delivery time window. Your options:  

   * **First day to show message**: Select when to first show the message. To ensure that delivery begins when you want it to, configure this setting 24 hours before you want the message to appear.   
   * **Last day to show message**:  Select the last day to show the message. This date must be at least 7 days after the start date.   
2. Select **Next: Assignments** to continue to assignment options.   

# [Get Started app](#tab/get-started)  
On the **Schedule** page, schedule the delivery of your message. 

1. Configure the **Message repeat frequency**. Select how often you want the message to reappear after employees dismiss it. The message will initially go away when the employee dismisses it or completes the call-to-action, but will reappear at the frequency you select here. Your options: 
   * **Once a week**
   * **Once every two weeks**
   * **Once a month**  
2. Turn on the **Always on** toggle to make messages visible in the Get Started app.  
3. Select **Next: Assignments** to continue to assignment options.     
---  
## Step 3: Assign message  
Assign the message to Azure AD-registered users in your organization. You can only assign messages to Azure AD user groups, not Azure AD device groups. If a group includes both users and devices, Intune will only send the message to the users. 

1. To include groups in the assignment, you have two options:    
   * **Add groups**: Select this option to individually choose from a list of Azure AD groups.  
   * **Include all users**: Select the option to assign the message to all Azure AD-registered users.  
2. If needed, exclude Azure AD groups from the assignment. Under **Exclude**, select **Add groups** and choose the Azure AD groups to leave out.  
3. Select **Next: Review + Create** to review and finalize your message.  

## Step 4: Review and create message  
Review your message, scheduling details, and assignments before creating your message. When you're ready to send the message, select **Create**. 

Return to **Organizational messages (preview)** and select the **Message** tab to view and edit your new message.  

## Next steps  
* Monitor and track the status and user engagement details for scheduled organizational messages. For more information, see [View reporting details for organizational messages](organizational-messages-reporting.md).  
* [Cancel an organizational message](organizational-messages-cancel.md) that's no longer needed. 
* For frequently asked questions, known issues, and limitations, see [Overview of organizational messages](organizational-messages-overview.md).  
