---
# required metadata
title: Create organizational messages | Microsoft Intune  
description: Learn how to create and manage organizational messages in Microsoft Intune.       
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 11/15/2022
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
ms.collection: M365-identity-device-management
---

# Create organizational messages  

*Applies to Windows 11*  

> [!IMPORTANT]
> This feature is in public preview. For more information, see [Public preview in Microsoft Intune](../fundamentals/public-preview.md).  

Create, edit, and monitor [organizational messages](organizational-messages-overview.md) in the Microsoft Endpoint Manager admin center. You can send important messages and call-to-actions to employees on Windows 11 devices managed by Microsoft Intune. 

This article describes how to create the following types of organizational messages: 

 * Taskbar messages  
 * Notification area messages  
 * Get Started app messages  

## Before you create a message   
In the Microsoft Endpoint Manager admin center, go to  **Tenant administration** > **Organizational messages (preview)**.  Spend some time in the **Overview** tab to learn about messaging options and prerequisites. For more information about the steps you need to take before you create a message, see [Prerequisites](organizational-messages-prerequisites.md). 

If you recently onboarded your tenant to Azure AD, it can take 36 to 64 hours before you're able to use the organizational messages feature.   

## Step 1: Create a message  
Select where you want the message to appear, and its theme.     

1. Go to the **Message** tab and select **Create**.  
2. For **Message type**, select the type of message you want to set up. Your options: 
    *  **Taskbar**  
    *  **Notification area**  
    *  **Get Started app**    
3. For **Message theme**, select the option that best describes the purpose of the message. Themes vary based on the message type you select. If you're setting up a message in the Get Started app, you'll select a theme later.    

    Your options:  
     * **Mandatory update**: Prompt users to install a mandatory update. 
     * **Organizational HR training**: Prompt users to complete  HR training.   
     * **Organizational skills training**: Prompt users to complete skill-specific training. 
     * **Organizational training**: Prompt users to complete training provided by your organization.     
     * **Organizational update**: Prompt users to install an update from your organization.  
     * **Update browser**: Prompt users to update their browser.  
     * **Update device**: Prompt users to update their device.  

3. Select **OK**.  

## Step 2: Configure message content  
On the **Message** page, configure the content for your message. As you enter your information, look at the example message to preview how your message will appear to users.  Options vary by message type. 

*For taskbar and notification area messages:*      

