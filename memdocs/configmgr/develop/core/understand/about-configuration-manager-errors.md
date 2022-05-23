---
title: "Configuration Manager Errors"
ms.date: "09/20/2016"
description: "In Configuration Manager, when a Configuration Manager error occurs it is either a Windows Management Instrumentation (WMI) or a SMS Provider error."
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: a8e24656-4cad-4494-9c01-99ec904b7025
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# About Configuration Manager Errors
In Configuration Manager, when a Configuration Manager error occurs it is either a Windows Management Instrumentation (WMI) or a SMS Provider error.  

 A WMI error is reported in an instance of __ExtendedStatus. An SMS Provider error is reported in an instance of `SMS_ExtendedStatus`.  

 How you process an error depends on the programming language that you are using.  

## Error Handling with WMI  
 In VBScript the error object `Number` property is non-zero if an error occurs during synchronous operation. Typically, you check this value after making changes to, or querying, the SMS Provider. In an asynchronous operation you receive an error object of the `OnCompleted` callback function.  

 After you get the error object instance, you can check the __Class property to determine the origin of the error. WMI creates an instance of \__ExtendedStatus for WMI errors, and the SMS Provider creates an instance of `SMS_ExtendedStatus` for SMS Provider errors. `SMS_ExtendedStatus` is derived from \__ExtendedStatus. The details of an SMS Provider error can also be found in SMSProv.log.  

 For more information see, [How to Handle Configuration Manager Synchronous Errors by Using WMI](../../../develop/core/understand/how-to-handle-configuration-manager-synchronous-errors-by-using-wmi.md).  

 [How to Handle Configuration Manager Asynchronous Errors by Using WMI](../../../develop/core/understand/how-to-handle-configuration-manager-asynchronous-errors-by-using-wmi.md).  

## Error Handling with the Managed SMS Provider  
 To handle Configuration Manager errors by using the managed SMS Provider, you catch the Configuration Manager-specific exceptions.  

|Exception|Description|  
|---------------|-----------------|  
|`SmsQueryException`|`SmsQueryException` is raised when a Configuration Manager query error occurs. It provides exception information specific to Configuration Manager (`SMS_ExtendedStatus`) and also encapsulates any WMI exceptions raised.<br /><br /> `SmsQueryException.ErrorCode` maps to the equivalent System.ManagementException exception code.<br /><br /> `SmsQueryException.ExtendStatusCode` maps to the SMS Provider error code raised in `SMS_ExtendedStatus.ErrorCode`.|  
|`SmsConnectionException`|`SmsConnectionException` is raised when the connection to WMI is lost.|  
|`SmsException`|`SmsException` is the base class from which `SmsQueryException` and `SmsConnectionException` derive. It is never raised but can be caught to catch both `SmsQueryException` and `SmsConnectionException`.|  

### Accessing the __ExtendedStatus and the SMS_ExtendedStatus objects  
 Because the __ExtendedStatus and `SMS_ExtendedStatus` are not wrapped by the managed SMS Provider, you must use the System.Management ManagedException object.  

 If you do not need access to the error WMI objects, you can get access to an exception details string in SMSException.Details.  

 For more information about handling synchronous exceptions, see [How to Handle Configuration Manager Synchronous Errors by Using Managed Code](../../../develop/core/understand/how-to-handle-configuration-manager-synchronous-errors-by-using-managed-code.md).  

 For more information about handling asynchronous exceptions, see [How to Handle Configuration Manager Asynchronous Errors by Using Managed Code](../../../develop/core/understand/how-to-handle-configuration-manager-asynchronous-errors-by-using-managed-code.md).  

## See Also  
 [About errors](about-configuration-manager-errors.md)
 [How to Handle Configuration Manager Synchronous Errors by Using WMI](../../../develop/core/understand/how-to-handle-configuration-manager-synchronous-errors-by-using-wmi.md)   
 [How to Handle Configuration Manager Asynchronous Errors by Using WMI](../../../develop/core/understand/how-to-handle-configuration-manager-asynchronous-errors-by-using-wmi.md)   
 [Configuration Manager Asynchronous Errors by Using Managed Code](../../../develop/core/understand/how-to-handle-configuration-manager-asynchronous-errors-by-using-managed-code.md)   
 [How to Handle Configuration Manager Synchronous Errors by Using Managed Code](../../../develop/core/understand/how-to-handle-configuration-manager-synchronous-errors-by-using-managed-code.md)
