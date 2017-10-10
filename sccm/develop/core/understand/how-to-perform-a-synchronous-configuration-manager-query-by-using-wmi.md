---
title: "Perform a Synchronous Query by Using WMI"
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
ms.assetid: d08b5e24-7026-4328-b67d-3ba2c87aea63searchScope: - ConfigMgr SDK
caps.latest.revision: 7
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Perform a Synchronous Configuration Manager Query by Using WMI
In System Center Configuration Manager, you perform a synchronous query for System Center Configuration Manager objects by calling the [SWbemServices](https://msdn.microsoft.com/library/aa393854.aspx) object [ExecQuery](https://msdn.microsoft.com/library/aa393866.aspx) method and passing a WQL query.  

 A synchronous query is a query that maintains control over the process of your application for the duration of the query. A synchronous query has the potential of locking up your application for large queries or for queries over a network. Alternatively, you can run an asynchronous query that returns control to the application while the query is run. For more information, see [How to Perform an Asynchronous Configuration Manager Query by Using Managed Code](../../../develop/core/understand/how-to-perform-an-asynchronous-query-by-using-managed-code.md)  

> [!NOTE]
>  Lazy properties are not returned in synchronous queries. For more information, see [How to Read Lazy Properties by Using WMI](../../../develop/core/understand/how-to-read-lazy-properties-by-using-wmi.md).  

### To perform a synchronous query  

1.  Set up a connection to the SMS Provider. For more information, see [How to Connect to an SMS Provider in Configuration Manager by Using WMI](../../../develop/core/understand/how-to-connect-to-an-sms-provider-in-configuration-manager-by-using-wmi.md).  

2.  Using the SWbemServices object that you obtain from step one, use the ExecQuery method to get a [SWbemObjectSet](https://msdn.microsoft.com/library/aa393762.aspx) collection containing the query results.  

3.  Iterate through the SWbemObjectSet collection to access a [SWbemObject](https://msdn.microsoft.com/library/aa393741.aspx) for each object returned by the query.  

## Example  
 The following example performs a synchronous query of all packages in Configuration Manager.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Sub QueryPackages(connection)  

    On Error Resume next  

    Dim packages  
    Dim package  

    ' Run the query.  
    Set packages = _  
        connection.ExecQuery("Select * From SMS_Package")  

    If Err.Number<>0 Then  
        Wscript.Echo "Couldn't get Packages"  
        Wscript.Quit  
    End If  

    For Each package In packages  
        WScript.Echo  package.Name  
    Next  

    If packages.Count=0 Then  
        Wscript.Echo "No packages found"  
    End If  

End Sub  
```  

 This example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`connection`|[SWbemServices](https://msdn.microsoft.com/library/aa393854.aspx)|A valid connection to the SMS Provider.|  

## See Also  
 [Windows Management Instrumentation](http://go.microsoft.com/fwlink/?LinkId=43950)   
 [Configuration Manager Objects](../../../develop/core/understand/configuration-manager-objects-overview.md)   
 [How to Call a Configuration Manager Object Class Method by Using WMI](../../../develop/core/understand/how-to-call-a-configuration-manager-object-class-method-by-using-wmi.md)   
 [How to Connect to an SMS Provider in Configuration Manager by Using WMI](../../../develop/core/understand/how-to-connect-to-an-sms-provider-in-configuration-manager-by-using-wmi.md)   
 [How to Create a Configuration Manager Object by Using WMI](../../../develop/core/understand/how-to-create-a-configuration-manager-object-by-using-wmi.md)   
 [How to Delete a Configuration Manager Object by Using WMI](../../../develop/core/understand/how-to-delete-a-configuration-manager-object-by-using-wmi.md)   
 [How to Modify a Configuration Manager Object by Using WMI](../../../develop/core/understand/how-to-modify-a-configuration-manager-object-by-using-wmi.md)   
 [How to Perform an Asynchronous Configuration Manager Query by Using WMI](../../../develop/core/understand/how-to-perform-an-asynchronous-configuration-manager-query-by-using-wmi.md)   
 [How to Read a Configuration Manager Object by Using WMI](../../../develop/core/understand/how-to-read-a-configuration-manager-object-by-using-wmi.md)   
 [How to Read Lazy Properties by Using WMI](../../../develop/core/understand/how-to-read-lazy-properties-by-using-wmi.md)   
 [How to Use Configuration Manager Objects With WMI](../../../develop/core/understand/how-to-use-configuration-manager-objects-with-wmi.md)   
 [Configuration Manager Extended WMI Query Language](../../../develop/core/understand/extended-wmi-query-language.md)   
 [Configuration Manager Result Sets](../../../develop/core/understand/result-sets.md)   
 [Configuration Manager Special Queries](../../../develop/core/understand/special-queries.md)   
 [Configuration Manager Queries](../../../develop/core/understand/queries.md)
