---
title: "How users enroll devices with On-premises MDM "
titleSuffix: "Configuration Manager"
description: "Understand how users enroll devices with On-premises Mobile Device Management in System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 59004b34-b64f-4d77-898c-07bf3dc75430
caps.latest.revision: 9
caps.handback.revision: 0
author: dougeby
ms.author: dougeby
manager: angrobe

---
# How users enroll devices with On-premises Mobile Device Management in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

With System Center Configuration Manager On-premises Mobile Device Management, users can enroll devices if they have been granted enrollment permission (by way of updated client settings), and their devices have the required root certificate installed to have trusted communications with the servers hosting the required site system roles. For more information on how to set up enrollment, see [Set up device enrollment for On-premises Mobile Device Management in System Center Configuration Manager](../../mdm/get-started/set-up-device-enrollment-on-premises-mdm.md).  

> [!NOTE]  
>  The current branch of Configuration Manager supports enrollment in On-premises Mobile Device Management for devices running the following operating systems:  
>   
> -  Windows 10 Enterprise  
> -   Windows 10 Pro  
> -   Windows 10 Team \(beginning in Configuration Manager version 1602\)  
> -   Windows 10 Mobile  
> -   Windows 10 Mobile Enterprise
> -   Windows 10 IoT Enterprise   

The following tasks explain how to enroll and verify enrollment of computers and devices for On\-premises Mobile Device Management:  

-   [Enroll a Windows 10 computer](#bkmk_enrollDesk)  

-   [Enroll a Windows 10 Mobile device](#bkmk_enrollMob)  

-   [Verify device enrollment](#bkmk_verify)  

##  <a name="bkmk_enrollDesk"></a> Enroll a Windows 10 computer  

1.  On a Windows 10 computer, go to **Settings**.  

2.  Click **Accounts**, and then click **Work access**.  

3.  In Work Access under **Connect to work or school**, click **Connect**, enter your work email address, and click **Continue**.  

4.  Enter the FQDN of the server hosting the enrollment proxy point site system role, and click **Continue**.  

5.  In Connecting to a service, enter your work email password, and click **Sign in**.  

6.  Click **Skip** for remembering the sign-in info, and after a short time the device is connected.  

##  <a name="bkmk_enrollMob"></a> Enroll a Windows 10 Mobile device  

1.  On a Windows 10 Mobile device, go to **Settings**.  

2.  Click **Accounts**, and then click **Work access**.  

3.  Click **Connect**.  

4.  Enter your work email address and the FQDN of the server hosting the enrollment proxy point site system role. Click **Connect**.  

5.  On the next screen, enter your work email address and password, and then click **Sign-in**. After a short time,  the device is enrolled. Click **Done**.  

##  <a name="bkmk_verify"></a> Verify device enrollment  
 You can verify that devices have been successfully enrolled in the Configuration Manager console.  

1.  Start the Configuration Manager console.  

2.  Click **Assets and Compliance** > **Overview** > **Devices**. The enrolled device appears in the list.  
