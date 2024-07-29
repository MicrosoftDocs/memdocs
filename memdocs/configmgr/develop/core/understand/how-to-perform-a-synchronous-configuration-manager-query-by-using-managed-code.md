---
title: Perform a Synchronous Query by Using Managed Code
titleSuffix: Configuration Manager
description: To perform a synchronous query by using the managed SMS Provider, you use *WqlConnectionManager.QueryProcessor.ExecuteQuery* method.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: how-to
ms.assetid: 0ec43754-0e84-472a-af93-e7d11ab32654
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# How to Perform a Synchronous Configuration Manager Query by Using Managed Code
To perform a synchronous query by using the managed SMS Provider, you use *WqlConnectionManager.QueryProcessor.ExecuteQuery* method.  

 The [ExecuteQuery](/previous-versions/system-center/developer/cc146278(v=msdn.10)) method takes a WQL query string and optional context information for the call. An [IResultObject](/previous-versions/system-center/developer/cc147376(v=msdn.10)) is returned containing the objects found in the query.  

### To perform a synchronous query  

1.  Set up a connection to the SMS Provider. For more information, see [SMS Provider fundamentals](sms-provider-fundamentals.md).  

2.  Using the **WqlConnectionManager** object you obtain in step one, call the **QueryProcessor** object *ExecuteQuery* method to query SMS Provider and get an [IResultObject](/previous-versions/system-center/developer/cc147376(v=msdn.10)) containing a collection of query results.  

## Example  
 The following code example shows how to make a synchronous query for the available packages by using *ExecuteQuery*.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../develop/core/understand/calling-code-snippets.md).  

```  
public void QueryPackages(WqlConnectionManager connection)  
{  
    try  
    {  
        IResultObject query = connection.QueryProcessor.ExecuteQuery("Select * from SMS_Package");  
        foreach (IResultObject o in query)  
        {  
            Console.WriteLine(o["Name"].StringValue);  
            o.Dispose();  
        }  
    }  
    catch (SmsException ex)  
    {  
        Console.WriteLine("Failed to query packages: " + ex.Message);  
        throw;  
    }  
}  

```  

 This example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`connection`|Managed: `WqlConnectionManager`|A valid connection to the SMS Provider.|  

## Compiling the Code  

### Namespaces  
 System  

 System.Collections.Generic  

 System.ComponentModel  

 Microsoft.ConfigurationManagement.ManagementProvider  

 Microsoft.ConfigurationManagement.ManagementProvider.WqlQueryEngine  

### Assembly  
 microsoft.configurationmanagement.managementprovider  

 adminui.wqlqueryengine  

## Robust Programming  
 The Configuration Manager exceptions that can be raised are [SmsConnectionException](/previous-versions/system-center/developer/cc147431(v=msdn.10)) and [SmsQueryException](/previous-versions/system-center/developer/cc147436(v=msdn.10)). These can be caught together with [SmsException](/previous-versions/system-center/developer/cc147433(v=msdn.10)).  

## See Also  
 [Objects overview](configuration-manager-objects-overview.md)
 [Configuration Manager Lazy Properties](../../../develop/core/understand/configuration-manager-lazy-properties.md)   
 [How to Call a Configuration Manager Object Class Method by Using Managed Code](../../../develop/core/understand/how-to-call-a-configuration-manager-object-class-method-by-using-managed-code.md)   
 [How to Connect to a Configuration Manager Provider using Managed Code](../../../develop/core/understand/how-to-connect-to-an-sms-provider-by-using-managed-code.md)   
 [How to Create a Configuration Manager Object by Using Managed Code](../../../develop/core/understand/how-to-create-a-configuration-manager-object-by-using-managed-code.md)   
 [How to Modify a Configuration Manager Object by Using Managed Code](../../../develop/core/understand/how-to-modify-a-configuration-manager-object-by-using-managed-code.md)   
 [How to Perform an Asynchronous Configuration Manager Query by Using Managed Code](../../../develop/core/understand/how-to-perform-an-asynchronous-query-by-using-managed-code.md)   
 [How to Read a Configuration Manager Object by Using Managed Code](../../../develop/core/understand/how-to-read-a-configuration-manager-object-by-using-managed-code.md)   
 [How to Read Lazy Properties by Using Managed Code](../../../develop/core/understand/how-to-read-lazy-properties-by-using-managed-code.md)   
 [Configuration Manager Extended WMI Query Language](../../../develop/core/understand/extended-wmi-query-language.md)   
 [Configuration Manager Result Sets](../../../develop/core/understand/result-sets.md)   
 [Configuration Manager Special Queries](../../../develop/core/understand/special-queries.md)   
 [About queries](about-configuration-manager-queries.md)
