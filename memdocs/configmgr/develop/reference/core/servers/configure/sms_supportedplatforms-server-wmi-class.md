---
description: Learn how to represent the platforms that Configuration Manager supports using the SMS_SupportedPlatforms.
title: "SMS_SupportedPlatforms Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 72421b75-2201-401e-ac74-1dd0bbb20d97
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_SupportedPlatforms Server WMI Class
The `SMS_SupportedPlatforms` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the platforms (operating system, architecture, and versions) that Configuration Manager supports.  

## Syntax  

```  
Class SMS_SupportedPlatforms : SMS_BaseClass  
{  
      String CI_UniqueID;  
      String Condition;  
      String DisplayText;  
      Boolean IsSupported;  
      String OSMaxVersion;  
      String OSMinVersion;  
      String OSName;  
      String OSPlatform;  
      String ResourceDll;  
      UInt32 StringId;  
};  
```  

## Methods  
 The following table lists the methods in the `SMS_SupportedPlatforms` class.  

|Method|Description|  
|------------|-----------------|  
|[Enable Method in Class SMS_SupportedPlatforms](../../../../../develop/reference/core/servers/configure/enable-method-in-class-sms_supportedplatforms.md)|Enables or disables the platforms.|  

## Properties  
 `CI_UniqueID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The unique ID of the Configuration Item that defines the platform rules.  

 `Condition`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The XML data that specifies the WQL that the client uses to check the supported platforms.  

 `DisplayText`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Name of the platform that humans can read. It is used if the resource string does not exist.  

 `IsSupported`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true`, if the platform is supported as client operating system.  

 `OSMaxVersion`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key, Not_null]  

 Highest version number for the platform. A version of 99.99.9999.9999 denotes all future versions.  

 `OSMinVersion`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key, Not_null]  

 Lowest version number for the platform. A version of 0.00.0000.0 denotes all previous versions.  

 `OSName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key, Not_null]  

 Name of the operating system for the platform, for example, "Win NT".  

 `OSPlatform`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key, Not_null]  

 Name of the computer architecture for the platform, for example, I386.  

 `ResourceDll`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Name of the resource DLL containing the localized name of the platform.  

 `StringId`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 String ID in the resource DLL containing the localized name of the platform.  

## Remarks  
 There are no special class qualifiers for this class. For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

 This class is populated when Configuration Manager is installed. Your application cannot add, update, or delete instances of this class by using WMI. However, new instances are added to the class when a package definition file is processed that contains a platform that is not identified by a class instance.  

 Your application uses the information contained in this class to populate `SMS_OS_Details` objects. For more information, see the `SupportedOperatingSystems` property of [SMS_Program Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_program-server-wmi-class.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_OS_Details Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_os_details-server-wmi-class.md)   
 [SMS_Program Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_program-server-wmi-class.md)
