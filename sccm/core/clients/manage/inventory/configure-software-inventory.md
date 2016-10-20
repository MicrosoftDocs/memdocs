---
title: "Configure software inventory | System Center Configuration Manager"
description: "Set up software inventory and an inventory exclusion folder in System Center Configuration Manager."
ms.custom: na
ms.date: 12/08/2015
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: cc226259-0e28-410a-94d3-223bdc948818
caps.latest.revision: 4
caps.handback.revision: 0
author: nbigmanms.author: nbigmanmanager: angrobe

---
# How to configure software inventory in System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
You can create a hidden file named **Skpswi.dat** and place it in the root of a client hard drive to exclude it from System Center Configuration Manager software inventory. You can also place this file in the root of any folder structure you want to exclude from software inventory. This procedure can be used to disable software inventory on a single workstation or server client, such as a large file server.  

> [!NOTE]  
>  Software inventory will not inventory the client drive again unless this file is deleted from the drive on the client computer.  

### To exclude folders from software inventory  

1.  Using Notepad.exe, create an empty file named **Skpswi.dat**.  

2.  Right click the **Skpswi.dat** file and click **Properties**. In the file properties for the Skpswi.dat file, select the **Hidden** attribute.  

3.  Place the **Skpswi.dat** file at the root of each client hard drive or folder structure that you want to exclude from software inventory.  
