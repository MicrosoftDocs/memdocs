---
title: "DDRAddStringArray"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 2763cae0-56ae-4ea0-8654-fcc95613831b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth
description: Learn how the DDRAddStringArray function, in Configuration Manager, adds a string array property to the data discovery record.


---
# DDRAddStringArray
The `DDRAddStringArray` function, in Configuration Manager, adds a string array property to the data discovery record (DDR).  

## Syntax  

```  
[IDL]  
HRESULT DDRAddStringArray();  
```  

#### Parameters  
 `sName`  
 Name of the class property.  

 `sArray`  
 Array of strings assigned to the property. You can only enter string values from the single-byte character set.  

 `nArraySize`  
 Number of elements in `sArray`.  

 `nSQLWidth`  
 Maximum length of a string that can be assigned to this property. This value does not include the NULL character. For SMS 2003, this value cannot be greater than 900 characters. For SMS 2.0, this value cannot be greater than 255 characters.  

 `dwFlags`  
 Characteristics of the property, such as a key field used for comparisons. Enter the following flag or a zero.  

|Flag|Description|  
|----------|-----------------|  
|ADDPROP_KEY (Hexadecimal 8)|Identifies this property as a key field during a comparison of this DDR with class instances in the database. If an instance in the database matches the data of the DDR key properties, the instance is updated; otherwise, a new instance is created.|  

## Return Values  
 If the function succeeds, the return value is S_OK.  

 If the [DDRNew](../../../../../develop/reference/core/servers/configure/ddrnew.md) function has not been called, the return value is S_FALSE.  

## Remarks  
 Strings longer than the maximum length specified in `nSQLWidth` are truncated.  

 You can use underscores, concatenation, or spaces for property names that contain multiple words. For example, you can specify `sName` as `License_Number`, `LicenseNumber`, or `LicenseNumber`. If you specify `sName` as `LicenseNumber`, the Data Discovery Manager (DDM) concatenates the words, which results in `LicenseNumber`. However, the column name, which is created in the database, is `License_Number`. You must use the same convention when you add DDRs that create or update instances in an existing resource class.  

## Requirements  

## Runtime Requirements  
 smsrsgenctl.dll  

 smsrsgen.dll  

 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [DDRAddIntegerArray](../../../../../develop/reference/core/servers/configure/ddraddintegerarray.md)   
 [DDRAddString](../../../../../develop/reference/core/servers/configure/ddraddstring.md)   
 [DDRPropertyFlagsEnum Enumeration](../../../../../develop/reference/core/servers/configure/ddrpropertyflagsenum-enumeration.md)   
 [SMSResGen COM Automation Class](../../../../../develop/reference/core/servers/configure/smsresgen-com-automation-class.md)
