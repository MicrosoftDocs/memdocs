---
title: "Read Lazy Properties by Using WMI"
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
ms.assetid: 1fa2d52e-b5e6-4362-81cf-e175ff45435asearchScope: - ConfigMgr SDK
caps.latest.revision: 7
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Read Lazy Properties by Using WMI
To read a lazy property from a System Center Configuration Manager object returned in a query, you get the object instance, which in turn retrieves any lazy object properties from the SMS Provider.  

> [!NOTE]
>  If you know the full path to the WMI object, a call to the `SWbemServices` class `Get` method will return the WMI object along with any lazy properties. For more information, see [How to Read a Configuration Manager Object by Using WMI](../../../develop/core/understand/how-to-read-a-configuration-manager-object-by-using-wmi.md).  

 For more information about lazy properties, see [Configuration Manager Lazy Properties](../../../develop/core/understand/configuration-manager-lazy-properties.md).  

### To read lazy properties  

1.  Set up a connection to the SMS Provider. For more information, see [How to Connect to an SMS Provider in Configuration Manager by Using WMI](../../../develop/core/understand/how-to-connect-to-an-sms-provider-in-configuration-manager-by-using-wmi.md).  

2.  Using the [SWbemServices](https://msdn.microsoft.com/library/aa393854.aspx) object you obtain from step one, use the [ExecQuery](https://msdn.microsoft.com/library/aa393866.aspx) object to query System Center Configuration Manager objects.  

3.  Iterate through the query results.  

4.  Using the `SWbemServices` object you obtain from step one, call [Get](https://msdn.microsoft.com/library/aa393868.aspx) to get the [SWbemObject](https://msdn.microsoft.com/library/aa393741.aspx) object for each queried object you want to get lazy properties from.  

## Example  
 The following VBScript code example queries for all [SMS_Collection](../../../develop/reference/core/clients/collections/sms_collection-server-wmi-class.md) objects and then displays rule names obtained from the `CollectionRules` lazy property.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Sub ReadLazyProperty(connection)  

    Dim collection  
    Dim collections  
    Dim collectionLazy  
    Dim i  

    ' Get all collections.  
    Set collections = _  
        connection.ExecQuery("Select * From SMS_Collection")  

    For Each collection in collections  

        Wscript.Echo Collection.Name   

        ' Get the collection object.  
        Set collectionLazy = connection.Get("SMS_Collection.CollectionID='" + collection.CollectionID + "'")  

        ' Display the rule names that are in the lazy property CollectionRules.  
        If IsNull(collectionLazy.CollectionRules) Then  
            Wscript.Echo "No rules"  
        Else   
            For i = 0 To UBound(collectionLazy.CollectionRules)  
                WScript.Echo "Rule " + collectionLazy.CollectionRules(i).RuleName  
            Next  
       End If       
    Next          

End Sub      
```  

 This example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`connection`|-   `SWbemServices`|A valid connection to the SMS Provider.|  

## Compiling the Code  

## See Also  
 [Windows Management Instrumentation](http://go.microsoft.com/fwlink/?LinkId=43950)   
 [Configuration Manager Lazy Properties](../../../develop/core/understand/configuration-manager-lazy-properties.md)   
 [Configuration Manager Objects](../../../develop/core/understand/configuration-manager-objects-overview.md)   
 [How to Call a Configuration Manager Object Class Method by Using WMI](../../../develop/core/understand/how-to-call-a-configuration-manager-object-class-method-by-using-wmi.md)   
 [How to Connect to an SMS Provider in Configuration Manager by Using WMI](../../../develop/core/understand/how-to-connect-to-an-sms-provider-in-configuration-manager-by-using-wmi.md)   
 [How to Create a Configuration Manager Object by Using WMI](../../../develop/core/understand/how-to-create-a-configuration-manager-object-by-using-wmi.md)   
 [How to Delete a Configuration Manager Object by Using WMI](../../../develop/core/understand/how-to-delete-a-configuration-manager-object-by-using-wmi.md)   
 [How to Modify a Configuration Manager Object by Using WMI](../../../develop/core/understand/how-to-modify-a-configuration-manager-object-by-using-wmi.md)   
 [How to Perform an Asynchronous Configuration Manager Query by Using WMI](../../../develop/core/understand/how-to-perform-an-asynchronous-configuration-manager-query-by-using-wmi.md)   
 [How to Perform a Synchronous Configuration Manager Query by Using WMI](../../../develop/core/understand/how-to-perform-a-synchronous-configuration-manager-query-by-using-wmi.md)   
 [How to Read a Configuration Manager Object by Using WMI](../../../develop/core/understand/how-to-read-a-configuration-manager-object-by-using-wmi.md)   
 [How to Use Configuration Manager Objects With WMI](../../../develop/core/understand/how-to-use-configuration-manager-objects-with-wmi.md)
