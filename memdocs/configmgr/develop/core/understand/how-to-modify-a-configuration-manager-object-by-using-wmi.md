---
description: Learn how to modify an Object by using WMI.
title: Modify an Object by Using WMI
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: 6101f903-172b-4e59-8801-4a9c5975e3c9
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# How to Modify a Configuration Manager Object by Using WMI
You modify a Configuration Manager object, in Configuration Manager, by using the object's [SWbemObject](/windows/win32/wmisdk/swbemobject) object to change its properties.  

### To modify a Configuration Manager object  

1.  Set up a connection to the SMS Provider. For more information, see [How to Connect to an SMS Provider in Configuration Manager by Using WMI](../../../develop/core/understand/how-to-connect-to-an-sms-provider-in-configuration-manager-by-using-wmi.md).  

2.  Using the [SWbemServices](/windows/win32/wmisdk/swbemservices) object you obtain from step one, call the [Get](/windows/win32/wmisdk/swbemservices-get) method and specify the class and key information for the object you want. This returns a [SWbemObject](/windows/win32/wmisdk/swbemobject) representing object.  

3.  Using the [SWbemObject](/windows/win32/wmisdk/swbemobject), update the object properties.  

4.  Call [Put_](/windows/win32/wmisdk/swbemobject-put-) to update the object in the SMS Provider.  

## Example  
 The following VBScript code example gets a package (SMS_Package) object, changes the package description, and then commits the changes back to the SMS Provider. In this example, the package is retrieved through a call to the SWbemServices object [Get](/windows/win32/wmisdk/swbemservices-get). You can also retrieve the package by using a query. For more information, see [How to Perform a Synchronous Configuration Manager Query by Using WMI](../../../develop/core/understand/how-to-perform-a-synchronous-configuration-manager-query-by-using-wmi.md).  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Sub ModifyPackageDescription (connection, packageID, description)  

    On Error Resume Next   
    Dim package  

    ' Get the package.  
    Set package = connection.Get("SMS_Package.PackageID='" & packageID & "'")  
    If Err.Number<>0 Then  
        Wscript.Echo "Couldn't get package " + packageID  
        Exit Sub  
    End If  

    Wscript.Echo "Package Name: " + package.Name  
    Wscript.Echo "Current Description: " + package.Description  

    ' Update and commit the package.  
    package.Description = description  

    package.Put_  
    If Err.Number<>0 Then  
        WScript.Echo "Couldn't commit the package"  
        Exit Sub  
    End If  

    Wscript.Echo "New Description: " + package.Description  
End Sub  
```  

 This example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`connection`|[SWbemServices](/windows/win32/wmisdk/swbemservices)|A valid connection to the SMS Provider.|  
|`packageID`|`String`|The package identifier. This is available from the `SMS_Package` class `PackageID` identifier.|  
|`Description`|`String`|A new description for the object.|  

## See Also  
 [Windows Management Instrumentation](/windows/win32/wmisdk/wmi-start-page)   
 [Objects overview](configuration-manager-objects-overview.md)
 [How to Call a Configuration Manager Object Class Method by Using WMI](../../../develop/core/understand/how-to-call-a-configuration-manager-object-class-method-by-using-wmi.md)   
 [How to Connect to an SMS Provider in Configuration Manager by Using WMI](../../../develop/core/understand/how-to-connect-to-an-sms-provider-in-configuration-manager-by-using-wmi.md)   
 [How to Create a Configuration Manager Object by Using WMI](../../../develop/core/understand/how-to-create-a-configuration-manager-object-by-using-wmi.md)   
 [How to Delete a Configuration Manager Object by Using WMI](../../../develop/core/understand/how-to-delete-a-configuration-manager-object-by-using-wmi.md)   
 [How to Perform an Asynchronous Configuration Manager Query by Using WMI](../../../develop/core/understand/how-to-perform-an-asynchronous-configuration-manager-query-by-using-wmi.md)   
 [How to Perform a Synchronous Configuration Manager Query by Using WMI](../../../develop/core/understand/how-to-perform-a-synchronous-configuration-manager-query-by-using-wmi.md)   
 [How to Read a Configuration Manager Object by Using WMI](../../../develop/core/understand/how-to-read-a-configuration-manager-object-by-using-wmi.md)   
 [How to Read Lazy Properties by Using WMI](../../../develop/core/understand/how-to-read-lazy-properties-by-using-wmi.md)
