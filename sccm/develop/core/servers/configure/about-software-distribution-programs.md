---
title: "Software Distribution Programs"
titleSuffix: "Configuration Manager"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: 590d8888-608d-491e-a754-4831138fca2asearchScope: - ConfigMgr SDK
caps.latest.revision: 12
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# About Software Distribution Programs
Programs are commands that are associated with a System Center Configuration Manager package that tell a client what should occur on the client computer when the package is received. You can associate almost any activity with a program. For example, a program can be used to install new software on clients, distribute data files, run virus-detection software, or update client configuration.  

 Every deployable package must contain at least one program, but you can specify more than one, if needed. A package can often have several programs associated with it, allowing the package to be run in different ways on different clients. This is often the case when you are installing a new application on a client computer and want to create programs to perform either a typical, minimum, or custom installation.  

 Although the package contains the application, files, or information that need to be applied to the client computers, the program is responsible for defining how that application is to be used. As a result, the program must include all appropriate references to script files or command switches. The program also defines the platform and environment in which the package can run, which means that you might have a program for each suitable platform when you have clients using different operating systems.  

 After you create a program for a given package, you can make that program and package available to a collection of clients by using an advertisement.  

## See Also  
 [Configuration Manager Software Distribution](../../../../develop/core/servers/configure/software-distribution.md)   
 [Software Distribution Packages](../../../../develop/core/servers/configure/software-distribution-packages.md)   
 [Software Distribution Programs](../../../../develop/core/servers/configure/software-distribution-programs.md)   
 [Software Distribution Advertisements](../../../../develop/core/servers/configure/software-distribution-advertisements.md)   
 [Configuration Manager Collections](../../../../develop/core/clients/collections/collections.md)
