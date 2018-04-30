---
title: "GetReportPointInfo Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: e8c328eb-87c7-4ee0-96a5-6bd02b49f776
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# GetReportPointInfo Method in Class SMS_Report
The `GetReportPointInfo` Windows Management Instrumentation (WMI) class method, in Configuration Manager, gets report point information.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 GetReportPointInfo(  
   String SiteCode,  
   UInt32 InstanceCount,  
   String NALPaths[],  
   String RPFolders[],  
   UInt32 Protocols[],  
   UInt32 PortNumbers[],  
   String ServerRemoteNames[]  
);  
```  

#### Parameters  
 `SiteCode`  
 Data type: `String`  

 Qualifiers: [in, SizeLimit("3")]  

 The site code of the site.  

 `InstanceCount`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 Count of objects for which to retrieve report point information.  

 `NALPaths`  
 Data type: `String` Array  

 Qualifiers: [out]  

 NAL paths to resources associated with the report point information.  

 `RPFolders`  
 Data type: `String` Array  

 Qualifiers: [out]  

 Folders containing report point information.  

 `Protocols`  
 Data type: `UInt32` Array  

 Qualifiers: [out]  

 Communication protocols used by the report point information.  

 `PortNumbers`  
 Data type: `UInt32` Array  

 Qualifiers: [out]  

 Port numbers used by the report point information.  

 `ServerRemoteNames`  
 Data type: `String` Array  

 Qualifiers: [out]  

 Server remote names used by the report point information.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Report Server WMI Class](../../../develop/reference/misc/sms_report-server-wmi-class.md)
