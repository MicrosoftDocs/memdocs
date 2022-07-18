---
description: Learn how to use the ISMSResGen Interface to enable the creation of Data Discovery Records (DDR). This interface inherits from IDispatch.  
title: "ISMSResGen Interface"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 56a4b6d7-c9d1-4919-9954-5bc28618d862
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# ISMSResGen Interface
The `ISMSResGen` automation interface, in Configuration Manager, enables the creation of Data Discovery Records (DDR). This interface inherits from `IDispatch`.  

## In This Section  

|Term|Definition|  
|----------|----------------|  
|[DDRNew](../../../../../develop/reference/core/servers/configure/ddrnew.md)|Creates a new DDR.|  
|[DDRAddInteger](../../../../../develop/reference/core/servers/configure/ddraddinteger.md)|Adds an integer property to the DDR.|  
|[DDRAddString](../../../../../develop/reference/core/servers/configure/ddraddstring.md)|Adds a string property to the DDR.|  
|[DDRAddIntegerArray](../../../../../develop/reference/core/servers/configure/ddraddintegerarray.md)|Adds an integer array property to the DDR.|  
|[DDRAddStringArray](../../../../../develop/reference/core/servers/configure/ddraddstringarray.md)|Adds a string array property to the DDR.|  
|[DDRWrite](../../../../../develop/reference/core/servers/configure/ddrwrite.md)|Writes the DDR to a file.|  
|[DDRPropertyFlagsEnum Enumeration](../../../../../develop/reference/core/servers/configure/ddrpropertyflagsenum-enumeration.md)|Defines flags used by `ISMSResGen`.|  

## Remarks  
 These functions create a single DDR that is sent to the Data Discovery Manager (DDM). The order in which you call the functions is important; you must call `DDRNew` before calling any of the functions that add properties. However, the order in which you add properties to your class is arbitrary. The last function you call must be `DDRWrite` to create the DDR. The DDR must then be manually copied to the **SMS\Inboxes\Auth\Ddm.box** directory.  

 DDRs that fail to load are moved to the **SMS\Inboxes\Ddm.box\Bad_ddrs** directory. If you have logging turned on, you can view the DDM.log file for an explanation of the failure. After you fix the errors, you can rerun your program to load the DDR.  

 The IID for `ISMSResGen` is ECB65D0E-B16B-4817-92B0-BF2D9CEFB3AC.  

## Requirements  

### Runtime Requirements  
 smsrsgenctl.dll  

 smsrsgen.dll  

 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMSResGen COM Automation Class](../../../../../develop/reference/core/servers/configure/smsresgen-com-automation-class.md)
