---
title: "SMS_UserClassPermissions Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 840ce395-0fe8-47c4-815a-cf70367e32bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_UserClassPermissions Server WMI Class
The `SMS_UserClassPermissions` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a user's class-level permissions for a secured class.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_UserClassPermissions : SMS_BaseClass  
{  
      UInt32 ClassPermissions;  
      UInt32 ObjectKey;  
      String UserName;  
};  
```  

## Methods  
 The `SMS_UserClassPermissions` class does not define any methods.  

## Properties  
 `ClassPermissions`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers:  

 [bits]  

 Permissions granted to a user for a specific class. The default value is 0.  

|Bit|Decimal|Hexadecimal|Description|  
|---------|-------------|-----------------|-----------------|  
|0|1|0x00000001|READ|  
|1|2|0x00000002|MODIFY|  
|2|4|0x00000004|DELETE|  
|3|8|0x00000008|DISTRIBUTE|  
|4|16|0x00000010|Not used|  
|5|32|0x00000020|REMOTE_CONTROL|  
|6|64|0x00000040|ADVERTISE|  
|7|128|0x00000080|MODIFY_RESOURCE|  
|8|256|0x00000100|ADMINISTER|  
|9|512|0x00000200|DELETE_RESOURCE|  
|10|1024|0x00000400|CREATE|  
|11|2048|0x00000800|VIEW_COLL_FILE|  
|12|4096|0x00001000|READ_RESOURCE|  
|13|8192|0x00002000|DELEGATE|  
|14|16384|0x00004000|METER|  
|15|32768|0x00008000|MANAGESQLCOMMAND|  
|16|65536|0x00010000|MANAGESTATUSFILTER|  
|17|131072|0x00020000|MANAGEFOLDER|  
|18|262144|0x00040000|NETWORKACCESS|  
|19|524288|0x00080000|IMPORTMACHINE|  
|20|1048576|0x00100000|CREATETSMEDIA|  
|21|2097152|0x00200000|MODIFYCOLLECTIONSETTING|  
|22|4194304|0x00400000|MANAGEOSDCERTIFICATE|  
|23|8388608|0x00800000|RECOVERUSERSTATE|  
|24|16777216|0x01000000|MANAGEBMC|  
|25|33554432|0x02000000|VIEWBMC|  
|26|67108864|0x04000000|MANAGEAI|  
|27|134217728|0x08000000|VIEWAI|  

 `ObjectKey`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Numeric key that describes the type of secured object. See the `ObjectKey` property of [SMS_SecuredObject Server WMI Class](../../../develop/reference/misc/sms_securedobject-server-wmi-class.md).  

 `UserName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers:  

 [key]  

 Name of the user, including the domain name. The default value is "".  

## Remarks  
 There are no special class qualifiers for this class. For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_UserClassPermissionNames Server WMI Class](../../../develop/reference/misc/sms_userclasspermissionnames-server-wmi-class.md)
