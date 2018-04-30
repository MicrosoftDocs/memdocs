---
title: "DeleteByQuery Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: d4417ea5-ce21-4659-a450-10a3e54efe9e
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# DeleteByQuery Method in Class SMS_SoftwareProductCompliance
The `DeleteByQuery` Windows Management Instrumentation (WMI) class method, in Configuration Manager, deletes records specified by a WQL SELECT statement that references the `SMS_SoftwareProductCompliance` class.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
UInt32 DeleteByQuery(  
     String WQLSelect  
);  
```  

#### Parameters  
 `WQLSelect`  
 Data type: `String`  

 Qualifiers: [in]  

 WQL SELECT statement that selects records to be deleted and must reference the `SMS_SoftwareProductCompliance` class. This sample SELECT statement deletes all records that specify non-English products.  

```  
SELECT * FROM SMS_SoftwareProductCompliance WHERE ResProdLangID NOT IN (1033, 0, 65535)  
```  

## Return Values  
 A `UInt32` data type indicating the number of objects deleted.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_SoftwareProductCompliance Server WMI Class](../../../develop/reference/misc/sms_softwareproductcompliance-server-wmi-class.md)
