---
description: Learn how to specify one supported platform for an operating system deployment driver in Configuration Manager using PlatformApplicabilityCondition.
title: PlatformApplicabilityCondition
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: c264dab1-07c2-4cc6-95e2-6283b850fb54
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# PlatformApplicabilityCondition
`PlatformApplicabilityCondition` specifies one supported platform for an operating system deployment driver in Configuration Manager.  

> [!NOTE]
>  It is only valid to populate this information with values from `SMS_SupportedPlatforms Server WMI Class` objects. Drivers can be targeted only at major releases, for example, all Windows.  

 **Type**: String.  

 **Instances**: Zero or more.  

## Attributes  

|Attribute|Description|  
|---------------|-----------------|  
|DisplayName|The platform name displayed in the Configuration Manager console.|  
|MaxVersion|The maximum supported version. For example, "5.20.9999.9999".|  
|MinVersion|The minimum supported version. For example, "5.20.3790.0".|  
|Name|The operating system name. For example, "Windows NT".|  
|Platform|The supported platform, for example, "x64".|  

## See Also  
 [Operating System Deployment Driver Supported Platforms Schema](../../../develop/reference/osd/operating-system-deployment-driver-supported-platforms-schema.md)   
 [PlatformApplicabilityConditions](../../../develop/reference/osd/platformapplicabilityconditions.md)   
 [Query1](../../../develop/reference/osd/query1.md)   
 [Query2](../../../develop/reference/osd/query2.md)
