---
title: "Software Distribution Overview"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: b3c66208-ef68-4e4f-9fd5-2baf0ea0b19f
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Software Distribution Overview
With this release, System Center Configuration Manager expands the abilities of system administrators to centrally manage computers effectively. Building on the capabilities provided by Configuration Manager 2007, System Center Configuration Manager provides a refined tool set for software distribution.  

## Distributing Software  
 The software distribution process advertises packages, which contain programs, to members of a collection. The client then installs the software from specified distribution points. The order in which you create the components that make up the software distribution process is important.  

1. Create an instance of `SMS_Package`.  

2. Create an instance of `SMS_Program`.  

3. If an existing collection does not identify the users to whom you want to distribute the software, create a new collection by creating an instance of `SMS_Collection`.  

4. If the package contains source files, define a distribution point for the package by creating an instance of `SMS_DistributionPoint`.  

5. Create an instance of `SMS_Advertisement`.  

   The following topics show how to create the software distribution components:  

   [How to Create a Package](../../../../develop/core/servers/configure/how-to-create-a-package.md)  

   [How to Create a Program](../../../../develop/core/servers/configure/how-to-create-a-program.md)  

   [How to Assign a Package to a Distribution Point](../../../../develop/core/servers/configure/how-to-assign-a-package-to-a-distribution-point.md)  

   [How to Create an Advertisement](../../../../develop/core/servers/configure/how-to-create-an-advertisement.md)  

## See Also  
 [Configuration Manager SDK](../../../../develop/core/misc/system-center-configuration-manager-sdk.md)   
 [Configuration Manager Software Distribution](../../../../develop/core/servers/configure/software-distribution.md)
