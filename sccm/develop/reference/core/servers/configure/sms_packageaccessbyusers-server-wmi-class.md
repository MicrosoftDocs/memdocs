---
title: "SMS_PackageAccessByUsers Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 38fb7c0d-8420-4602-8b8d-3fa74e8df0d8
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_PackageAccessByUsers Server WMI Class
The `SMS_PackageAccessByUsers` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that controls which users are granted access rights to a package folder or to distribution points.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_PackageAccessByUsers : SMS_BaseClass  
{  
      UInt32 Access;  
      String PackageID;  
      String UserName;  
};  
```  

## Methods  
 The `SMS_PackageAccessByUsers` class does not define any methods.  

## Properties  
 `Access`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers:  

 [bits]  

 Access rights for the user. Possible values are listed below. The default value is 0x65.  

|||  
|-|-|  
|0|READ|  
|1|WRITE|  
|2|EXECUTE|  
|3|CREATE|  
|4|DELETE|  
|5|VIEW_FOLDERS|  
|6|VIEW_FILES|  
|7|CHANGE_PERMISSIONS|  
|8|CHANGE_ATTRIBUTES|  

 `PackageID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 ID of the package to which the privileges apply. The default value is "".  

 `UserName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 User name or group name in the network abstraction layer (NAL) path format. The default value is "". For more information about the NAL path format, see `PackNALPath`.  

## Remarks  
 There are no special class qualifiers for this class. For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

 This class controls client access to package folders and distribution points by using Windows NT or Novell security.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Software Distribution Server WMI Classes](../../../../../develop/reference/core/servers/configure/software-distribution-server-wmi-classes.md)
