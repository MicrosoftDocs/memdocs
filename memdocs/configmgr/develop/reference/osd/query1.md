---
title: Query1
titleSuffix: Configuration Manager
description: Query1 specifies a query, in Configuration Manager, that is used to identify the platform that a client computer is running.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: b639050e-d04e-4650-8fe1-a1d39e5b759f
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# Query1
**Query1** specifies a query, in Configuration Manager, that is used to identify the platform that a client computer is running.  

> [!NOTE]
>  This information should come from `SMS_SupportedPlatforms Server WMI Class` objects and match the platform information specified in the PlatformApplicabilityCondition node.  

 The query is run on the client computer and typically inspects Windows Management Instrumentation (WMI) to determine the client platform. For example, `SELECT * FROM Win32_OperatingSystem WHERE BuildNumber = '3790' AND OSType=18 AND ProductType=1`.  

 **Type**: Element.  

 **Instances**: One.  

## Attributes  
 None  

## See Also  
 [Operating System Deployment Driver Supported Platforms Schema](../../../develop/reference/osd/operating-system-deployment-driver-supported-platforms-schema.md)   
 [PlatformApplicabilityCondition](../../../develop/reference/osd/platformapplicabilitycondition.md)   
 [Query2](../../../develop/reference/osd/query2.md)
