---
title: "SMS_ActiveSyncService Class"
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
ms.assetid: 892689e8-48df-4cf6-918b-95c3049387a7searchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_ActiveSyncService Client WMI Class
The `SMS_ActiveSyncService` class is a client Windows Management Instrumentation (WMI) class, in Configuration Manager, that represents the ActiveSync service on the client.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ActiveSyncService : SMS_Class_Template  
{  
      String LastSyncTime;  
      UInt32 MajorVersion;  
      UInt32 MinorVersion;  
};  
```  

## Methods  
 The `SMS_ActiveSyncService` class does not define any methods.  

## Properties  
 `LastSyncTime`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers:  

 [SMS_Report("True")]  

 The last time when the client was synchronized with connected devices.  

 `MajorVersion`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [SMS_Report("True"), key]  

 The major version number of the client operating system.  

 `MinorVersion`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [SMS_Report("True"), key]  

 The minor version number of the client operating system.  

## Remarks  
 All properties of this class are marked with qualifiers to indicate that they represent items that are generated dynamically (reported) based on the content of the SMS_def.mof file. For more information, see the `DrillThroughReportPath` property of [SMS_Report Server WMI Class](../../../../../develop/reference/misc/sms_report-server-wmi-class.md).  

## See Also  
 [Device Management Client WMI Classes](../../../../../develop/reference/core/clients/client-classes/device-management-client-wmi-classes.md)   
 [SMS_ActiveSyncConnectedDevice Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_activesyncconnecteddevice-client-wmi-class.md)
