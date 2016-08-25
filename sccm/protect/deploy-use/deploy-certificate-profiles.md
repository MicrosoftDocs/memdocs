---
title: "How to deploy certificate profiles in System Center Configuration Manager"
ms.custom: na
ms.date: 2015-12-08
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: 
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1ecfe2c6-45bc-4d8a-a7f6-53525c958e0f
caps.latest.revision: 7
caps.handback.revision: 0
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
# How to deploy certificate profiles in System Center Configuration Manager
To deploy certificates to users or devices in System Center Configuration Manager, you must deploy certificate profiles to one or more collections of users or devices.  
  
 You can deploy trusted certification authority (CA) certificates, and user or device certificates. Before you deploy a user or device certificate, check whether the device has installed the trusted root CA certificate for those certificates. If the device does not have the trusted root certificate, perhaps because it is not a domain member or is from an untrusted forest, you must deploy the root CA certificate to the device in addition to deploying the user or device certificate.  
  
 Use the **Deploy Certificate Profile** dialog box to configure the deployment of certificate profiles. This configuration includes defining the collection to which the certificate profile will be deployed and specifying how often the certificate profile is evaluated for compliance.  
  
> [!NOTE]  
>  If you deploy multiple company resource access profiles to the same user or device, the following behavior occurs:  
>   
>  -   If a conflicting setting contains an optional value, it will not be sent to the device.  
> -   If a conflicting setting contains a mandatory value, the default value will be sent to the device. If there is no default value, the entire company resource access profile will fail.  
  
> [!NOTE]  
>  Before you can deploy certificate profiles, you must first configure the infrastructure and create certificate profiles. For more information, see the following topics:  
>   
>  -   [Configuring certificate profiles in System Center Configuration Manager](../../protect/deploy-use/configuring-certificate-profiles.md)  
> -   [How to create certificate profiles in System Center Configuration Manager](../../protect/deploy-use/create-certificate-profiles.md)  
  
### To deploy a certificate profile  
  
1.  In the System Center Configuration Manager console, click **Assets and Compliance**.  
  
2.  In the **Assets and Compliance** workspace, expand **Compliance Settings**, expand **Company Resource Access**, and then click **Certificate Profiles**.  
  
3.  In the **Certificate Profiles** list, select the certificate profile that you want to deploy.  
  
4.  On the **Home** tab, in the **Deployment** group, click **Deploy**.  
  
5.  In the **Deploy Certificate Profile** dialog box, specify the following information:  
  
    -   **Collection**: Click **Browse** to select the user or device collection where you want to deploy the certificate profile.  
  
    -   **Generate an alert**: Enable this option to configure an alert that is generated if the certificate profile compliance is less than a specified percentage by a specified date and time. You can also specify whether you want an alert to be sent to Microsoft System Center Operations Manager.  
  
    -   **Random delay (hours)**: (For certificate profiles that contain Simple Certificate Enrollment Protocol settings only) – Specifies a delay window to avoid excessive processing on the Network Device Enrollment Service. The default value is **64** hours.  
  
    -   **Specify the compliance evaluation schedule for this certificate profile**: Specifies the schedule by which the deployed certificate profile is evaluated on client computers. This can be either a simple schedule or a custom schedule.  
  
        > [!NOTE]  
        >  The profile is evaluated on client computers when the users log on.  
  
6.  Click **OK** to close the **Deploy Certificate Profile** dialog box and to create the deployment. For more information about how to monitor the deployment, see [How to monitor certificate profiles in System Center Configuration Manager](../../protect/deploy-use/monitor-certificate-profiles.md).  
  
## See Also  
 [Operations and maintenance for certificate profiles in System Center Configuration Manager](../Topic/Operations%20and%20maintenance%20for%20certificate%20profiles%20in%20System%20Center%20Configuration%20Manager.md)