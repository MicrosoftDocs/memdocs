---
description: Learn all about software distribution programs and how they are packaged and made available to a collection of clients.
title: Software Distribution Programs
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 590d8888-608d-491e-a754-4831138fca2a
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# About Software Distribution Programs
Programs are commands that are associated with a Configuration Manager package that tell a client what should occur on the client computer when the package is received. You can associate almost any activity with a program. For example, a program can be used to install new software on clients, distribute data files, run virus-detection software, or update client configuration.  

 Every deployable package must contain at least one program, but you can specify more than one, if needed. A package can often have several programs associated with it, allowing the package to be run in different ways on different clients. This is often the case when you are installing a new application on a client computer and want to create programs to perform either a typical, minimum, or custom installation.  

 Although the package contains the application, files, or information that need to be applied to the client computers, the program is responsible for defining how that application is to be used. As a result, the program must include all appropriate references to script files or command switches. The program also defines the platform and environment in which the package can run, which means that you might have a program for each suitable platform when you have clients using different operating systems.  

 After you create a program for a given package, you can make that program and package available to a collection of clients by using an advertisement.  

## See Also  
 [Software distribution overview](software-distribution-overview.md)
 [About deployments](about-software-distribution-deployments.md)
