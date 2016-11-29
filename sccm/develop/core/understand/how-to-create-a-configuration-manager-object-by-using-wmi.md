---
title: "Create an Object by Using WMI | Microsoft Docs"
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
ms.assetid: c52cf79a-45d7-45c8-b8f2-5610d06b38e0
caps.latest.revision: 8
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Create a Configuration Manager Object by Using WMI
You create a Configuration Manager object, in System Center Configuration Manager, by calling the [SWbemObject](assetId:///SWbemObject?qualifyHint=False&autoUpgrade=True) object [SpawnInstance](assetId:///SpawnInstance?qualifyHint=False&autoUpgrade=True) method.  

 The assetId:///SWbemObject?qualifyHint=False&autoUpgrade=True is the class definition for the object type that you want to create. For example, [SMS_Package](assetId:///SMS_Package?qualifyHint=False&autoUpgrade=True). You get the [SWBemObject](assetId:///SWBemObject?qualifyHint=False&autoUpgrade=True) by calling the [SWBemServices](assetId:///SWBemServices?qualifyHint=False&autoUpgrade=True) object [Get](assetId:///Get?qualifyHint=False&autoUpgrade=True) method.  

### To create a Configuration Manager object  

1.  Set up a connection to the SMS Provider. For more information, see [How to Connect to an SMS Provider in Configuration Manager by Using WMI](../../../develop/core/understand/how-to-connect-to-an-sms-provider-in-configuration-manager-by-using-wmi.md).  

2.  Using the [SWbemServices](assetId:///SWbemServices?qualifyHint=False&autoUpgrade=True) object you obtain from step one, call assetId:///Get?qualifyHint=False&autoUpgrade=True to get the assetId:///SWbemObject?qualifyHint=False&autoUpgrade=True for the Configuration Manager object class definition.  

3.  Call assetId:///SpawnInstance?qualifyHint=False&autoUpgrade=True on the assetId:///SWbemObject?qualifyHint=False&autoUpgrade=True to create the new object. A assetId:///SWbemObject?qualifyHint=False&autoUpgrade=True is returned for the new object.  

4.  Using the assetId:///SWbemObject?qualifyHint=False&autoUpgrade=True returned from the call to assetId:///SpawnInstance?qualifyHint=False&autoUpgrade=True, populate the object properties.  

5.  Call [Put](assetId:///Put?qualifyHint=False&autoUpgrade=True) to commit the new object to the SMS Provider.  

## Example  
 The following VBScript code example creates an assetId:///SMS_Package?qualifyHint=False&autoUpgrade=True object.  

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
|`Connection`|assetId:///SWbemServices?qualifyHint=False&autoUpgrade=True|A valid connection to the SMS Provider.|  

## Compiling the Code  

## See Also  
 [Windows Management Instrumentation](http://go.microsoft.com/fwlink/?LinkId=43950)   
 [Configuration Manager Objects](../../../develop/core/understand/configuration-manager-objects-overview.md)   
 [How to Call a Configuration Manager Object Class Method by Using WMI](../../../develop/core/understand/how-to-call-a-configuration-manager-object-class-method-by-using-wmi.md)   
 [How to Connect to an SMS Provider in Configuration Manager by Using WMI](../../../develop/core/understand/how-to-connect-to-an-sms-provider-in-configuration-manager-by-using-wmi.md)   
 [How to Delete a Configuration Manager Object by Using WMI](../../../develop/core/understand/how-to-delete-a-configuration-manager-object-by-using-wmi.md)   
 [How to Modify a Configuration Manager Object by Using WMI](../../../develop/core/understand/how-to-modify-a-configuration-manager-object-by-using-wmi.md)   
 [How to Perform an Asynchronous Configuration Manager Query by Using WMI](../../../develop/core/understand/how-to-perform-an-asynchronous-configuration-manager-query-by-using-wmi.md)   
 [How to Perform a Synchronous Configuration Manager Query by Using WMI](../../../develop/core/understand/how-to-perform-a-synchronous-configuration-manager-query-by-using-wmi.md)   
 [How to Read a Configuration Manager Object by Using WMI](../../../develop/core/understand/how-to-read-a-configuration-manager-object-by-using-wmi.md)   
 [How to Read Lazy Properties by Using WMI](../../../develop/core/understand/how-to-read-lazy-properties-by-using-wmi.md)   
 [How to Use Configuration Manager Objects With WMI](../../../develop/core/understand/how-to-use-configuration-manager-objects-with-wmi.md)
