---
title: "Software Distribution Deployments"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 879be718-4ce0-46bc-a2e3-161b97f836a5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# About Software Distribution Deployments
In Configuration Manager, after a software distribution package has been created, with programs to tell client computers what to do with the package, you need to advertise the program that you want the clients to run. Advertising the program makes a program available to a specified collection of clients.  

 Advertisements are evaluated by Configuration Manager to determine which clients will receive a specific program to run on their computers. An advertisement specifies the following information:  

- The specific program to run on the client.  

- The target collection of computers, users, or user groups that are to receive the program.  

- The schedule that specifies when the program is available to clients. In the case of assigned (mandatory) advertisements, additional options such as Wake On LAN and ignoring maintenance windows can be used with this schedule.  

  The site's clients cannot receive advertised programs until you enable the software distribution advertised programs client agent on the site's clients. The **Advertised Programs Client Agent** performs the necessary software distribution-related tasks on these clients, primarily allowing the clients to receive and run the programs that you advertise.  

## See Also  
 [About deployments](about-software-distribution-deployments.md)
 [Software distribution overview](software-distribution-overview.md)
