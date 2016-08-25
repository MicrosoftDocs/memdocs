---
title: "Working with user data and profiles configuration items in System Center Configuration Manager"
ms.custom: na
ms.date: 2015-12-08
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: 
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a9439076-6a27-4361-a544-49bbfe7abc8a
caps.latest.revision: 6
author: robstackmsft
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
# Working with user data and profiles configuration items in System Center Configuration Manager
User data and profiles configuration items in System Center Configuration Manager contain settings that can manage folder redirection, offline files and roaming profiles on computers that run Windows 8 for users in your hierarchy. For example, you can:  
  
-   Redirect a user’s Documents folder to a network share.  
  
-   Ensure that specified files stored on the network are available on a user’s computer when the network connection is unavailable.  
  
-   Configure which files in a user’s roaming profile are synchronized with a network share when the user logs on and off.  
  
 Unlike other configuration items in Configuration Manager, you do not add user data and profile configuration items to a configuration baseline which you then deploy. Instead, you deploy the configuration item directly by using the **Deploy User Data and Profiles Configuration Item** dialog box.  
  
> [!IMPORTANT]  
>  You can only deploy user data and profiles configuration items to user collections.  
  
## Enable user data and profiles for compliance settings  
 Use the following procedure to configure the default client setting for user data and profiles compliance settings which will apply to all computers in your hierarchy. If you want this setting to apply to only some computers, create a custom device client setting and assign it to a collection that contains the computers for which you want to use user data and profiles compliance settings. For more information about how to create custom device settings, see [How to configure client settings in System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md).  
  
#### How to enable user data and profiles for compliance settings  
  
1.  In the Configuration Manager console, click **Administration**.  
  
2.  In the **Administration** workspace, click **Client Settings**.  
  
3.  Click **Default Settings**.  
  
4.  On the **Home** tab, in the **Properties** group, click **Properties**.  
  
5.  In the **Default Settings** dialog box, click **Compliance Settings**.  
  
6.  From the **Enable User Data and Profiles** drop-down list, select **Yes**.  
  
7.  Click **OK** to close the **Default Settings** dialog box.  
  
## Next steps  
 Next, you'll likely want to start to create and deploy user data and profiles configuration items.  
  
 For help with all settings you can use, see [How to create user data and profiles configuration items in System Center Configuration Manager](../../compliance/deploy-use/create-user-data-and-profiles-configuration-items.md).  
  
## See Also  
 [Ensure device compliance with System Center Configuration Manager](../../compliance/understand/ensure-device-compliance.md)