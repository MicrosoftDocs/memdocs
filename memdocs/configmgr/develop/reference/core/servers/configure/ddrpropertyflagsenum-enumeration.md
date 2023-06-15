---
description: Learn how to use the DDRPropertyFlagsEnum enumeration in Configuration Manager which specifies flags that are used by ISMSResGen.
title: DDRPropertyFlagsEnum Enumeration
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: ab94d236-9868-4feb-a75d-5be49758b394
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# DDRPropertyFlagsEnum Enumeration
The `DDRPropertyFlagsEnum` enumeration, in Configuration Manager, specifies flags that are used by `ISMSResGen`.  

## Syntax  

```  
enum DDRPropertyFlagsEnum  
{  
    ADDPROP_NONE = 0x0,  
    ADDPROP_GUID = 0x00000002,  
    ADDPROP_GROUPING = 0x00000004,  
    ADDPROP_KEY = 0x00000008,  
    ADDPROP_ARRAY = 0x00000010,   
    ADDPROP_AGENT = 0x00000020,  
    ADDPROP_NAME = 0x00000044,  
    ADDPROP_NAME2 = 0x00000084  
};  
```  

## Elements  
 ADDPROP_NONE(0x0)  
 No special properties.  

 ADDPROP_GUID(0x00000002)  
 Defines this property as being a GUID.  

 ADDPROP_GROUPING(0x00000004)  
 Reserved.  

 ADDPROP_KEY(0x00000008)  
 Defines this property as being a Key value that must be unique.  

 ADDPROP_ARRAY(0x00000010)  
 Reserved.  

 ADDPROP_AGENT(0x00000020)  
 Reserved.  

 ADDPROP_NAME(0x00000044)  
 Specifies this property as the actual `Name` property in the resource.  

 ADDPROP_NAME2(0x00000084)  
 Specifies this property as the actual `Comment` property in the resource.  

## Requirements  

## Runtime Requirements  
 smsrsgenctl.dll  

 smsrsgen.dll  

 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMSResGen COM Automation Class](../../../../../develop/reference/core/servers/configure/smsresgen-com-automation-class.md)   
 [DDRAddStringArray](../../../../../develop/reference/core/servers/configure/ddraddstringarray.md)   
 [DDRAddIntegerArray](../../../../../develop/reference/core/servers/configure/ddraddintegerarray.md)   
 [DDRAddInteger](../../../../../develop/reference/core/servers/configure/ddraddinteger.md)   
 [DDRNew](../../../../../develop/reference/core/servers/configure/ddrnew.md)   
 [DDRWrite](../../../../../develop/reference/core/servers/configure/ddrwrite.md)   
 [DDRAddString](../../../../../develop/reference/core/servers/configure/ddraddstring.md)   
 [SMSResGen COM Automation Class](../../../../../develop/reference/core/servers/configure/smsresgen-com-automation-class.md)   
 [ISMSResGen Interface](../../../../../develop/reference/core/servers/configure/ismsresgen-interface.md)
