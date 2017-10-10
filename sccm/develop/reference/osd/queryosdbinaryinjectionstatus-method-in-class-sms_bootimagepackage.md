---
title: "QueryOSDBinaryInjectionStatus Method"
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
ms.assetid: 8c89cda5-5f27-4729-932a-e351969b3db1searchScope: - ConfigMgr SDK
caps.latest.revision: 8
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# QueryOSDBinaryInjectionStatus Method in Class SMS_BootImagePackage
The `QueryOSDBinaryInjectionStatus` Windows Management Instrumentation (WMI) class method, in Configuration Manager, queries the current status of the injection of operating system deployment binaries into a boot image.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 QueryOSDBinaryInjectionStatus(  
     String ContextID,  
     UInt32 Status,  
     UInt32 Progress,  
     UInt32 MaxProgress,  
     String ProgressText,  
     SInt32 ErrorCode,  
     String ExtendedErrorInfo  
);  
```  

#### Parameters  
 `ContextID`  
 Data type: `String`  

 Qualifiers: [in]  

 The ID of the context (index) optionally associated with the status upon import of a boot image. This ID is indicated by the `ContextID` property of [SMS_BootImagePackage Server WMI Class](../../../develop/reference/osd/sms_bootimagepackage-server-wmi-class.md).  

 `Status`  
 Data type: `UInt32`  

 Qualifiers: [out]  

 The current status of binary injection. Possible values are:  

|||  
|-|-|  
|0|Complete|  
|1|In progress|  
|2|Error|  
|3|No status|  

 `Progress`  
 Data type: `UInt32`  

 Qualifiers: [out]  

 The progress status indicating the number of the current step in the binary injection operation.  

 `MaxProgress`  
 Data type: `UInt32`  

 Qualifiers: [out]  

 The total number of steps in the binary injection operation.  

 `ProgressText`  
 Data type: `String`  

 Qualifiers: [out]  

 A user-readable string identifying the current progress of the binary injection operation.  

 `ErrorCode`  
 Data type: `SInt32`  

 Qualifiers: [out]  

 A 32-bit error code in case of an error in the binary injection operation. An example of an error code is FILE_NOT_FOUND (2). The log file contains error code details.  

 `ExtendedErrorInfo`  
 Data type: `String`  

 Qualifiers: [out]  

 Additional error information if the `ErrorCode` parameter is set to an error code. Currently this parameter is used to report driver file information if the binary injection operation fails to inject the binaries for a particular driver.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Remarks  
 To use the `QueryOSDBinaryInjectionStatus` method, your application must:  

1.  Establish a connection to the SMS Provider. For more information see, [About the SMS Provider in Configuration Manager](../../../develop/core/understand/about-the-sms-provider-in-configuration-manager.md).  

2.  Access the [SMS_BootImagePackage Server WMI Class](../../../develop/reference/osd/sms_bootimagepackage-server-wmi-class.md) object.  

3.  Call the [ExportDefaultBootImage Method in Class SMS_BootImagePackage](../../../develop/reference/osd/exportdefaultbootimage-method-in-class-sms_bootimagepackage.md).  

4.  Then call `QueryOSDBinaryInjectionStatus` as needed to find out the status of the binary injection operation.  

5.  Use the values of the `Progress` and `MaxProgress` parameters to determine the percent complete status of the binary injection operation.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_BootImagePackage Server WMI Class](../../../develop/reference/osd/sms_bootimagepackage-server-wmi-class.md)   
 [ExportDefaultBootImage Method in Class SMS_BootImagePackage](../../../develop/reference/osd/exportdefaultbootimage-method-in-class-sms_bootimagepackage.md)
