---

title: Software updates maintenance
description: "To maintain updates in Configuration Manager, you can schedule the WSUS cleanup task, or you can run it manually."
keywords:
author: dougebyms.author: dougebymanager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service:
ms.technology:
 - configmgr-sum
ms.assetid: 4b0e2e90-aac7-4d06-a707-512eee6e576c


---
# Software updates maintenance*Applies to: System Center Configuration Manager (Current Branch)*
You can schedule and run the WSUS clean up task from the Configuration Manager console or you can manually run the WSUS cleanup task from in Software Update Point Component properties. When you select to run the WSUS cleanup task, it will run at the next software updates synchronization. The expired software updates will be set to a status of declined on the WSUS server and the Windows Update Agent on computers will no longer scan these software updates. By default, the WSUS cleanup job runs every 30 days.  

#### To schedule and run the WSUS cleanup job  

1.  In the Configuration Manager console, navigate to **Administration** > **Overview** > **Site Configuration** > **Sites**.  

2.  Click **Configure Site Components** in the **Settings** group, and then click **Software Update Point** to open Software Update Point Component Properties.  

3.  Click the **Supersedence Rules** tab, select **Run WSUS cleanup wizard**, and then click **OK**.
