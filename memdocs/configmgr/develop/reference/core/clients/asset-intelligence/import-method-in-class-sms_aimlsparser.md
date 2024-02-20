---
title: Import Method
titleSuffix: Configuration Manager
description: A Windows Management Instrumentation class method that imports the MLS statement as specified by the MLSFilepath parameter into the Configuration Manager database.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 384ee719-c047-49a3-9847-5df0e443245f
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# Import Method in Class SMS_AIMLSParser
The `Import` Windows Management Instrumentation (WMI) class method, in Configuration Manager, imports the MLS statement as specified by the `MLSFilepath` parameter (in UNC format) into the Configuration Manager database.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 Import(      
     String MLSFilepath,  
     UInt32 Flags  
);  
```  

#### Parameters  
 `MLSFilepath`  
 Data type: `String`  

 Qualifiers: [in]  

 The UNC path of the .csv file to be imported.  

 `Flags`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 Specifies the type of data the .csv file contains, specified by the `MLSFilepath` property.  

|Value|Description|  
|-----------|-----------------|  
|0|Microsoft licenses.|  
|Non 0|Any non-Microsoft licenses.|  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_AIMLSParser Server WMI Class](../../../../../develop/reference/core/clients/asset-intelligence/sms_aimlsparser-server-wmi-class.md)
