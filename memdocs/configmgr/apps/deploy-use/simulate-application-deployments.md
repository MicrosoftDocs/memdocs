---
title: Simulate application deployments
titleSuffix: Configuration Manager
description: Evaluate the detection method, requirements, and dependencies for a deployment type without installing the application.
ms.date: 10/06/2016
ms.subservice: app-mgt
ms.service: configuration-manager
ms.topic: conceptual
author: baladelli
manager: apoorvseth
ms.author: baladell
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# Simulate application deployments with Configuration Manager

*Applies to: Configuration Manager (current branch)*

You can use simulated deployments to test an application deployment without installing or uninstalling the application. A simulated deployment evaluates the detection method, requirements, and dependencies for a deployment type. It reports the results in the **Deployments** node of the **Monitoring** workspace. Use the procedure in this topic to simulate an application deployment in Configuration Manager.  

> [!NOTE]  
> You cannot use simulated deployments for collections of mobile devices.  
>   
> You cannot deploy an application with a deployment purpose of **Uninstall** if a simulated deployment of the same application is active.  

## Configure a simulated application deployment

1.  In the Configuration Manager console, select one of the following:  
    -   A collection of users.  
    -   A collection of devices.  
    -   A Configuration Manager application.  

2.  On the **Home** tab, in the **Deployment** group, choose **Simulate Deployment**.  

3.  In the Simulate Application Deployment Wizard, set the following details for your simulated deployment:  

    -   **Application**. Choose **Browse**, and then select the application you want to create a simulated deployment for.  

    -   **Collection**. Choose **Browse**, and then select the collection that you want to use for the simulated deployment.  

    -   **Action**. From the drop-down list, select whether you want to simulate the installation or the uninstallation of the selected application.  

    -   **Deploy automatically with or without user login**. If this option is checked, the clients evaluate the simulated deployment whether or not the clients are logged in.  

4.  Click **Next**, review the information on the **Summary** page, and then finish the wizard to create the simulated application deployment.  

5.  Simulated applications appear in the **Deployments** node of the **Monitoring** workspace, with a purpose of **Simulate**. For more information about how to monitor application deployments, see [Monitor applications from the Configuration Manager console](../../apps/deploy-use/monitor-applications-from-the-console.md).  
