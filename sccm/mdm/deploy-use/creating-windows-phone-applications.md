---
title: "Create Windows Phone applications"
description: "See which considerations you must take into account when you create and deploy applications for Windows Phone devices."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 68fe11fa-5fb2-4b81-b0f5-b6f2392fb4ad
caps.latest.revision: 10
author: mattbriggs
ms.author: mabrigg
manager: angrobe

---
# Create Windows Phone applications with System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

A System Center Configuration Manager application has one or more deployment types that comprise the installation files and information that are required to deploy software to a device. A deployment type also has rules that specify when and how the software is deployed.  

 You can create applications by using the following methods:  

-   Automatically create the application and deployment types by reading the application installation files.  

-   Manually create the application and then add deployment types later.  

-   Import an application from a file.  

See [Start the create application wizard](../../apps/deploy-use/create-applications.md#start-the-create-application-wizard) for the steps required to create Configuration Manager applications and deployment types. Also, keep the following considerations in mind when you create and deploy applications for Windows Phone devices.  

## General considerations  
 Configuration Manager supports deploying the following app file types:  

|Device type|Supported file types|  
|-----------------|---------------------|  
|Windows Phone 8|.xap|  
|Windows Phone 8.1|.xap, .appx, .appxbundle|
|Windows 10 Mobile|.xap, .appx, .appxbundle|

 The following deployment actions are supported:  

|Device type|Supported actions|  
|-----------------|-----------------------|  
|Windows Phone 8, Windows Phone 8.1, and Windows 10 Mobile|Available, Required, Uninstall|  

## Steps to deploy the latest Windows Phone company portal app with supersedence  
 The following table provides the steps, details, and more information for creating and deploying the latest Windows Phone 8 company portal app.  

|Step|More information|  
|----------|----------------------|  
|**Step 1:** Get the latest company portal app.|Download the [Windows Phone 8 company portal app](http://go.microsoft.com/fwlink/?LinkId=268440).|  
|**Step 2:** Sign the company portal app with your Symantec certificate.|For information on how to sign the company portal app, see [Set up Windows Phone and Windows 10 Mobile hybrid device management with System Center Configuration Manager and Microsoft Intune](../../mdm/deploy-use/enroll-hybrid-windows.md).|  
|**Step 3:** Create a new application with the latest version of the company portal app, and specify a supersedence relationship.|For more information, see [Create applications](../../apps/deploy-use/create-applications.md) and [Revise and supersede applications](../../apps/deploy-use/revise-and-supersede-applications.md).|  
|**Step 4:** Add the application to the Microsoft Intune Subscription Wizard.|For more information, see [Set up Windows Phone and Windows 10 Mobile hybrid device management with System Center Configuration Manager and Microsoft Intune](../../mdm/deploy-use/enroll-hybrid-windows.md).|  
|**Step 5:** Delete the deployment that is automatically created when you added the company portal app to the Microsoft Intune Subscription Wizard.|The Microsoft Intune subscription has created an automatic deployment of this app, as this deployment will not support supersedence.|  
|**Step 6:** Create a new deployment of the application. On the **Deployment Settings** page of the **Deploy Software Wizard**, check **Automatically upgrade any superceded versions of this application**.|Create a new deployment with supersedence using the application you created with the supersedence relationship.|  
|**Step 7 (Optional):** By default, the superseding apps install on devices after 7 days. To deploy the company portal app sooner to previously enrolled devices, change the **schedule re-evaluation for deployments** setting to a lower value.<br /><br /> If you set this value to a lower value than the default, it might negatively affect the performance of your network and client computers.|No additional information.|  
