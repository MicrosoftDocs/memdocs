---
title: "SMS_CollectionVariable Class"
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
ms.assetid: 8950faec-bcc1-48a5-93f0-93f7a3d363fesearchScope: - ConfigMgr SDK
caps.latest.revision: 9
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_CollectionVariable Server WMI Class
The `SMS_CollectionVariable` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a collection variable that is accessible at the time of task execution.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_CollectionVariable  
{  
      Boolean IsMasked;  
      String Name;  
      String Value;  
};  
```  

## Methods  
 The `SMS_CollectionVariable` class does not define any methods.  

## Properties  
 `IsMasked`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 This value should be set to `true` if the collection variable contains a sensitive value such as a password. If the value is set to `true`, the SMS Provider treats this property as write-only and disallows reads. The default value is `false`.  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Collection variable name. The default value is "".  

 `Value`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Collection variable value. The default value is "".  

## Remarks  
 Class qualifiers for this class include:  

-   Embedded  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

 Collection variables are associated with collections as collection extended properties.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_CollectionSettings Server WMI Class](../../../develop/reference/core/clients/collections/sms_collectionsettings-server-wmi-class.md)
