---
title: "How to configure client settings in System Center Configuration Manager"
ms.custom: na
ms.date: 2015-12-08
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: 
  - configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 95e9858a-bad4-4651-9e61-2e31dc5050fa
caps.latest.revision: 5
author: Mtillman
translation.priority.ht: 
  - cs-cz
  - de-de
  - en-gb
  - es-es
  - fr-fr
  - hu-hu
  - it-it
  - ja-jp
  - ko-kr
  - nl-nl
  - pl-pl
  - pt-br
  - pt-pt
  - ru-ru
  - sv-se
  - tr-tr
  - zh-cn
  - zh-tw
---
# How to configure client settings in System Center Configuration Manager
You manage all client settings in System Center Configuration Manager from the **Client Settings** node in the **Administration** workspace of the Configuration Manager console. Modify the default settings when you want to configure settings for all users and devices in the hierarchy that do not have any custom settings applied. If you want to apply different settings to just some users or devices, create custom settings and deploy these to collections.  
  
> [!NOTE]  
>  You can also use configuration items to manage clients to assess, track, and remediate the configuration compliance of devices. For more information, see [Ensure device compliance with System Center Configuration Manager](../../../compliance/understand/ensure-device-compliance.md).  
  
 Use one of the following procedures to configure client settings:  
  
-   [How to Configure the Default Client Settings](#BKMK_DefaultClientSettings)  
  
-   [How to Create and Deploy Custom Client Settings](#BKMK_CustomClientSettings)  
  
-   [How to View Resultant Client Settings](#BKMK_ResultantClientSettings)  
  
##  <a name="BKMK_DefaultClientSettings"></a> How to Configure the Default Client Settings  
 Use the following procedure to configure the default client settings for all clients in the hierarchy.  
  
#### To configure the default client settings  
  
1.  In the Configuration Manager console, click **Administration**.  
  
2.  In the **Administration** workspace, click **Client Settings**, and then select **Default Client Settings**.  
  
3.  On the **Home** tab, click **Properties**.  
  
4.  View and configure the client settings for each group of settings in the navigation pane. For more information about each setting, see [About client settings in System Center Configuration Manager](../../../core/clients/deploy/about-client-settings.md).  
  
5.  Click **OK** to close the **Default Client Settings** dialog box.  
  
 Client computers will be configured with these settings when they next download client policy. To initiate policy retrieval for a single client, see [Initiate Policy Retrieval for a Configuration Manager Client](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval) in [How to manage clients in System Center Configuration Manager](../../../core/clients/manage/manage-clients.md).  
  
##  <a name="BKMK_CustomClientSettings"></a> How to Create and Deploy Custom Client Settings  
 Use the following procedure to configure and deploy custom settings for a selected collection of users or devices. When you deploy these custom settings, they override the default client settings.  
  
> [!NOTE]  
>  Before you begin this procedure, ensure that you have a collection that contains the users or devices that require these custom client settings.  
  
#### To configure and deploy custom client settings  
  
1.  In the Configuration Manager console, click **Administration**.  
  
2.  In the **Administration** workspace, click **Client Settings**.  
  
3.  On the **Home** tab, in the **Create** group, click **Create Custom Client Settings**, and then click one of the following options depending on whether you want to create custom client settings for devices or for users:  
  
    -   **Create Custom Client Device Settings**  
  
    -   **Create Custom Client User Settings**  
  
4.  In the **Create Custom Device Settings** or **Create Custom User Settings** dialog box, specify a unique name for the custom settings, and an optional description.  
  
5.  Select one or more of the available check boxes that display a group of settings.  
  
6.  Click the first group settings from the navigation pane, and then view and configure the available custom settings. Repeat this process for any remaining group settings. For information about each client setting, see [About client settings in System Center Configuration Manager](../../../core/clients/deploy/about-client-settings.md).  
  
7.  Click **OK** to close the **Create Custom Device Settings** or **Create Custom User Settings** dialog box.  
  
8.  Select the custom client setting that you have just created. On the **Home** tab, in the **Client Settings** group, click **Deploy**.  
  
9. In the **Select Collection** dialog box, select the collection that contains the devices or users to be configured with the custom settings, and then click **OK**. You can verify the selected collection if you click the **Deployments** tab in the details pane.  
  
10. View the order of the custom client setting that you have just created. When you have multiple custom client settings, they are applied according to their order number. If there are any conflicts, the setting that has the lowest order number overrides the other settings. To change the order number, on the **Home** tab, in the **Client Settings** group, click **Move Item Up** or **Move Item Down**.  
  
 Client computers will be configured with these settings when they next download client policy. To initiate policy retrieval for a single client, see see [Initiate Policy Retrieval for a Configuration Manager Client](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval) in [How to manage clients in System Center Configuration Manager](../../../core/clients/manage/manage-clients.md).  
  
##  <a name="BKMK_ResultantClientSettings"></a> How to View Resultant Client Settings  
 When multiple client settings have been deployed to the same device, user, or user group, the prioritization and combination of settings can be complex. Use the following procedure to view the calculated resultant client settings.  
  
#### To view the resultant client settings  
  
1.  In the Configuration Manager console, click **Assets and Compliance**.  
  
2.  In the **Assets and Compliance** workspace, click **Devices**, **Users**, or **User Collections**.  
  
3.  Select a device, user, or user group and in the **Client Settings** group, select **Resultant Client Settings**.  Alternately, you can right click the device, user, or user group, select **Client Settings**, and click **Resultant Client Settings**.  
  
4.  Select a client setting from the left pane, and the resultant settings are displayed.  
  
    > [!NOTE]  
    >  To view the resultant client settings, the logged on user must have read access to Client Settings.  
  
    > [!NOTE]  
    >  The displayed resultant settings are read only. To modify any settings, use the above procedures.  
  
## See Also  
 [Preparation steps for deploying clients in System Center Configuration Manager](../Topic/Preparation%20steps%20for%20deploying%20clients%20in%20System%20Center%20Configuration%20Manager.md)