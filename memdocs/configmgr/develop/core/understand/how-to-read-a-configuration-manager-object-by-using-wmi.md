---
title: "Read an Object by Using WMI"
titleSuffix: "Configuration Manager"
description: "In Configuration Manager, you read a Configuration Manager object by using the SWbemServices object Get method to return an object instance that is identified by a key value."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: 17017166-8b01-4a7d-99df-97be3bdda83f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# How to Read a Configuration Manager Object by Using WMI
In Configuration Manager, you read a Configuration Manager object by using the [SWbemServices](/windows/win32/wmisdk/swbemservices) object [Get](/windows/win32/wmisdk/swbemservices-get) method to return an object instance that is identified by a key value.  

> [!NOTE]
>  To query for multiple objects, use either a synchronous or asynchronous query. For more information, see [How to Perform a Synchronous Configuration Manager Query by Using Managed Code](../../../develop/core/understand/how-to-perform-a-synchronous-configuration-manager-query-by-using-managed-code.md)  

### To read a Configuration Manager object  

1.  Set up a connection to the SMS Provider. For more information, see [How to Connect to an SMS Provider in Configuration Manager by Using WMI](../../../develop/core/understand/how-to-connect-to-an-sms-provider-in-configuration-manager-by-using-wmi.md).  

2.  Using the SWbemServices object that you obtain from step 1, call the Get method and specify the class and key information for the object you want.  

## Example  
 The following VBScript code example function displays the name and description for a supplied key package identifier (`packageID`).  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Sub DisplayPackageName (connection, packageID)  

    On Error Resume Next   
    Dim package  

    Set package = connection.Get("SMS_Package.PackageID='" & packageID & "'")  
    If Err.Number<>0 Then  
        Wscript.Echo "Couldn't get package " + packageID  
        Exit Sub  
    End If  

    Wscript.Echo "Package Name: " + package.Name  
    Wscript.Echo "Package Description: " + package.Description  

End Sub  
```  

 This example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`connection`|[SWbemServices](/windows/win32/wmisdk/swbemservices)|A valid connection to the SMS Provider.|  
|`packageID`|`String`|A package identifier. This can be obtained from the [SMS_Package](../../../develop/reference/core/servers/configure/sms_package-server-wmi-class.md) class PackageID property.|  

## See Also  
 [Windows Management Instrumentation](/windows/win32/wmisdk/wmi-start-page)   
 [Objects overview](configuration-manager-objects-overview.md)
 [How to Call a Configuration Manager Object Class Method by Using WMI](../../../develop/core/understand/how-to-call-a-configuration-manager-object-class-method-by-using-wmi.md)   
 [How to Connect to an SMS Provider in Configuration Manager by Using WMI](../../../develop/core/understand/how-to-connect-to-an-sms-provider-in-configuration-manager-by-using-wmi.md)   
 [How to Create a Configuration Manager Object by Using WMI](../../../develop/core/understand/how-to-create-a-configuration-manager-object-by-using-wmi.md)   
 [How to Delete a Configuration Manager Object by Using WMI](../../../develop/core/understand/how-to-delete-a-configuration-manager-object-by-using-wmi.md)   
 [How to Modify a Configuration Manager Object by Using WMI](../../../develop/core/understand/how-to-modify-a-configuration-manager-object-by-using-wmi.md)   
 [How to Perform an Asynchronous Configuration Manager Query by Using WMI](../../../develop/core/understand/how-to-perform-an-asynchronous-configuration-manager-query-by-using-wmi.md)   
 [How to Perform a Synchronous Configuration Manager Query by Using WMI](../../../develop/core/understand/how-to-perform-a-synchronous-configuration-manager-query-by-using-wmi.md)   
 [How to Read Lazy Properties by Using WMI](../../../develop/core/understand/how-to-read-lazy-properties-by-using-wmi.md)
