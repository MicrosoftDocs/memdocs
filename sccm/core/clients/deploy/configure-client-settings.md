---
title: "Configure client settings"
description: "Select client settings in System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 95e9858a-bad4-4651-9e61-2e31dc5050fa
caps.latest.revision: 5
author: arob98
ms.author: angrobe
manager: angrobe
---
# How to configure client settings in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

You manage all client settings in System Center Configuration Manager from  **Administration** > **Client Settings**. Modify the default settings when you want to configure settings for all users and devices in the hierarchy that do not have any custom settings applied. If you want to apply different settings to just some users or devices, create custom settings and deploy these to collections.  

For information about each client setting, see [About client settings in System Center Configuration Manager](../../../core/clients/deploy/about-client-settings.md).

> [!NOTE]  
>  You can also use configuration items to manage clients to assess, track, and remediate the configuration compliance of devices. For more information, see [Ensure device compliance with System Center Configuration Manager](../../../compliance/understand/ensure-device-compliance.md).  

##  Configure the default client settings    

1.  In the Configuration Manager console, choose **Administration** > **Client Settings** > **Default Client Settings**.  

3.  On the **Home** tab, choose **Properties**.  

4.  View and configure the client settings for each group of settings in the navigation pane.  

 Client computers will be configured with these settings when they next download client policy. To initiate policy retrieval for a single client, see [Initiate Policy Retrieval for a Configuration Manager Client](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval) in [How to manage clients in System Center Configuration Manager](../../../core/clients/manage/manage-clients.md).  

##  Create and deploy custom client settings  
When you deploy these custom settings, they override the default client settings. Before you begin this procedure, ensure that you have a collection that contains the users or devices that require these custom client settings.  

1.  In the Configuration Manager console, choose **Administration** > **Client Settings**.  

3.  On the **Home** tab, in the **Create** group, choose **Create Custom Client Settings**, and then choose either:  

    -   **Create Custom Client Device Settings**  

    -   **Create Custom Client User Settings**  

4.  Specify a unique name and option description.  

5.  Select one or more of the check boxes that display a group of settings.  

6.  Choose each group of  settings from the navigation pane, and configure the available settings, then click **OK**.   

8.  Select the custom client setting that you created. On the **Home** tab, in the **Client Settings** group, choose **Deploy**.  

9. In the **Select Collection** dialog box, select the appropriate collection, and then choose **OK**. You can verify the selected collection if you click the **Deployments** tab in the details pane.  

10. View the order of the custom client setting that you have just created. When you have multiple custom client settings, they are applied according to their order number. If there are any conflicts, the setting that has the lowest order number overrides the other settings. To change the order number, on the **Home** tab, in the **Client Settings** group, choose **Move Item Up** or **Move Item Down**.  

 Client computers will be configured with these settings when they next download client policy. To initiate policy retrieval for a single client, see [Initiate Policy Retrieval for a Configuration Manager Client](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval) in [How to manage clients in System Center Configuration Manager](../../../core/clients/manage/manage-clients.md).  

##  View client settings  
 When multiple client settings have been deployed to the same device, user, or user group, the prioritization and combination of settings can be complex. To view the client settings:  

1.  In the Configuration Manager console, choose **Assets and Compliance** > **Devices** > **Users** or **User Collections**.  

3.  Select a device, user, or user group and in the **Client Settings** group, select **Resultant Client Settings**.  

4.  Select a client setting from the left pane, and the settings are displayed. In this view, the settings are read-only. 

    > [!NOTE]  
    >  To view the client settings, you must have read access to Client Settings.  

    