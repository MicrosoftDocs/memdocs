---
description: Learn how to retrieve the site's monitored configuration status, such as the SQL Server port, SQL Server Service Broker port, and SQL Server Firewall port.
title: SMS_CMSiteConfiguration Class
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 3fa45ffd-9661-4863-b86a-e552a865b2d5
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_CMSiteConfiguration Server WMI Class
The `SMS_CMSiteConfiguration` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that returns the site's monitored configuration status, such as the SQL Server port, SQL Server Service Broker port, and SQL Server Firewall port.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_CMSiteConfiguration : SMS_BaseClass  
{  
    String Configuration;  
    DateTime LastEvaluatingTime;  
    UInt32 MessageID;  
    String Param1;  
    String Param2;  
    String Param3;  
    String Param4;  
    String Param5;  
    String Param6;  
    UInt32 RoleID;  
    String RoleName;  
    String SiteCode;  
    UInt32 State;  
};  
```  

## Methods  
 The `SMS_CMSiteConfiguration` class does not define any methods.  

## Properties  
 `Configuration`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: none  

 Configuration.   

 `LastEvaluatingTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: none  

 Last evaluation time.   

 `MessageID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: none  

 Message identifier.   

 `Param1`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: none  

 Parameter 1.   

 `Param2`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: none  

 Parameter 2.   

 `Param3`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: none  

 Parameter 3.   

 `Param4`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: none  

 Parameter 4.   

 `Param5`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: none  

 Parameter 5.   

 `Param6`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: none  

 Parameter 6.   

 `RoleID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key]  

 Role identifier.   

 `RoleName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: none  

 Role name.   

 `SiteCode`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key]  

 Site code.   

 `State`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [enumeration]  

 State.   

|Value|State|  
|-|-|  
|0|Valid|  
|1|Failed without Remediation|  
|2|Failed with remediaton|  
|99|Unknown|  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Site Configuration Server WMI Classes](../../../../../develop/reference/core/servers/configure/site-configuration-server-wmi-classes.md)
