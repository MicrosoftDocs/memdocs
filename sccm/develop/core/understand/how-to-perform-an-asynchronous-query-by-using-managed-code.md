---
title: "Perform an Asynchronous Query by Using Managed Code"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: cfbb34e8-9b47-48db-a8ef-408a0a89ad17
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# How to Perform an Asynchronous Configuration Manager Query by Using Managed Code
In System Center Configuration Manager, to perform an asynchronous query by using the managed SMS Provider, you use the [ProcessQuery](https://msdn.microsoft.com/library/cc146295.aspx) method.  

 The first parameter of the [ProcessQuery](https://msdn.microsoft.com/library/cc146295.aspx) method is an instance of the [SmsBackgroundWorker](https://msdn.microsoft.com/library/microsoft.configurationmanagement.managementprovider.smsbackgroundworker.aspx) class that provides two event handlers:  

-   [QueryProcessObjectReady](https://msdn.microsoft.com/library/microsoft.configurationmanagement.managementprovider.smsbackgroundworker.queryprocessorobjectready.aspx). This event handler is called for each object returned by the query. The event handler provides an IResultObject object that represents the object.  

-   [QueryProcessCompleted](https://msdn.microsoft.com/library/microsoft.configurationmanagement.managementprovider.smsbackgroundworker.queryprocessorcompleted.aspx). This event handler is called when the query is completed. It also provides information about any errors that occur. For more information, see For information about error handling, see [How to Handle Configuration Manager Asynchronous Errors by Using Managed Code](../../../develop/core/understand/how-to-handle-configuration-manager-asynchronous-errors-by-using-managed-code.md).  

 The second parameter to of the [ProcessQuery](https://msdn.microsoft.com/library/cc146295.aspx) method is the WQL statement for the query.  

### To perform an asynchronous query  

1.  Set up a connection to the SMS Provider. For more information, see [About the SMS Provider in Configuration Manager](../../../develop/core/understand/about-the-sms-provider-in-configuration-manager.md).  

2.  Create the **SmsBackgroundWorker** object and populate the [QueryProcessorObjectReady](https://msdn.microsoft.com/library/microsoft.configurationmanagement.managementprovider.smsbackgroundworker.queryprocessorobjectready.aspx) and [QueryProcessorCompleted](https://msdn.microsoft.com/library/microsoft.configurationmanagement.managementprovider.smsbackgroundworker.queryprocessorcompleted.aspx) properties with the callback method names.  

3.  From the **WqlConnectionManager** object you obtain in step one, call the **QueryProcessor** object [ProcessQuery](https://msdn.microsoft.com/library/cc146295.aspx) method to start the asynchronous query.  

## Example  
 The following example queries for all available SMS_Collection objects, and in the event handler, the example writes several of the collection properties to the System Center Configuration Manager console.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../develop/core/understand/calling-code-snippets.md).  

```  
public void QueryCollections(WqlConnectionManager connection)  
{  
    try  
    {  
        // Set up the query.  
        SmsBackgroundWorker bw1 = new SmsBackgroundWorker();  
        bw1.QueryProcessorObjectReady += new EventHandler<QueryProcessorObjectEventArgs>(bw1_QueryProcessorObjectReady);  
        bw1.QueryProcessorCompleted += new EventHandler<RunWorkerCompletedEventArgs>(bw1_QueryProcessorCompleted);  

        // Query for all collections.  
        connection.QueryProcessor.ProcessQuery(bw1, "select * from SMS_Collection");  

        // Pause while query runs.  
        Console.ReadLine();  
    }  
    catch (SmsException ex)  
    {  
        Console.WriteLine("Failed to start asynchronous query: ", ex.Message);  
    }  
}  

void bw1_QueryProcessorObjectReady(object sender, QueryProcessorObjectEventArgs e)  
{  
    try  
    {  
        // Get the collection.  
        IResultObject collection = (IResultObject)e.ResultObject;  

        //Display properties.  
        Console.WriteLine(collection["CollectionID"].StringValue);  
        Console.WriteLine(collection["Name"].StringValue);  
        Console.WriteLine();  
        collection.Dispose();  
    }  
    catch (SmsQueryException eX)  
    {  
        Console.WriteLine("Query Error: " + eX.Message);  
    }  
}  

void bw1_QueryProcessorCompleted(object sender, RunWorkerCompletedEventArgs e)  
{  
    Console.WriteLine("Done...");  
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
 The Configuration Manager exceptions that can be raised are [SmsConnectionException](https://msdn.microsoft.com/library/microsoft.configurationmanagement.managementprovider.smsconnectionexception.aspx) and [SmsQueryException](https://msdn.microsoft.com/library/microsoft.configurationmanagement.managementprovider.smsqueryexception.aspx). These can be caught together with [SmsException](https://msdn.microsoft.com/library/microsoft.configurationmanagement.managementprovider.smsexception.aspx).  

## See Also  
 [About Configuration Manager Objects](../../../develop/core/understand/about-configuration-manager-objects.md)   
 [Configuration Manager Lazy Properties](../../../develop/core/understand/configuration-manager-lazy-properties.md)   
 [How to Call a Configuration Manager Object Class Method by Using Managed Code](../../../develop/core/understand/how-to-call-a-configuration-manager-object-class-method-by-using-managed-code.md)   
 [How to Connect to a Configuration Manager Provider using Managed Code](../../../develop/core/understand/how-to-connect-to-an-sms-provider-by-using-managed-code.md)   
 [How to Create a Configuration Manager Object by Using Managed Code](../../../develop/core/understand/how-to-create-a-configuration-manager-object-by-using-managed-code.md)   
 [How to Modify a Configuration Manager Object by Using Managed Code](../../../develop/core/understand/how-to-modify-a-configuration-manager-object-by-using-managed-code.md)   
 [How to Perform a Synchronous Configuration Manager Query by Using Managed Code](../../../develop/core/understand/how-to-perform-a-synchronous-configuration-manager-query-by-using-managed-code.md)   
 [How to Read a Configuration Manager Object by Using Managed Code](../../../develop/core/understand/how-to-read-a-configuration-manager-object-by-using-managed-code.md)   
 [How to Read Lazy Properties by Using Managed Code](../../../develop/core/understand/how-to-read-lazy-properties-by-using-managed-code.md)   
 [How to Use Configuration Manager Objects With Managed Code](../../../develop/core/understand/how-to-use-configuration-manager-objects-with-managed-code.md)   
 [How to Perform a Synchronous Configuration Manager Query Using  Managed Code](../../../develop/core/understand/how-to-perform-a-synchronous-configuration-manager-query-by-using-managed-code.md)   
 [Configuration Manager Extended WMI Query Language](../../../develop/core/understand/extended-wmi-query-language.md)   
 [Configuration Manager Result Sets](../../../develop/core/understand/result-sets.md)   
 [Configuration Manager Special Queries](../../../develop/core/understand/special-queries.md)   
 [Configuration Manager Queries](../../../develop/core/understand/queries.md)
