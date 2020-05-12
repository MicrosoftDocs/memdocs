---
title: "GetCIDocuments Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 72f9b56c-4556-49d2-9d18-02ba7d3c1d8e
author: aczechowski
ms.author: aaroncz
manager: dougeby


---
# GetCIDocuments Method in Class SMS_Application
The `GetCIDocuments` Windows Management Instrumentation (WMI) class method, in Configuration Manager, gets all of the configuration item documents for the application installation.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
sint32 GetCIDocuments (  
     uint32  DocCIID[],  
     string DocumentID[],  
     string DocumentType[]  
);  
```  

#### Parameters  
 `DocCIID`  
 Data type: `UInt32` Array  

 Qualifiers: [out]  

 Configuration item ID of the documents.  

 `DocumentID`  
 Data type: `String` Array  

 Qualifiers: [out]  

 Document ID list.  

 `DocumentType`  
 Data type: `String` Array  

 Qualifiers: [out]  

 Type of document. Possible values are:  

|||  
|-|-|  
|1|Represent a manifest document.|  
|2|Represents a properties document.|  
|3|Represents a policy document that is the latest version configuration item.|  
|-3|Represents a policy document that is not the latest version configuration item.|  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Application Server WMI Class](../../../develop/reference/apps/sms_application-server-wmi-class.md)   
