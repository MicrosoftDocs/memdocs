---
title: "SMS_OS_Details Class"
titleSuffix: "Configuration Manager"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: 1be82e7a-bb57-4ffa-a5c6-96c7f9739761searchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_OS_Details Server WMI Class
The `SMS_OS_Details` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in System Center Configuration Manager, that describes the supported platforms (operating system, architecture, and versions) on which a program can run.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_OS_Details  
{  
      String MaxVersion;  
      String MinVersion;  
      String Name;  
      String Platform;  
};  
```  

## Methods  
 The `SMS_OS_Details` class does not define any methods.  

## Properties  
 `MaxVersion`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The maximum operating system version of the range that is described by this class. The default value is "".  

 `MinVersion`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The minimum operating system version of the range described by this class. The default value is "".  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The name of the operating system. The default value is "".  

 `Platform`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The hardware platform on which the operating system runs.  

## Remarks  
 Class qualifiers for this class include:  

-   Embedded  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

 The values you specify in this class must come from the [SMS_SupportedPlatforms Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_supportedplatforms-server-wmi-class.md) class.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Software Distribution Server WMI Classes](../../../../../develop/reference/core/servers/configure/software-distribution-server-wmi-classes.md)   
 [SMS_Program Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_program-server-wmi-class.md)   
 [How to Modify the Supported Platforms for a Program](../../../../../develop/core/servers/configure/how-to-modify-the-supported-platforms-for-a-program.md)
