---
title: "How to deploy email profiles in System Center Configuration Manager"
ms.custom: na
ms.date: 2015-12-08
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: 
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c976916e-2f0d-471d-ae19-721de9bbacfa
caps.latest.revision: 4
caps.handback.revision: 0
author: Nbigman

---
# How to deploy email profiles in System Center Configuration Manager
Email profiles in System Center Configuration Manager must be deployed to one or more collections of users or devices before they can be used.  
  
 Use the **Deploy Exchange ActiveSync Profile** dialog box to configure the deployment of email profiles. As part of the configuration, you define the collection to which the email profile is to be deployed and specify how often the email profile is evaluated for compliance.  
  
> [!NOTE]  
>  If you deploy multiple company resource access profiles to the same user, the following behavior occurs:  
>   
>  -   If a conflicting setting contains an optional value, it will not be sent to the device.  
> -   If a conflicting setting contains a mandatory value, the default value will be sent to the device. If there is no default value, the entire company resource access profile will fail.  
>   
>  For example, if you deploy two email profiles to the same user and the values specified for **Exchange ActiveSync host** or **Email address** are different, then both email profiles will fail as they are mandatory settings.  
  
## Deploying email profiles  
  
#### To deploy an email profile  
  
1.  In the System Center Configuration Manager console, click **Assets and Compliance**.  
  
2.  In the **Assets and Compliance** workspace, expand **Compliance Settings**, expand **Company Resource Access**, and then click **Email Profiles**.  
  
3.  In the **Email Profiles** list, select the email profile that you want to deploy, and then in the **Home** tab, in the **Deployment** group, click **Deploy**.  
  
4.  In the **Deploy Exchange ActiveSync Profile** dialog box, specify the following information:  
  
    -   **Collection** - Click **Browse** to select the collection where you want to deploy the email profile.  
  
    -   **Generate an alert** - Enable this option to configure an alert that is generated if the email profile compliance is less than a specified percentage by a specified date and time. You can also specify whether you want an alert to be sent to System Center Operations Manager.  
  
    -   **Specify the compliance evaluation schedule for this Exchange ActiveSync profile** - Specify the schedule by which the deployed email profile is evaluated on client computers. The schedule can be either a simple or a custom schedule.  
  
    > [!NOTE]  
    >  The profile is evaluated by client computers when the user logs on.  
  
5.  Click **OK** to close the **Deploy Exchange ActiveSync Profile** dialog box and to create the deployment. For more information about how to monitor the deployment, see [How to monitor email profiles in System Center Configuration Manager](../../protect/deploy-use/monitor-email-profiles.md).  
  
## See Also  
 [Operations and maintenance for email profiles in System Center Configuration Manager](../Topic/Operations%20and%20maintenance%20for%20email%20profiles%20in%20System%20Center%20Configuration%20Manager.md)