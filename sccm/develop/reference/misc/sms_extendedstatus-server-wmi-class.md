---
title: "SMS_ExtendedStatus Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: ab4e741a-2a0a-4b08-aa47-42bfb9dd94ed
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_ExtendedStatus Server WMI Class
The `SMS_ExtendedStatus` Windows Management Instrumentation (WMI) class, in Configuration Manager, supports an error object that supplies the cause and nature of the current error.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ExtendedStatus : __ExtendedStatus  
{  
     String CauseInfo;  
     String Description;  
     UInt32 ErrorCode;  
     String File;  
     UInt32 Line;  
     String ObjectInfo;  
     String Operation;  
     String ParameterInfo;  
     String ProviderName;  
     String SQLMessage;  
     UInt32 SQLSeverity;  
     UInt32 SQLStatus;  
     UInt32 StatusCode;  
};  
```  

## Methods  
 The `SMS_ExtendedStatus` class does not define any methods.  

## Properties  
 `CauseInfo`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Optional error information. This property can contain the reason the error occurred, along with other information. For example, Software Product Compliance sets this property to the field number that caused the error.  

 `Description`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Optional detailed description of an error or an operational status.  

 `ErrorCode`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Composite error code that defines the severity, facility, action, object, and reason for the error. The Ssperrcode.h header file contains macros to evaluate the error condition. The following table lists the five-bit field masks that make up this property. The default value is 0.  

|Mask|Description|  
|----------|-----------------|  
|Severity (bits 31-30)|Value that identifies whether the application can continue and to what extent it can continue. The three levels of severity are functional, minor, and major.<br /><br /> A functional error allows an application to continue with any aspect of Configuration Manager.<br /><br /> A minor error allows an application to continue with other areas of Configuration Manager that are not related to the area that caused this error.<br /><br /> If the application receives a major error, however, it should stop processing requests and terminate.|  
|Facility (bits 27-22)|The facility that was being accessed when the error occurred, for example, internal, file, Structured Query Language (SQL), or security.|  
|Action (bits 21-16)|The action that failed, for example, open, read, or persist.|  
|Object (bits 15-8)|The type of object against which the action was being performed, for example, a parameter or an instance.|  
|Reason (bits 7-0)|The reason for the failure. This value might not be set. For example, R_PDFERROR is set if an error occurred while loading a package definition file (.pdf).|  

 `File`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Module that raised the error condition. The default value is "".  

 `Line`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Line number inside the module where the error was raised. The default value is 0.  

 `ObjectInfo`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Optional error information that contains the object that caused the error, the parameter that caused the error, or the Structured Query Language (SQL) message text, along with other data. For example, Software Product Compliance sets this property to the number of the record that caused the error.  

 `Operation`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Operation taking place at the time of the failure or anomaly.  

 `ParameterInfo`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 One or more parameters involved in the error or status change.  

 `ProviderName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The name of the provider that caused or reported the error or status change. If a provider was not involved, this string is set to "Windows Management".  

 `SQLMessage`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Error message text of the last SQL error. This property is set to `null` if no SQL error is present.  

 `SQLSeverity`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Severity code of the last SQL error. This property is set to `null` if no SQL error is present.  

 `SQLStatus`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Error code of the last SQL error. This property is set to `null` if no SQL error is present.  

 `StatusCode`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Error or information code for an operation.  

## Remarks  
 Class qualifiers for this class include:  

-   Read (read-only)  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

 For information about how to use this class, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Supporting Classes](../../../develop/reference/misc/supporting-server-wmi-classes.md)   
 [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md)
