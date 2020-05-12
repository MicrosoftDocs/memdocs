---
title: "Uninstall applications"
titleSuffix: "Configuration Manager"
description: "Uninstall an application by using Configuration Manager"
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 0ea3edaa-27c6-4391-9896-cd97d9c5d06d
author: aczechowski
ms.author: aaroncz
manager: dougeby


---
# Uninstall applications with Configuration Manager

*Applies to: Configuration Manager (current branch)*


Take the following actions to uninstall an application you previously deployed.

-   Specify the command line to uninstall the deployment type content on the **Content** page of the Create Deployment Type Wizard.  

-   Deploy the application by using a deployment action of **Uninstall**.  

> [!IMPORTANT]  
> Some application types do not support uninstallation.  

 This list gives you more information about how application uninstall works:  

-   When you uninstall a Configuration Manager (Configuration Manager) application, any dependent applications are not automatically uninstalled.  

-   If you deploy an application that uses an action of **Uninstall** to a user, and the application was installed for all users of the computer, the uninstall might fail if the user's account does not have permissions to uninstall the application.  

-   If you remove a user or a device from a collection that has an application deployed to it, the application is not automatically removed from the device.  

-   A deployment with the deployment purpose of **Uninstall** does not check requirement rules. If the application is installed on the computer on which the deployment runs, it will be uninstalled.  

> [!IMPORTANT]  
> To deploy the application with the Uninstall action, you must first delete any existing application deployments, simulated deployments, or task sequence deployments that include this application. 

 For more information about how to create a deployment type, see [Create applications](../../apps/deploy-use/create-applications.md).  

 For more information about how to deploy an application, see [Deploy applications](../../apps/deploy-use/deploy-applications.md).  

## Uninstall an application  

1.  Configure the application deployment type with the uninstall command line by using one of the following methods:  

    -   On the **General** page of the Create Deployment Wizard, select the option **Automatically identify information about this deployment type from installation files**. If the information is available in the installation files, the uninstall command line is automatically added to the deployment type properties.  

    -   On the **Content** page of the Create Deployment Type Wizard, in the **Uninstall program** field, specify the command line to uninstall the application.  

        > [!NOTE]  
        >  The **Content** page is displayed only if you select the option **Manually specify the deployment type information** on the **General** page of the Create Deployment Type Wizard.  

    -   On the **Programs** tab of the **<*deployment type name*> Properties** dialog box, specify the command line to uninstall the application in the **Uninstall program** field.  

2.  Deploy the application, and then select the deployment action **Uninstall** on the **Deployment Settings** page of the Deploy Software Wizard.  

    > [!NOTE]  
    >  When you select a deployment action of **Uninstall**, the deployment purpose is automatically configured as **Required**.  
