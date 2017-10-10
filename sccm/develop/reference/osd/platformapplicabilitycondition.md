---
title: "PlatformApplicabilityCondition"
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
ms.assetid: c264dab1-07c2-4cc6-95e2-6283b850fb54searchScope: - ConfigMgr SDK
caps.latest.revision: 12
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# PlatformApplicabilityCondition
`PlatformApplicabilityCondition` specifies one supported platform for an operating system deployment driver in System Center Configuration Manager.  

> [!NOTE]
>  It is only valid to populate this information with values from `SMS_SupportedPlatforms Server WMI Class` objects. Drivers can be targeted only at major releases, for example, all Windows.  

 **Type**: String.  

 **Instances**: Zero or more.  

## Attributes  

|Attribute|Description|  
|---------------|-----------------|  
|DisplayName|The platform name displayed in the System Center Configuration Manager console.|  
|MaxVersion|The maximum supported version. For example, "5.20.9999.9999".|  
|MinVersion|The minimum supported version. For example, "5.20.3790.0".|  
|Name|The operating system name. For example, "Windows NT".|  
|Platform|The supported platform. For example "x64".|  

## See Also  
 [Operating System Deployment Driver Supported Platforms Schema](../../../develop/reference/osd/operating-system-deployment-driver-supported-platforms-schema.md)   
 [PlatformApplicabilityConditions](../../../develop/reference/osd/platformapplicabilityconditions.md)   
 [Query1](../../../develop/reference/osd/query1.md)   
 [Query2](../../../develop/reference/osd/query2.md)
