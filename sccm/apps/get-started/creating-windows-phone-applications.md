---
title: "Create Windows Phone applications | Microsoft Docs"
description: "See which considerations you must take into account when you create and deploy applications for Windows Phone devices."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 866113ff-efd0-40d2-ac3a-2edd49732a24
caps.latest.revision: 10
author: robstackmsftms.author: robstackmanager: angrobe

---
# Create Windows Phone applications with System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
In addition to the other System Center Configuration Manager requirements and procedures for creating an application, you must also take the following considerations into account when you create and deploy applications for Windows Phone devices.  

## General considerations  
 Configuration Manager supports deploying the following app types:  

|Device Type|Supported Files|  
|-----------------|---------------------|  
|Windows Phone 8|.xap|  
|Windows Phone 8.1|.xap, .appx, .appxbundle|  

 The following deployment actions are supported:  

|Device type|Supported actions|  
|-----------------|-----------------------|  
|Windows Phone 8 and Windows Phone 8.1|Available, Required, Uninstall|  

## Steps to deploy the latest Windows Phone Company Portal app with supersedence  
 The following table provides the steps, details, and more information for creating and deploying the latest Windows Phone 8 company portal app.  

|Step|More Information|  
|----------|----------------------|  
|**Step 1:** Get the latest company portal app.|Download the [Windows Phone 8 company portal app](http://go.microsoft.com/fwlink/?LinkId=268440).|  
|**Step 2:** Sign the company portal app with your Symantec certificate.|For information on how to sign the company portal app, see [Set up Windows Phone and Windows 10 Mobile hybrid device management with System Center Configuration Manager and Microsoft Intune](../../mdm/deploy-use/set-up-windows-phone-hybrid-enrollment.md).|  
|**Step 3:** Create a new application with the latest version of the company portal app and specify a supersedence relationship.|For more information, see [Create applications](../../apps/deploy-use/create-applications.md) and [Revise and supersede applications](../../apps/deploy-use/revise-and-supersede-applications.md).|  
|**Step 4:** Add the application to the Microsoft Intune Subscription Wizard.|Add the application Windows Phone 8 page of the Microsoft Intune Subscription Wizard. For more information, see [Set up Windows Phone and Windows 10 Mobile hybrid device management with System Center Configuration Manager and Microsoft Intune](../../mdm/deploy-use/set-up-windows-phone-hybrid-enrollment.md).|  
|**Step 5:** Delete the deployment that is automatically created when you added the company portal app to the Microsoft Intune Subscription Wizard.|The Microsoft Intune subscription has created an automatic deployment of this app, as this deployment will not support supersedence.|  
|**Step 6:** Create a new deployment of the application and check **Automatically upgrade any superceded versions of this application** on the **Deployment Settings** page of the **Deploy Software Wizard**.|Create a new deployment with supersedence using the application you created with the supersedence relationship.|  
|**Step 7 (Optional):** The superseding apps would install on devices after 7 days by default. To deploy the company portal app sooner to previously enrolled devices, you can change the **schedule re-evaluation for deployments** setting to a lower value.<br /><br /> If you set this value to a lower value than the default, it might negatively affect the performance of your network and client computers.|No additional information.|  