1. **Add a logo**: Choose an image file. For image requirements, see [Logo requirements](organizational-messages-prerequisites.md#logo-requirements).  
2. **Provide a link for the message**: To include a URL link in your message:  
      * Select the domain you want to use. The list contains all Azure AD verified custom domain names in your tenant. Example: `www.contoso.com` 
      * (Optional) Select **Add a link path, if needed** and add the path for your URL. Example: `/SoftwareUpdate`   
      * Select the full generated link to make sure it works. Example: `www.contoso.com/SoftwareUpdate`     
3. **Choose language to preview**: Select a language to preview the localized version of your message. The message is shown to employees in the [display language](https://support.microsoft.com/windows/manage-the-input-and-display-language-settings-in-windows-12a10cb4-8626-9b77-0ccb-5013e0c7c7a2) they've selected on their device. Organizational messages are supported in 15 languages. If the employee's preferred language isn't supported, the message will appear in their preferred fallback language.  
4. **Preview the message in dark theme**: Toggle the switch **On** to view how your message appears in dark theme. Check to make sure your logo shows up correctly in both light and dark theme.  

*For Get Started app messages:*    
1. **Add a logo**: Choose an image file. For image requirements, see [Logo requirements](organizational-messages-prerequisites.md#logo-requirements).     
2. **Select messages**: You must select two messages to show to users.   
     1. Select **Add your first message**. 
     2. Choose a theme for your message. Options include: 
        * **Review benefits**
        * **Review organization**
        * **Get started with device**
     3. **Provide a link for the message**: To include a URL link in your message:
        * Select the domain you want to use. The list contains all Azure AD verified custom domain names in your tenant. Example: `www.contoso.com` 
        * (Optional) Select **Add a link path, if needed** and add the path for your URL. Example: `/SoftwareUpdate`   
        * Select the full generated link to make sure it works. Example: `www.contoso.com/SoftwareUpdate`      
     4. Select **OK**.  
     5. Select **Add your second message**. Options include: 
        * **Organizational training**
        * **Organization policies**
        * **Help resources**
        * **Update VPN**  
     6. Provide a link for the message like you did for the first one. Select the generated link to make sure it works. 
     7. Select **OK**.  
3. **Choose language to preview**: Select a language to preview the localized version of your message. The message is shown to employees in the [display language](https://support.microsoft.com/windows/manage-the-input-and-display-language-settings-in-windows-12a10cb4-8626-9b77-0ccb-5013e0c7c7a2) they've selected on their device. Organizational messages are supported in 15 languages. If the employee's preferred language isn't supported, the message will be shown to them in their preferred fallback language.  
4. **Preview the message in dark theme**: Toggle the switch **On** to view how your message appears in dark theme. Check to make sure your logo shows up correctly in both light and dark theme.   

When you're done configuring the message, select **Next: Schedule** to continue to scheduling options.  

## Step 3: Schedule message  
Schedule the delivery for your message. Settings vary based on message type.    

Your options are:  

* **First day to show message**: Select when to first show the message. To ensure that delivery begins when you want it to, configure this setting 24 hours before you want the message to appear. This option isn't available for the Get Started app.   
* **Last day to show message**:  Select the last day to show the message. This date must be at least 7 days after the start date. This option isn't available for the Get Started app.  
* **Message repeat frequency**: Select how often you want the message to reappear after employees dismiss it. The message will initially go away when the employee dismisses it or completes the call-to-action, but it will reappear at the frequency you select here. Your options: 
    * **Once a week**
    * **Once every two weeks**
    * **Once a month**  

  This option isn't available for the Get Started app.  
 
 * **Always on**: Toggle the switch to **Always on** to make messages visible in the Get Stated app. This option isn't available for messages in the taskbar and notification area.    

When you're done scheduling your message, select **Next: Assignments**.     

## Step 4: Assign message  
Assign the message to Azure AD-registered users in your organization. You can only assign messages to Azure AD user groups, not Azure AD device groups. If a group includes both users and devices, Intune will only send the message to the users. 

To include groups in the assignment, you have two options:    
 * **Add groups**: Select this option to individually choose from a list of Azure AD groups.  
 * **Include all users**: Select the option to assign the message to all Azure AD-registered users.  

You can also exclude Azure AD groups from the assignment. Under **Exclude**, select **Add groups** and choose the Azure AD groups to leave out.  

When you're done assigning groups, select **Next: Review + Create**.   

## Step 5: Review and create message  
Review your message, scheduling details, and assignments before creating your message. When you're ready to send the message, select **Create**.  

## View reporting details    
In the **Messages** tab, you can view a list of all of your messages and see the following details:  

 * **Message type**: Shows whether the message is for the taskbar, notification area, or Get Started app. Select the hyperlink to see your message, schedule, and assignment settings.    
 * **Message theme**: Shows the theme you chose for the message.     
 * **Date created**:  Shows the date and time you created the message.   
 * **Status** Shows the status of the message, which includes: 
    * **Active**: The message is currently being shown to users according to your schedule.  
    * **Scheduled**: The message isn't currently being shown to users but has been scheduled.  
    * **Canceled**: The message was canceled and is no longer scheduled to go out to users.  
    * **Completed**: The message was sent out during the scheduled time and is done being shown.  
 * **Start date**: Shows the start date for the message.  
 * **End date** Shows the end date for the message.  
 * **Times shown**: Shows an estimate of the total number of times the message has been shown to users in the past 180 days.   
 * **Times clicked**: Shows an estimate of the total number of times users clicked the message in the past 180 days.   
 * **Click-through rate**: Shows how often, in percentage, that users clicked the message when shown. This data is determined by dividing times clicked by times shown.  

## Cancel a message  
To cancel a message that's no longer needed:  

1. Go to the **Messages** tab.  
2. Find your message in the table and scroll to the end of the row.   
3. Select the context menu (**...**), and then select **Cancel**.   

## Next steps  
For frequently asked questions, known issues, and limitations, see [Overview of organizational messages](organizational-messages-overview.md).  