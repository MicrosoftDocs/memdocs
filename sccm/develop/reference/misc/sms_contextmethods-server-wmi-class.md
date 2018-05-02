---
title: "SMS_ContextMethods Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 92b831f5-d232-4c63-b5fe-0565d07cad83
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_ContextMethods Server WMI Class
The `SMS_ContextMethods` Windows Management Instrumentation (WMI) class is an abstract class, in Configuration Manager, that contains methods for caching WMI context qualifiers with the SMS Provider.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ContextMethods ();  
```  

## Methods  
 The following table lists the methods in `SMS_ContextMethods`.  

|Term|Description|  
|----------|-----------------|  
|[ClearContextHandle Method in Class SMS_ContextMethods](../../../develop/reference/misc/clearcontexthandle-method-in-class-sms_contextmethods.md)|Releases cached context data.|  
|[GetContextHandle Method in Class SMS_ContextMethods](../../../develop/reference/misc/getcontexthandle-method-in-class-sms_contextmethods.md)|Caches multiple context qualifiers within the SMS Provider. This allows applications to use a much smaller context object when making API calls to WMI.|  

## Properties  
 The `SMS_ContextMethods` class does not define any properties.  

## Remarks  
 Class qualifiers for this class include:  

-   Abstract  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Supporting Classes](../../../develop/reference/misc/supporting-server-wmi-classes.md)   
 [Configuration Manager Context Qualifiers](../../../develop/core/understand/context-qualifiers.md)
