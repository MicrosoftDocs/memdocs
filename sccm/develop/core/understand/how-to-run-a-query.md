---
title: "Run a Query"
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
ms.assetid: c714a1cf-86af-4de2-9160-af360a484895searchScope: - ConfigMgr SDK
caps.latest.revision: 8
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Run a Configuration Manager Query
In System Center Configuration Manager, you run a `SMS_Query` based query by getting the query instance and then by running WQL query in the `SMS_Query` object `Expression` property.  

 After you have the WQL query, you can run the query either synchronously or asynchronously. The following example is synchronous. For information about running the query asynchronously, see [How to Perform an Asynchronous Configuration Manager Query by Using Managed Code](../../../develop/core/understand/how-to-perform-an-asynchronous-query-by-using-managed-code.md) and [How to Perform an Asynchronous Configuration Manager Query by Using WMI](../../../develop/core/understand/how-to-perform-an-asynchronous-configuration-manager-query-by-using-wmi.md). In these examples, change the `select * from collection` string to the `Expression` property value.  

### To run a query  

1.  Set up a connection to the SMS Provider. For more information, see [About the SMS Provider in Configuration Manager](../../../develop/core/understand/about-the-sms-provider-in-configuration-manager.md).  

2.  Get the `SMS_Query` object for the query you want to run.  

3.  Run the query identified by the `SMS_Query` object `Expression` property.  

## Example  
 The following example method synchronously runs the query identified by the `queryId` parameter.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Sub RunQuery(connection, queryId)  
    Dim query  
    Dim queryResults  
    Dim queryResult  

    ' Get query.  
    Set query=connection.Get("SMS_Query.QueryID='" & queryId  & "'" )  

    If err.number<>0 Then  
        WScript.echo "Couldn't get Queries"  
        Exit Sub  
    End If  

    ' Run query.  
    WScript.echo query.Name  
    WScript.echo "----------------------------------"  

    Set queryResults=connection.ExecQuery(query.Expression)  
    For Each queryResult In queryResults  
        wscript.echo "     " & queryResult.Name  
    Next  
    If queryResults.Count=0 Then  
        WScript.echo "      no query results"  
    End If  
End Sub  
```  

```c#  
public void RunQuery(WqlConnectionManager connection, string queryId)  
{  
    try  
    {  
        // Get the query.  
        IResultObject query = connection.GetInstance(@"SMS_Query.QueryID='" + queryId + "'");  

        Console.WriteLine(query["Name"].StringValue);  
        Console.WriteLine("----------------------------------");  

        // Get the query results.  
        IResultObject queryResults = connection.QueryProcessor.ExecuteQuery(query["Expression"].StringValue);  

        bool resultsFound = false;  
        foreach (IResultObject queryResult in queryResults)  
        {  
            resultsFound = true;  
            Console.WriteLine(queryResult["Name"].StringValue);  
        }  
        if (resultsFound == false)  
        {  
            Console.WriteLine("     No query results");  
        }  
    }  
    catch (SmsException ex)  
    {  
        Console.WriteLine("Failed to run query: " + ex.Message);  
        throw;  
    }  
}  
```  

 The example method has the following parameters:  

||||  
|-|-|-|  
|Parameter|Type|Description|  
|`connection`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](https://msdn.microsoft.com/library/aa393854.aspx)|A valid connection to the SMS Provider.|  
|`queryID`|-   Managed: `String`<br />-   VBScript: `String`|A query identifier. For more information see the `SMS_Query` class `QueryID` property.|  

## Compiling the Code  
 The C# example has the following compilation requirements:  

### Namespaces  
 System  

 System.Collections.Generic  

 System.Text  

 Microsoft.ConfigurationManagement.ManagementProvider  

 Microsoft.ConfigurationManagement.ManagementProvider.WqlQueryEngine  

### Assembly  
 microsoft.configurationmanagement.managementprovider  

 adminui.wqlqueryengine  

## Robust Programming  
 For more information about error handling, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## .NET Framework Security  
 For more information about securing Configuration Manager applications, see [Securing Configuration Manager Applications](../../../develop/core/understand/securing-configuration-manager-applications.md).  

## See Also  
 [About Configuration Manager Queries](../../../develop/core/understand/about-configuration-manager-queries.md)   
 [How to Create a Configuration Manager Query](../../../develop/core/understand/how-to-create-a-configuration-manager-query.md)   
 [How to Perform an Asynchronous Configuration Manager Query by Using Managed Code](../../../develop/core/understand/how-to-perform-an-asynchronous-query-by-using-managed-code.md)   
 [How to Perform an Asynchronous Configuration Manager Query by Using WMI](../../../develop/core/understand/how-to-perform-an-asynchronous-configuration-manager-query-by-using-wmi.md)
