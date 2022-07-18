---
title: "SMS_BoundaryGroupSiteSystems Class"
titleSuffix: "Configuration Manager"
description: "The SMS_BoundaryGroupSiteSystems WMI class represents site systems that serve computers within the boundary group."
ms.date: "03/13/2017"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 9d48ae1d-dce8-483f-bcd0-f4154a3ecbef
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_BoundaryGroupSiteSystems Server WMI Class
The `SMS_BoundaryGroupSiteSystems` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents site systems that serve computers within the boundary group.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_BoundaryGroupSiteSystems : SMS_BaseClass  
{  
    UInt32 Flags;  
    UInt32 GroupID;  
    String ServerNALPath;  
    String SiteCode;  
};  
```  

## Methods  
 The `SMS_BoundaryGroupSiteSystems` class does not define any methods.  

## Properties  
 `Flags`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [bits]  

 Specifies the connection type of the boundary. Possible values are:  

|Value|Description|  
|---|---|  
|0|FAST|  
|1|SLOW|  

> [!NOTE]
> This parameter is no longer used for distribution points.


 `GroupID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Unique identifier of the boundary group.  

 `ServerNALPath`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 NAL path of site system servicing machines within the boundary.  

 `SiteCode`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read, sizelimit("3")]  

 Site code of the role.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Site Configuration Server WMI Classes](../../../../../develop/reference/core/servers/configure/site-configuration-server-wmi-classes.md)
