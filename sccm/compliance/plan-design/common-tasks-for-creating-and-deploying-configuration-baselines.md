---
title: "Common tasks for configuration baselines - Configuration Manager | Microsoft Docs"
description: "Learn about how to create and deploy System Center Configuration Manager configuration baselines."
ms.custom: na
ms.date: 07/12/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4bb6afeb-d267-4f9b-ade2-26e5400c223b
caps.latest.revision: 6
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe

---
# Common tasks for creating and deploying configuration baselines with System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

This topic contains common scenarios to help you learn about how to create and deploy System Center Configuration Manager configuration baselines.  

 If you are already familiar with compliance settings, you can find detailed documentation about all the features you use in the [Create configuration baselines](../../compliance/deploy-use/create-configuration-baselines.md) and [Deploy configuration baselines](../../compliance/deploy-use/deploy-configuration-baselines.md) topics.  

 Before you start, read [Get started with compliance settings in System Center Configuration Manager](../../compliance/get-started/get-started-with-compliance-settings.md) to learn some basics about compliance settings, and also read [Plan for and configure compliance settings](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md) to implement any necessary prerequisites.  

## Create a configuration baseline  
 In this example, you've created a configuration item for only Windows 10 PCs that run the Configuration Manager client.  

 This configuration item enforces a required password of at least 6 characters on Windows 10 PCs. The configuration item is named **Windows 10 Password Enforcement**.  

Use the following procedure to learn how to add this configuration item to a configuration baseline to prepare it for deployment.  

1.  In the Configuration Manager console, click **Assets and Compliance** > **Compliance Settings** > **Configuration Baselines**.  

3.  On the **Home** tab, in the **Create** group, click **Create Configuration Baseline**.  

4.  In the **Create Configuration Baseline** dialog box, configure the following settings:  

    -   **Name** - Enter **Windows 10 Passwords** (or another name of your choice)  

5.  Click **Add** > **Configuration Items**.  

6.  In the **Add Configuration Items** dialog box, select the **Windows 10 Password Enforcement** configuration item that you previously created, then click **Add**.  

7.  Click OK to close the **Add Configuration Items** dialog box and return to the **Create Configuration Baseline** dialog box.

8.  Click **OK** to close the **Create Configuration Baseline** dialog box.  

 You can now see the configuration baseline in the **Configuration Baselines** node of the Configuration Manager console.  

## Deploy the configuration baseline  
 In this example, you deploy the configuration baseline you created in the previous procedure to a collection of computers.  

1.  In the Configuration Manager console, click **Assets and Compliance** > **Compliance Settings** > **Configuration Baselines**.  

3.  From the list of configuration baselines, select **Windows 10 Passwords**.  

4.  On the **Home** tab, in the **Deployment** group, click **Deploy**.  

5.  In the **Deploy Configuration Baselines** dialog box, configure the following Metings:  

    -   **Selected configuration baselines** - Ensure that the **Windows 10 Passwords** configuration baseline was automatically added to this list.  

    -   **Remediate noncompliant rules when supported** - Check this box to ensure that if the correct settings are not present on targeted devices, then they are remediated by Configuration Manager.  

    -   **Collection** - Click **Browse** to choose the collection of computers on which the configuration baseline is evaluated and remediated for compliance. In this example, the configuration baseline was deployed to the built-in **All Desktop and Server Clients** collection.  

        > [!TIP]  
        >  Don't worry if the collection you choose contains computers or devices that don't run Windows 10. As long as you configured supported platforms in the configuration item you created, only Windows 10 PCs are evaluated for compliance.  

    -   If necessary, configure the schedule by which the configuration baseline is evaluated. Otherwise, keep the default of **7 Days**.  

7.  Click **OK** to close the **Deploy Configuration Baselines** dialog box and create the deployment.  

 If you want to take a quick look at compliance statistics for this deployment, in the **Monitoring** workspace, click **Deployments**. At the bottom of the screen, you see a **Compliance Statistics** chart.  

## Next steps 

For more detailed information about how to monitor configuration baselines, see [Monitor compliance settings](../../compliance/deploy-use/monitor-compliance-settings.md).  
