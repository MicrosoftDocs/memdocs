---
title: "Deploy Wi-Fi, VPN, email, and certificate profiles"
titleSuffix: "Configuration Manager"
description: "Learn how to deploy Wi-Fi, VPN, email, and certificate profiles in System Center Configuration Manager."
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 3753608d-b539-44dc-8e3f-b631319e7687
author: aczechowski
manager: dougeby
ms.author: aaroncz
---
# Deploy profiles in System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
Profiles must be deployed to one or more collections before they can be used.  

 Use the **Deploy Wi-Fi Profile**, **Deploy VPN Profile**, **Deploy Exchange ActiveSync Profile**, or **Deploy Certificate Profile** dialog box to configure the deployment of these profiles. As part of the configuration, you define the collection to which the  profile is to be deployed and specify how often the profile is evaluated for compliance.  

> [!NOTE]  
>  If you deploy multiple company resource access profiles to the same user, the following behavior occurs:  
>   
>  -   If a conflicting setting contains an optional value, it will not be sent to the device.  
> -   If a conflicting setting contains a mandatory value, the default value will be sent to the device. If there is no default value, the entire company resource access profile will fail. For example, if you deploy two email profiles to the same user and the values specified for **Exchange ActiveSync host** or **Email address** are different, then both email profiles will fail as they are mandatory settings.  

> -   Before you can deploy certificate profiles, you must first configure the infrastructure and create certificate profiles. For more information, see the following topics:  
>   
>  -   [Configuring certificate infrastructure in System Center Configuration Manager](certificate-infrastructure.md)  
> -   [How to create certificate profiles in System Center Configuration Manager](create-certificate-profiles.md)    

> [!IMPORTANT]  
>  When a VPN profile deployment is removed, it is not removed from client devices. If you want to remove the profile from devices, you must manually remove it.
>   

## Deploying  profiles  


1.  In the System Center Configuration Manager console, choose **Assets and Compliance**.  

2.  In the **Assets and Compliance** workspace, expand **Compliance Settings**, expand **Company Resource Access**, and then choose the appropriate profile type, such as **Wi-Fi Profiles**.  

3.  In the list of profiles, select the profile that you want to deploy, and then in the **Home** tab, in the **Deployment** group, click **Deploy**.  

4.  In the deploy profile dialog box, specify the following information:  

    -   **Collection** - Click **Browse** to select the collection where you want to deploy the profile.  

    -   **Generate an alert** - Enable this option to configure an alert that is generated if the profile compliance is less than a specified percentage by a specified date and time. You can also specify whether you want an alert to be sent to System Center Operations Manager.  

	-   -   **Random delay (hours)**: (Only for certificate profiles that contain Simple Certificate Enrollment Protocol settings) Specifies a delay window to avoid excessive processing on the Network Device Enrollment Service. The default value is **64** hours.  

    -   **Specify the compliance evaluation schedule for this <type> profile** - Specify the schedule by which the deployed profile is evaluated on client computers. The schedule can be either a simple or a custom schedule.  

        > [!NOTE]  
        >  The profile is evaluated by client computers when the user logs on.  

5.  Click **OK** to close the dialog box and to create the deployment.

### See also  

[How to monitor Wi-Fi, VPN, and email profiles in System Center Configuration Manager](monitor-wifi-email-vpn-profiles.md)

[How to monitor certificate profiles in System Center Configuration Manager](monitor-certificate-profiles.md)
