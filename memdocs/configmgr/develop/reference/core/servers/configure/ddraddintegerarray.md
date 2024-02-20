---
title: DDRAddIntegerArray
titleSuffix: Configuration Manager
description: The DDRAddIntegerArray function, in Configuration Manager, adds an integer array property to the data discovery record (DDR).
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: a3f9f0ae-4225-47b1-8153-8a47eb53d75d
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# DDRAddIntegerArray
The `DDRAddIntegerArray` function, in Configuration Manager, adds an integer array property to the data discovery record (DDR).  

## Syntax  

```  
[IDL]  
HRESULT DDRAddIntegerArray();  
```  

#### Parameters  
 `Name`  
 Name of the class property.  

 `Array`  
 Array of integers assigned to the property.  

 `Flags`  
 Characteristics of the property, such as identifying this property as a key field for comparisons. Enter the following flag or a zero.  

|Flag|Description|  
|----------|-----------------|  
|ADDPROP_KEY (Hexadecimal 8)|Identifies this property as a key field during a comparison of this DDR with class instances in the database. If an instance in the database matches the data of the DDR key properties, the instance is updated; otherwise, a new instance is created.|  

## Return Values  
 If the function succeeds, the return value is S_OK.  

 If the [DDRNew](../../../../../develop/reference/core/servers/configure/ddrnew.md) function has not been called, the return value is S_FALSE.  

## Requirements  

## Runtime Requirements  
 smsrsgenctl.dll  

 smsrsgen.dll  

 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [DDRAddInteger](../../../../../develop/reference/core/servers/configure/ddraddinteger.md)   
 [DDRAddStringArray](../../../../../develop/reference/core/servers/configure/ddraddstringarray.md)   
 [DDRPropertyFlagsEnum Enumeration](../../../../../develop/reference/core/servers/configure/ddrpropertyflagsenum-enumeration.md)   
 [SMSResGen COM Automation Class](../../../../../develop/reference/core/servers/configure/smsresgen-com-automation-class.md)   
 [ISMSResGen Interface](../../../../../develop/reference/core/servers/configure/ismsresgen-interface.md)
