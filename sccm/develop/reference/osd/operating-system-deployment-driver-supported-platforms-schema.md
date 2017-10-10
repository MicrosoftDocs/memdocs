---
title: "OS Deployment Driver Supported Platforms Schema"
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
ms.assetid: b45c883b-d9c3-4c88-a7c9-f38b421d475asearchScope: - ConfigMgr SDK
caps.latest.revision: 12
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# Operating System Deployment Driver Supported Platforms Schema
The following reference section documents the XML schema that is used to specify the platforms that are supported by an operating system deployment driver in Microsoft System Center Configuration Manager.  

 The schema is used in the `SMS_Driver` class `SDMPackageXML` property.  

> [!CAUTION]
>  The supported platforms portion of `SDMPackageXML` is the only part of the Driver XML schema that can be edited. You should not make changes to other parts of the XML.  

## Supported Platform XML  
 \<[PlatformApplicabilityConditions](../../../develop/reference/osd/platformapplicabilityconditions.md)>  

 \<[PlatformApplicabilityCondition](../../../develop/reference/osd/platformapplicabilitycondition.md)>  

 \<[Query1](../../../develop/reference/osd/query1.md)>\</Query1>  

 \<[Query2](../../../develop/reference/osd/query2.md)>\</Query2>  

 \</PlatformApplicabilityCondition>  

 \</PlatformApplicabilityConditions>  

## See Also  
 [Operating System Deployment Driver Supported Platforms Schema](../../../develop/reference/osd/operating-system-deployment-driver-supported-platforms-schema.md)   
 [PlatformApplicabilityCondition](../../../develop/reference/osd/platformapplicabilitycondition.md)   
 [Query1](../../../develop/reference/osd/query1.md)   
 [Query2](../../../develop/reference/osd/query2.md)
