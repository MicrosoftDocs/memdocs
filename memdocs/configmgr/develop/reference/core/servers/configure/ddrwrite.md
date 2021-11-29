---
title: "DDRWrite"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 818ce2a2-5f8d-44c4-80f8-9683074c2508
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# DDRWrite
The `DDRWrite` function, in Configuration Manager, writes the data discovery records (DDRs) to a file.  

## Syntax  

```  
[IDL]  
HRESULT DDRWrite();  
```  

#### Parameters  
 `FileName`  
 Valid Universal Naming Convention (UNC) file name. Use the .ddr file name extension when you specify the file name.  

## Return Values  
 If the function succeeds, the return value is S_OK.  

 If the [DDRNew](../../../../../develop/reference/core/servers/configure/ddrnew.md) function has not been called or a file error occurs, the return value is S_FALSE.  

## Remarks  
 Calling `DDRWrite` completes the DDR and writes the record to a binary file. The DDR must be copied to the Data Discovery Manager (DDM) inbox on the site server at a later time (SMS\Inboxes\Auth\Ddm.box).  

## Requirements  

## Runtime Requirements  
 smsrsgenctl.dll  

 smsrsgen.dll  

 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [DDRPropertyFlagsEnum Enumeration](../../../../../develop/reference/core/servers/configure/ddrpropertyflagsenum-enumeration.md)   
 [SMSResGen COM Automation Class](../../../../../develop/reference/core/servers/configure/smsresgen-com-automation-class.md)   
 [ISMSResGen Interface](../../../../../develop/reference/core/servers/configure/ismsresgen-interface.md)
