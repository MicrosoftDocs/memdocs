---
title: Create an Object by Using WMI
titleSuffix: Configuration Manager
description: Create a Configuration Manager object by calling the SWbemObject object SpawnInstance_ method.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: how-to
ms.assetid: c52cf79a-45d7-45c8-b8f2-5610d06b38e0
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# How to Create a Configuration Manager Object by Using WMI
You create a Configuration Manager object, in Configuration Manager, by calling the [SWbemObject](/windows/win32/wmisdk/swbemobject) object [SpawnInstance_](/windows/win32/wmisdk/swbemobject-spawninstance-) method.  

 The [SWbemObject](/windows/win32/wmisdk/swbemobject) is the class definition for the object type that you want to create. For example, [SMS_Package](../../../develop/reference/core/servers/configure/sms_package-server-wmi-class.md). You get the [SWbemObject](/windows/win32/wmisdk/swbemobject) by calling the [SWBemServices](/windows/win32/wmisdk/swbemservices) object [Get](/windows/win32/wmisdk/swbemservices-get) method.  

### To create a Configuration Manager object  

1.  Set up a connection to the SMS Provider. For more information, see [How to Connect to an SMS Provider in Configuration Manager by Using WMI](../../../develop/core/understand/how-to-connect-to-an-sms-provider-in-configuration-manager-by-using-wmi.md).  

2.  Using the [SWBemServices](/windows/win32/wmisdk/swbemservices) object you obtain from step one, call [Get](/windows/win32/wmisdk/swbemservices-get) to get the [SWbemObject](/windows/win32/wmisdk/swbemobject) for the Configuration Manager object class definition.  

3.  Call [SpawnInstance_](/windows/win32/wmisdk/swbemobject-spawninstance-) on the SWbemObject to create the new object. An SWbemObject is returned for the new object.  

4.  Using the SWbemObject returned from the call to SpawnInstance, populate the object properties.  

5.  Call [Put_](/windows/win32/wmisdk/swbemobject-put-) to commit the new object to the SMS Provider.  

## Example  
 The following VBScript code example creates an [SMS_Package](../../../develop/reference/core/servers/configure/sms_package-server-wmi-class.md) object.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Sub CreatePackage (connection)  

    On Error Resume Next  

    ' Create a package object.  
    Set package = connection.Get("SMS_Package").SpawnInstance_()  

    If Err.Number<>0 Then  
        Wscript.Echo "Couldn't create packages object"  
        Exit Sub  
    End If  

    ' Populate the object.  
    package.Name = "Test Package"  
    package.Description = "A test package"  
    package.PkgSourceFlag = 2  
    package.PkgSourcePath = "C:\temp"  

    package.Put_  

    If Err.Number<>0 Then  
        Wscript.Echo "Couldn't commit the package"  
        Exit Sub  
    End If  

    WScript.Echo "Package created"  
End Sub  
```  

 This example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`Connection`|[SWBemServices](/windows/win32/wmisdk/swbemservices)|A valid connection to the SMS Provider.|  

## Compiling the Code  

## See Also  
 [Windows Management Instrumentation](/windows/win32/wmisdk/wmi-start-page)   
 [Objects overview](configuration-manager-objects-overview.md)
 [How to Call a Configuration Manager Object Class Method by Using WMI](../../../develop/core/understand/how-to-call-a-configuration-manager-object-class-method-by-using-wmi.md)   
 [How to Connect to an SMS Provider in Configuration Manager by Using WMI](../../../develop/core/understand/how-to-connect-to-an-sms-provider-in-configuration-manager-by-using-wmi.md)   
 [How to Delete a Configuration Manager Object by Using WMI](../../../develop/core/understand/how-to-delete-a-configuration-manager-object-by-using-wmi.md)   
 [How to Modify a Configuration Manager Object by Using WMI](../../../develop/core/understand/how-to-modify-a-configuration-manager-object-by-using-wmi.md)   
 [How to Perform an Asynchronous Configuration Manager Query by Using WMI](../../../develop/core/understand/how-to-perform-an-asynchronous-configuration-manager-query-by-using-wmi.md)   
 [How to Perform a Synchronous Configuration Manager Query by Using WMI](../../../develop/core/understand/how-to-perform-a-synchronous-configuration-manager-query-by-using-wmi.md)   
 [How to Read a Configuration Manager Object by Using WMI](../../../develop/core/understand/how-to-read-a-configuration-manager-object-by-using-wmi.md)   
 [How to Read Lazy Properties by Using WMI](../../../develop/core/understand/how-to-read-lazy-properties-by-using-wmi.md)
