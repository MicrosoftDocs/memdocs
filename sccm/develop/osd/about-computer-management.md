---
title: "Computer Management"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 57146de9-c8ca-480d-9f6f-41c88525b326
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# About Computer Management
Computer management in System Center Configuration Manager operating system deployment covers the following areas.  

## Computer Import  
 To deploy an operating system to a new computer without stand-alone media that is not currently managed by System Center Configuration Manager, the new computer must be added to the Configuration Manager database prior to initiating the operating system deployment process. Although Configuration Manager can automatically discover computers on your network that have a Windows operating system installed, if the computer has no operating system installed you must import the new computer information. For more information, see [How to Import a New Computer into Configuration Manager](../../develop/osd/how-to-import-a-new-computer-into-configuration-manager.md).  

## Computer Association  
 A computer association creates a relationship between a source and destination computer for the side-by-side migration of user state data. The source computer is an existing computer that is managed by Configuration Manager, and contains the user state data and settings that will be migrated to a specified destination computer. For more information, see [How to Create an Association Between Two Computers in Configuration Manager](../../develop/osd/how-to-create-an-association-between-two-computers-in-configuration-manager.md).  

## Computer and Machine Variables  
 Task sequences can be configured to run simultaneously on multiple computers or on collections. You can specify unique per-computer or per-collection information, such as specifying a unique operating system product key or joining all the members of a collection to a domain. These settings can be configured when you create a task sequence or edit an existing task sequence.  

 You can assign task sequence variables to a single computer or to a collection. When the task sequence starts to run on the target computer or the collection, the values that are specified are applied to the target computer or collection.  

 For more information, see the following:  

|Task|How to|  
|----------|------------|  
|Collection variables|[How to Create a Collection Variable in Configuration Manager](../../develop/osd/how-to-create-a-collection-variable.md)|  
|Computer variables|[How to Create a Computer Variable in Configuration Manager](../../develop/osd/how-to-create-a-computer-variable.md)|  
|Setting task sequence variables|[How to Set an Operating System Deployment Task Sequence Variable](../../develop/osd/how-to-set-an-operating-system-deployment-task-sequence-variable.md)|  
|Changing variables in a running task sequence|[How to Use Task Sequence Variables in a Running Configuration Manager Task Sequence](../../develop/osd/how-to-use-task-sequence-variables-in-a-running-task-sequence.md)|  

## See Also  
 [Configuration Manager Operating System Deployment](../../develop/osd/operating-system-deployment.md)
