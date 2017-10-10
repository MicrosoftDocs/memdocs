---

title: Remove a software update point
description: "Follow this procedure to remove the software update point site system role at a site from the Configuration Manager console."
keywords:
author: dougebyms.author: dougebymanager: angrobe

ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service:
ms.technology:
 - configmgr-sum
ms.assetid: 2486375c-d4a2-4cf2-9124-9bee02bbf173

---
#  <a name="BKMK_RemoveSUP"></a> Remove the software update point site system role  *Applies to: System Center Configuration Manager (Current Branch)*
You can remove the software update point site system role at a site from the Configuration Manager console. The client policy is updated to remove the software update point from the list. When you remove the last software update point at the site, the software update point list will contain no software update points, and software updates is essentially disabled at the site. When you have more than one software update point at a primary site and you remove the software update point that is configured as the synchronization source, you must choose another software update point at the site to be the new synchronization source.  

> [!NOTE]  
>  When you remove the software update point site role from a site system, wait at least 15 minutes before you reinstall the software update point site role.  

 Use the following procedure to remove a software update point.  

#### To remove the software update point  

1.  In the **Configuration Manager** console, click **Administration**.  

2.  In the Administration workspace, expand **Site Configuration**, and then click **Servers and Site System Roles**.  

3.  Select the site system server with the software update point to remove, and then in **Site System Roles**, select **Software update point**.  

4.  On the **Site Role** tab, in the **Site Role** group, click **Remove Role**. Confirm that you want to remove the software update point or select a new synchronization source for the other software update points at the site.  
