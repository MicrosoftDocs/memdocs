---
title: Configure remote control
titleSuffix: Configuration Manager
description: Set up remote control in Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
author: mestew
ms.author: mstewart
manager: dougeby
ms.localizationpriority: medium
---
# Configuring remote control in Configuration Manager

*Applies to: Configuration Manager (current branch)*

 This procedure describes configuring the default client settings for remote control. These settings apply to all computers in your hierarchy. If you want these settings to apply to only some computers, assign a custom device client setting to a collection that contains those computers. For more information a see [How to configure client settings](../../../../core/clients/deploy/configure-client-settings.md). 

To use Remote Assistance or Remote Desktop, it must be installed and configured on the computer that runs the Configuration Manager console. For more information about how to install and configure Remote Assistance or Remote Desktop, see your Windows documentation.  

#### To enable remote control and configure client settings  

1. In the Configuration Manager console, choose **Administration** > **Client Settings** > **Default Client Settings**.  

2. On the **Home** tab, in the **Properties** group, choose **Properties**.  

3. In the **Default**  dialog box, choose **Remote Tools**.  

4. Configure the remote control, Remote Assistance and Remote Desktop client settings. For a list of remote tools client settings that you can configure, see [Remote Tools](../../../../core/clients/deploy/about-client-settings.md#remote-tools).  

   You can change the company name that appears in the **ConfigMgr Remote Control** dialog box by configuring a value for **Organization name displayed in Software Center** in the **Computer Agent** client settings.  

   Client computers are configured with these settings the next time they download client policy. To initiate policy retrieval for a single client, see [How to manage clients](../../../../core/clients/manage/manage-clients.md).  

#### Enable keyboard translation

By default, Configuration Manager transmits the key position from the viewer's location to the sharer's location. This can present a problem for keyboard configurations that differ from viewer to sharer. For example, a viewer with an English keyboard would type an "A", but the sharer's French keyboard would provide a "Q". You now have the option of configuring remote control so that the character itself is transmitted from the viewer's keyboard to the sharer, and what the viewer intends to type arrives at the sharer.

To turn on keyboard translation, in **Configuration Manager Remote Control**, choose **Action**,and choose **Enable keyboard translation** to transmit key position.

> [!NOTE]
>
> Special keys, such as ~!#@$%, will not be translated correctly.


## Keyboard shortcuts for the remote control viewer

|Keyboard shortcut|Description|  
|-----------------------|-----------------|  
|Alt+Page Up|Switches between running programs from left to right.|  
|Alt+Page Down|Switches between running programs from right to left.|  
|Alt+Insert|Cycles through running programs in the order that they were opened.|  
|Alt+Home|Displays the **Start** menu.|  
|Ctrl+Alt+End|Displays the Windows Security dialog box (Ctrl+Alt+Del).|  
|Alt+Delete|Displays the Windows menu.|  
|Ctrl+Alt+Minus Sign (on the numeric keypad)|Copies the active window of the local computer to the remote computer Clipboard.|  
|Ctrl+Alt+Plus Sign (on the numeric keypad)|Copies the entire local computer's window area to the remote computer Clipboard.|  
