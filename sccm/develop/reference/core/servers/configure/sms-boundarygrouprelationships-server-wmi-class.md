---
title: "SMS_BoundaryGroupRelationships Class"
titleSuffix: "Configuration Manager"
ms.date: "03/13/2017"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 155ed51e-a6a9-4ed6-bddb-5eabbb77ec4c
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_BoundaryGroupRelationships Server WMI Class

The `SMS_BoundaryGroupRelationships` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents fallback relationships for boundary groups.

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_BoundaryGroupRelationships : SMS_BaseClass  
{  
    UInt32 DestinationGroupID;
    String DestinationGroupName;
    UInt32 SourceGroupID;
    String SourceGroupName;
};  
```  

## Methods  
 The following table shows the methods in `SMS_BoundaryGroupRelationships`.  

|Method|Description|  
|------------|-----------------|  
|[FallbackDP Method in Class SMS_BoundaryGroupRelationships](../../../../../develop/reference/core/servers/configure/fallbackdp-method-in-class-sms-boundarygrouprelationships.md)|Sets the fallback time for a distribution point (DP).|  
|[FallbackMP Method in Class SMS_BoundaryGroupRelationships](../../../../../develop/reference/core/servers/configure/fallbackmp-method-in-class-sms-boundarygrouprelationships.md)|Sets the fallback time for a management point (MP).|
|[FallbackSMP Method in Class SMS_BoundaryGroupRelationships](../../../../../develop/reference/core/servers/configure/fallbacksmp-method-in-class-sms-boundarygrouprelationships.md)|Sets the fallback time for a state migration point (SMP).|
|[FallbackSUP Method in Class SMS_BoundaryGroupRelationships](../../../../../develop/reference/core/servers/configure/fallbacksup-method-in-class-sms-boundarygrouprelationships.md)|Sets the fallback time for a software update point (SUP).|

## Properties  
 `DestinationGroupID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 ID of the destination boundary group.

 `DestinationGroupName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Name of the destination boundary group.

 `SourceGroupID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 ID of the source boundary group.

 `SourceGroupName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Name of the source boundary group.

## Remarks

 Class qualifiers for this class include:

 -   Secured

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

 ## See Also   
 [SMS_BoundaryGroup Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_boundarygroup-server-wmi-class.md)

 [Configuration Manager Site Configuration Server WMI Classes](../../../../../develop/reference/core/servers/configure/site-configuration-server-wmi-classes.md)
