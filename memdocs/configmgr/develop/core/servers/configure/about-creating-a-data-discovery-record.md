---
description: Learn how to create data discovery records (DDRs), using the SMSRsGenCtl.dll and other functions.
title: About Creating a Data Discovery Record
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: conceptual
ms.assetid: 21c55e40-fd35-421c-bdbe-49b673a99403
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# About Creating a Data Discovery Record
To create data discovery records (DDRs), you must use the SMSRsGenCtl.dll and the functions that are described in the following table. These functions create a single DDR that can be process by Data Discovery Manager (DDM). The order in which you call the functions is important; you must call `DDRNew` before calling any of the functions that add properties. The order in which you add properties to your class is arbitrary. However, the last function you call must be `DDRWrite` to create the DDR. The DDR must then be manually copied to the SMS\Inboxes\Auth\Ddm.box directory.  

 DDRs that fail to process are moved to the SMS\Inboxes\Ddm.box\Bad_ddrs directory. If you have logging turned on, you can view the DDM.log file for an explanation of the failure. After fixing the source of the errors, you can rerun your program to load the DDR.  

 C programmers can use the SMSRsGen.dll file to access the DDR functions. Visual Basic programmers can use the SMSRsGenCtl.dll to access the DDR methods. These methods have the same name and parameters as the C library functions.  

 Because the `SMSResGen` control is not thread safe, do not try to create more than one instance of the class.  

 The `SMSResGen` method has the following functions:  

> [!IMPORTANT]
>  The function `DDRSendToSMS`, available in previous releases of the SDK and in versions of `SMSRsGen.dll` and `SMSRsGenCtl.dll`, has been deprecated and should not be used with Configuration Manager.  

 [DDRNew](../../../../develop/reference/core/servers/configure/ddrnew.md)  
 Creates a new DDR.  

 [DDRAddInteger](../../../../develop/reference/core/servers/configure/ddraddinteger.md)  
 Adds an integer property to the DDR.  

 [DDRAddString](../../../../develop/reference/core/servers/configure/ddraddstring.md)  
 Adds a string property to the DDR.  

 [DDRAddIntegerArray](../../../../develop/reference/core/servers/configure/ddraddintegerarray.md)  
 Adds an integer array property to the DDR.  

 [DDRAddStringArray](../../../../develop/reference/core/servers/configure/ddraddstringarray.md)  
 Adds a string array property to the DDR.  

 [DDRWrite](../../../../develop/reference/core/servers/configure/ddrwrite.md)  
 Writes the DDR to a file.  

## See Also  
 [Configuration Manager SDK](../../../../develop/core/misc/system-center-configuration-manager-sdk.md)   
 [SMSResGen COM Automation Class](../../../../develop/reference/core/servers/configure/smsresgen-com-automation-class.md)
