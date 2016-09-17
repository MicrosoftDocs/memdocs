---
title: "Deploy Wi-Fi profiles | System Center Configuration Manager"
ms.custom: na
ms.date: 2015-12-08
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: 
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3753608d-b539-44dc-8e3f-b631319e7687
caps.latest.revision: 5
author: Nbigman
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
# How to deploy Wi-Fi profiles in System Center Configuration Manager
Wi-Fi profiles in System Center Configuration Manager must be deployed to one or more collections before they can be used.  
  
 Use the **Deploy Wi-Fi Profile** dialog box to configure the deployment of Wi-Fi profiles. As part of the configuration, you define the collection to which the Wi-Fi profile is to be deployed and specify how often the Wi-Fi profile is evaluated for compliance.  
  
> [!NOTE]  
>  If you deploy multiple company resource access profiles to the same user, the following behavior occurs:  
>   
>  -   If a conflicting setting contains an optional value, it will not be sent to the device.  
> -   If a conflicting setting contains a mandatory value, the default value will be sent to the device. If there is no default value, the entire company resource access profile will fail.  
  
> [!NOTE]  
>  When a Wi-Fi profile deployment is removed, the Wi-Fi profile is not removed from client devices. If you want to remove the profile from devices, you must manually remove it.  
  
## Deploying Wi-Fi profiles  
  
#### To deploy a Wi-Fi profile  
  
1.  In the System Center Configuration Manager console, click **Assets and Compliance**.  
  
2.  In the **Assets and Compliance** workspace, expand **Compliance Settings**, expand **Company Resource Access**, and then click **Wi-Fi Profiles**.  
  
3.  In the **Wi-Fi Profiles** list, select the Wi-Fi profile that you want to deploy, and then in the **Home** tab, in the **Deployment** group, click **Deploy**.  
  
4.  In the **Deploy Wi-Fi Profile** dialog box, specify the following information:  
  
    -   **Collection** - Click **Browse** to select the collection where you want to deploy the Wi-Fi profile.  
  
    -   **Generate an alert** - Enable this option to configure an alert that is generated if the Wi-Fi profile compliance is less than a specified percentage by a specified date and time. You can also specify whether you want an alert to be sent to System Center Operations Manager.  
  
    -   **Specify the compliance evaluation schedule for this Wi-Fi profile** - Specify the schedule by which the deployed Wi-Fi profile is evaluated on client computers. The schedule can be either a simple or a custom schedule.  
  
        > [!NOTE]  
        >  The profile is evaluated by client computers when the user logs on.  
  
5.  Click **OK** to close the **Deploy Wi-Fi Profile** dialog box and to create the deployment. For more information about how to monitor the deployment, see [How to monitor Wi-Fi profiles in System Center Configuration Manager](../../protect/deploy-use/monitor-wifi-profiles.md) .  
  
## See Also  
 [Operations and maintenance for Wi-Fi Profiles in System Center Configuration Manager](../Topic/Operations%20and%20maintenance%20for%20Wi-Fi%20Profiles%20in%20System%20Center%20Configuration%20Manager.md)