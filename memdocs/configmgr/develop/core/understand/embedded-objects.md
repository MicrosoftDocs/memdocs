---
title: Embedded Objects
titleSuffix: Configuration Manager
description: You cannot use Windows Management Instrumentation (WMI) to enumerate, query, get, or put embedded objects. You can only retrieve and store embedded objects through the parent instance.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: article
ms.assetid: 910108e3-1be0-4474-9df6-7d51bc45cf58
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# Configuration Manager Embedded Objects
Configuration Manager embedded objects do not exist by themselves in the Common Information Model (CIM) repository — they exist within other objects. As a result, you cannot use Windows Management Instrumentation (WMI) to enumerate, query, get, or put embedded objects. You can only retrieve and store embedded objects through the parent instance.  

 Embedded objects are commonly used when accessing the site control file. In this case, special embedded objects, such as properties and property lists are used.  

 When a class or method contains an embedded object of an abstract type, such as `SMS_ScheduleToken`, you store and retrieve classes that are inherited from it. For example, instead of using `SMS_ScheduleToken`, you use one of the embedded objects inherited from it, such as `SMS_ST_RecurWeekly`.  

## See Also  
 [How to Read and Write to the Configuration Manager Site Control File by Using Managed Code](../../../develop/core/understand/how-to-read-and-write-to-the-site-control-file-by-using-managed-code.md)   
 [How to Read and Write to the Configuration Manager Site Control File by Using WMI](../../../develop/core/understand/how-to-read-and-write-to-the-site-control-file-by-using-wmi.md)
