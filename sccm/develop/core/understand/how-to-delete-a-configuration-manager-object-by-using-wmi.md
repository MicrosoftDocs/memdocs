---
title: "Delete an Object by Using WMI"
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
ms.assetid: e843aaf1-f278-447d-82b1-642f4286b65dsearchScope: - ConfigMgr SDK
caps.latest.revision: 7
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Delete a Configuration Manager Object by Using WMI
To delete a System Center Configuration Manager object, in System Center Configuration Manager, call the [SWbemObject](https://msdn.microsoft.com/library/aa393741.aspx) object [Delete_](https://msdn.microsoft.com/library/aa393771.aspx) method.  

### To delete a Configuration Manager object  

1.  Set up a connection to the SMS Provider. For more information, see [How to Connect to an SMS Provider in Configuration Manager by Using WMI](../../../develop/core/understand/how-to-connect-to-an-sms-provider-in-configuration-manager-by-using-wmi.md).  

2.  Using the [SWbemServices](https://msdn.microsoft.com/library/aa393854.aspx) object you obtain from step one, call the [Get](https://msdn.microsoft.com/library/aa393868.aspx) method and specify the class and key information for the object you want to delete. `Get` returns a `SWbemObject` that represents the object.  

3.  Using the `SWbemObject`, call `Delete` to delete the object.  

## Example  
 The following VBScript code example deletes the package ([SMS_Package](../../../develop/reference/core/servers/configure/sms_package-server-wmi-class.md)) identified by its package identifier `packageID`.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Sub DeletePackage (connection, packageID)  

    On Error Resume Next   
    Dim package  

    Set package = connection.Get("SMS_Package.PackageID='" & packageID & "'")  
    If Err.Number<>0 Then  
        Wscript.Echo "Couldn't get package " + packageID  
        Exit Sub  
    End If  

    package.Delete_  

    WScript.Echo "Package deleted"  

    If Err.Number<>0 Then  
        Wscript.Echo "Couldn't delete " + packageID  
        Exit Sub  
    End If  

End Sub  

```  

 This example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`connection`|`SWbemServices`|A valid connection to the SMS Provider.|  
|`packageID`|`String`|The package identifier. This is obtained from the `SMS_Package` class `PackageID`.|  

## See Also  
 [Windows Management Instrumentation](http://go.microsoft.com/fwlink/?LinkId=43950)   
 [Configuration Manager Objects](../../../develop/core/understand/configuration-manager-objects-overview.md)   
 [How to Call a Configuration Manager Object Class Method by Using WMI](../../../develop/core/understand/how-to-call-a-configuration-manager-object-class-method-by-using-wmi.md)   
 [How to Connect to an SMS Provider in Configuration Manager by Using WMI](../../../develop/core/understand/how-to-connect-to-an-sms-provider-in-configuration-manager-by-using-wmi.md)   
 [How to Create a Configuration Manager Object by Using WMI](../../../develop/core/understand/how-to-create-a-configuration-manager-object-by-using-wmi.md)   
 [How to Modify a Configuration Manager Object by Using WMI](../../../develop/core/understand/how-to-modify-a-configuration-manager-object-by-using-wmi.md)   
 [How to Perform an Asynchronous Configuration Manager Query by Using WMI](../../../develop/core/understand/how-to-perform-an-asynchronous-configuration-manager-query-by-using-wmi.md)   
 [How to Perform a Synchronous Configuration Manager Query by Using WMI](../../../develop/core/understand/how-to-perform-a-synchronous-configuration-manager-query-by-using-wmi.md)   
 [How to Read a Configuration Manager Object by Using WMI](../../../develop/core/understand/how-to-read-a-configuration-manager-object-by-using-wmi.md)   
 [How to Read Lazy Properties by Using WMI](../../../develop/core/understand/how-to-read-lazy-properties-by-using-wmi.md)   
 [How to Use Configuration Manager Objects With WMI](../../../develop/core/understand/how-to-use-configuration-manager-objects-with-wmi.md)
