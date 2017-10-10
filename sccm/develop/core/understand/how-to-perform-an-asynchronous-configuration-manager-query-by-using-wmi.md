---
title: "Perform an Asynchronous Query by Using WMI"
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
ms.assetid: ff1c49fa-dede-4a22-b0e8-38460c4aa057searchScope: - ConfigMgr SDK
caps.latest.revision: 7
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Perform an Asynchronous Configuration Manager Query by Using WMI
In System Center Configuration Manager, you perform an synchronous query for Configuration Manager objects by calling the [SWbemServices](https://msdn.microsoft.com/library/aa393854.aspx) object [ExecQueryAsync](https://msdn.microsoft.com/library/aa392108.aspx) method and by implementing a sink method to handle query results.  

 To handle each returned object, create an [objWbemSink.OnObjectReady](https://msdn.microsoft.com/library/aa393881.aspx) event subroutine. To be notified when the query is completed, create a [objWbemSink.OnCompleted](https://msdn.microsoft.com/library/aa393879.aspx) event subroutine.  

> [!NOTE]
>  Lazy properties are not returned in asynchronous queries. For more information, see [How to Read Lazy Properties by Using WMI](../../../develop/core/understand/how-to-read-lazy-properties-by-using-wmi.md).  

### To perform an asynchronous query  

1.  Set up a connection to the SMS Provider. For more information, see [How to Connect to an SMS Provider in Configuration Manager by Using WMI](../../../develop/core/understand/how-to-connect-to-an-sms-provider-in-configuration-manager-by-using-wmi.md).  

2.  Create an [OnObjectReady](https://msdn.microsoft.com/library/aa393881.aspx) subroutine to handle objects by the query.  

3.  Create an [OnCompleted](https://msdn.microsoft.com/library/aa393879.aspx) subroutine to handle query completion.  

4.  Using the [SWbemServices](https://msdn.microsoft.com/library/aa393854.aspx) object you obtain from step one, use [ExecQueryAsync](https://msdn.microsoft.com/library/aa392108.aspx) object to query System Center Configuration Manager objects asynchronously.  

## Example  
 The following VBScript code example asynchronously queries for all [SMS_Collection](../../../develop/reference/core/clients/collections/sms_collection-server-wmi-class.md) objects.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Dim bdone  
Sub QueryCollection(connection)  

    Dim sink  
    bdone = False  

    Set sink = WScript.CreateObject("wbemscripting.swbemsink","sink_")  

    ' Query for all collections.  
    connection.ExecQueryAsync sink, "select * from SMS_Collection"  

    ' Wait until all instances are returned.  
    While Not bdone      
        wscript.sleep 1000  
    Wend  
 End Sub     

' The sink subroutine to handle the OnObjectReady   
' event. This is called as each object returns.  
Sub sink_OnObjectReady(collection, octx)  
    WScript.Echo "CollectionID: " + collection.CollectionID  
    WScript.Echo "Name: " + collection.Name  
    Wscript.Echo  
End Sub  

' The sink subroutine to handle the OnCompleted event.  
' This is called when all the objects are returned.   
' The oErr parameter obtains an SWbemLastError object,  
' if available from the provider.  
Sub sink_OnCompleted(HResult, oErr, oCtx)  
    WScript.Echo "All collections returned"  
    bdone = true  
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
 [How to Perform a Synchronous Configuration Manager Query by Using WMI](../../../develop/core/understand/how-to-perform-a-synchronous-configuration-manager-query-by-using-wmi.md)   
 [How to Read a Configuration Manager Object by Using WMI](../../../develop/core/understand/how-to-read-a-configuration-manager-object-by-using-wmi.md)   
 [How to Read Lazy Properties by Using WMI](../../../develop/core/understand/how-to-read-lazy-properties-by-using-wmi.md)   
 [How to Use Configuration Manager Objects With WMI](../../../develop/core/understand/how-to-use-configuration-manager-objects-with-wmi.md)   
 [Configuration Manager Extended WMI Query Language](../../../develop/core/understand/extended-wmi-query-language.md)   
 [Configuration Manager Result Sets](../../../develop/core/understand/result-sets.md)   
 [Configuration Manager Special Queries](../../../develop/core/understand/special-queries.md)   
 [Configuration Manager Queries](../../../develop/core/understand/queries.md)
