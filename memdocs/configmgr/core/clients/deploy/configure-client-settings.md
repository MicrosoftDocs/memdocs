---
title: "Configure client settings"
titleSuffix: "Configuration Manager"
description: "Select client settings in Configuration Manager."
ms.date: 12/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 95e9858a-bad4-4651-9e61-2e31dc5050fa
author: aczechowski
ms.author: aaroncz
manager: dougeby


---
# How to configure client settings in Configuration Manager

*Applies to: Configuration Manager (current branch)*

You manage all client settings in Configuration Manager from  **Administration** > **Client Settings**. Modify the default settings when you want to configure settings for all users and devices in the hierarchy that do not have any custom settings applied. If you want to apply different settings to just some users or devices, create custom settings and deploy to collections.  

For information about each client setting, see [About client settings](../../../core/clients/deploy/about-client-settings.md).

> [!NOTE]  
>  You can also use configuration items to manage clients to assess, track, and remediate the configuration compliance of devices. For more information, see [Ensure device compliance with Configuration Manager](../../../compliance/understand/ensure-device-compliance.md).  

##  Configure the default client settings    

1. In the Configuration Manager console, choose **Administration** > **Client Settings** > **Default Client Settings**.  

2. On the **Home** tab, choose **Properties**.  

3. View and configure the client settings for each group of settings in the navigation pane.  

   Client computers will be configured with these settings when they next download client policy. To initiate policy retrieval for a single client, see [Initiate Policy Retrieval for a Configuration Manager Client](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval) in [How to manage clients](../../../core/clients/manage/manage-clients.md).  

##  Create and deploy custom client settings  
When you deploy these custom settings, they override the default client settings. Before you begin this procedure, ensure that you have a collection that contains the users or devices that require these custom client settings.  

1. In the Configuration Manager console, choose **Administration** > **Client Settings**.  

2. On the **Home** tab, in the **Create** group, choose **Create Custom Client Settings**, and then choose either:  

   -   **Create Custom Client Device Settings**  

   -   **Create Custom Client User Settings**  

3. Specify a unique name and option description.  

4. Select one or more of the check boxes that display a group of settings.  

5. Choose each group of  settings from the navigation pane, and configure the available settings, then click **OK**.   

6. Select the custom client setting that you created. On the **Home** tab, in the **Client Settings** group, choose **Deploy**.  

7. In the **Select Collection** dialog box, select the appropriate collection, and then choose **OK**. You can verify the selected collection if you click the **Deployments** tab in the details pane.  

8. View the order of the custom client setting that you created. When you have multiple custom client settings, they are applied according to their order number. If there are any conflicts, the setting that has the lowest order number overrides the other settings. To change the order number, on the **Home** tab, in the **Client Settings** group, choose **Move Item Up** or **Move Item Down**.  

   Client computers will be configured with these settings when they next download client policy. To initiate policy retrieval for a single client, see [Initiate Policy Retrieval for a Configuration Manager Client](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval) in [How to manage clients](../../../core/clients/manage/manage-clients.md).  



##  View client settings  
 When you deploy multiple client settings to the same device, user, or user group, the prioritization and combination of settings is complex. To view the client settings:  

1.  In the Configuration Manager console, choose **Assets and Compliance** > **Devices** > **Users** or **User Collections**.  

3.  Select a device, user, or user group and in the **Client Settings** group, select **Resultant Client Settings**.  

4.  Select a client setting from the left pane, and the settings are displayed. In this view, the settings are read-only. 

    > [!NOTE]  
    >  To view the client settings, you must have read access to Client Settings.  

    
