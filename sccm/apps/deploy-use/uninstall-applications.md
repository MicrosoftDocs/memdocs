---
title: "Uninstall applications | System Center Configuration Manager"
description: "Uninstall an application by using System Center Configuration Manager"
ms.custom: na
ms.date: 12/08/2015
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0ea3edaa-27c6-4391-9896-cd97d9c5d06d
caps.latest.revision: 4
caps.handback.revision: 0
author: robstackmsft

---
# Uninstall applications with System Center Configuration Manager
Perform the following steps to uninstall an application by using System Center Configuration Manager:  

-   Specify the command line to uninstall the deployment type content on the **Content** page of the **Create Deployment Type Wizard**.  

-   Deploy the application by using a deployment action of **Uninstall**.  

> [!IMPORTANT]  
>  Some application types do not support uninstallation.  

 The following list gives more information about the application uninstall behavior:  

-   When you uninstall a Configuration Manager application, any dependent applications are not automatically uninstalled.  

-   If you deploy an application that uses an action of **Uninstall** to a user, and the application was installed for all users of the computer, then the uninstall might fail if the user’s account does not have permissions to uninstall the application.  

-   If you remove a user or device from a collection that has an application deployed to it, the application will not be automatically removed from the device.  

-   A deployment with the deployment purpose of **Uninstall** does not check requirement rules. If the application is installed on the computer on which the deployment runs, it will be uninstalled.  

> [!IMPORTANT]  
>  You must delete any existing deployments or simulated deployments of an application to a collection before you can deploy the application with a deployment action of **Uninstall**.  

 For more information about how to create a deployment type, see [How to create applications with System Center Configuration Manager](../../apps/deploy-use/create-applications.md).  

 For more information about how to deploy an application, see [How to deploy applications with System Center Configuration Manager](../../apps/deploy-use/deploy-applications.md).  

## Uninstall an application  

1.  Configure the application deployment type with the uninstall command line by using one of the following methods:  

    -   On the **General** page of the **Create Deployment Wizard**, select the option **Automatically identify information about this deployment type from installation files**. If the information is available in the installation files, the uninstall command line is automatically added to the deployment type properties.  

    -   On the **Content** page of the **Create Deployment Type Wizard**, in the **Uninstall program** field, specify the command line to uninstall the application.  

        > [!NOTE]  
        >  The **Content** page is displayed only if you select the option **Manually specify the deployment type information** on the **General** page of the **Create Deployment Type Wizard**.  

    -   In the **Programs** tab of the *<deployment type name\>***Properties** dialog box specify the command line to uninstall the application in the **Uninstall program** field.  

2.  Deploy the application and select the deployment action **Uninstall** from the **Deployment Settings** page of the **Deploy Software Wizard**.  

    > [!NOTE]  
    >  When you select a deployment action of **Uninstall**, the deployment purpose is automatically configured as **Required**.  
