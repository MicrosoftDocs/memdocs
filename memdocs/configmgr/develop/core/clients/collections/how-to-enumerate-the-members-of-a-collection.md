---
title: "Enumerate the Members of a Collection"
titleSuffix: "Configuration Manager"
description: "In Configuration Manager, the preferred method to enumerate through a collection is to use SMS_FullCollectionMembership Server WMI Class."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: b6405754-0475-4a07-a6ff-1adc76de3815
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3


---
# How to Enumerate the Members of a Collection
In Configuration Manager, the preferred method to enumerate through a collection is to use `SMS_FullCollectionMembership Server WMI Class`.  

 **Query 1: SMS_FullCollectionMembership**: This example shows how to enumerate the members of the All Systems (SMS00001) collection by using the `SMS_FullCollectionMembership Server WMI Class`.  

 **Query 2: SMS_CollectionMember_a**: This example shows a slower alternative, by using the [SMS_CollectionMember_a Server WMI Class](../../../../develop/reference/core/clients/collections/sms_collectionmember_a-server-wmi-class.md) class.  

 **Query 3: SMS_Collection**: This example shows a further alternative, which is to query the members by using the actual collection class name that is specified in the `MemberClassName` property of [SMS_Collection Server WMI Class](../../../../develop/reference/core/clients/collections/sms_collection-server-wmi-class.md). Querying the actual class offers performance advantages and lets you create more complex queries, such as JOINs. The example is equivalent to the earlier queries.  

> [!NOTE]
>  When the SMS Provider first initializes, it registers and dynamically loads the SMS collection class into memory. If a WQL query is made against the collection class before it is loaded, an empty query result set will be returned.  

 Collections are closely tied to packages, programs and advertisements. For more information, see [Software Distribution Overview](../../../../develop/core/servers/configure/software-distribution-overview.md).  

 These examples require the following values:  

- A Windows Management Instrumentation (WMI) connection object.  

  Example of the subroutine call in Visual Basic:  

```  
Call EnumerateCollectionMembers(swbemServices)  
```  

 Example of the method call in C#:  

```  
EnumerateCollectionMembers(WMIConnection)  
```  

### To enumerate the members of a collection  

1.  Set up a connection to the SMS Provider.  

2.  Define a query to select the resources for the collection.  

3.  Execute the query and enumerate the results.  

## Example  
 The following example method enumerates the members of a collection.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../../develop/core/understand/calling-code-snippets.md).  

```vbs  

Sub EnumerateCollectionMembers(connection)  
    Const wbemFlagReturnImmediately = 16    Const wbemFlagForwardOnly = 32  
    ' Set required variables.  
    ' Note:  Values must be manually added to the queries below.  
    Dim Query1    Dim Query2    Dim Query3    Dim ListOfResources1    Dim ListOfResources2    Dim ListOfResources3    Dim Resource1    Dim Resource2    Dim Resource3  
    ' The following example shows how to enumerate the members of the All Systems (SMS00001) collection.  
    Query1 = "SELECT ResourceID FROM SMS_FullCollectionMembership WHERE CollectionID = 'SMS00001'"   

    ' Run query.  
    Set ListOfResources1 = connection.ExecQuery(Query1, , wbemFlagForwardOnly Or wbemFlagReturnImmediately)  

    ' The query returns a collection that needs to be enumerated.  
    Wscript.Echo " "  
    Wscript.Echo "Query: " & Query1  
    For Each Resource1 In ListOfResources1       
        Wscript.Echo Resource1.ResourceID     
    Next  

    ' A slower alternative is to use the SMS_CollectionMember_a association class.  
    Query2 = "SELECT ResourceID FROM SMS_CollectionMember_a WHERE CollectionID = 'SMS00001'"   

    ' Run query.  
    Set ListOfResources2 = connection.ExecQuery(Query2, , wbemFlagForwardOnly Or wbemFlagReturnImmediately)  

    ' The query returns a collection that needs to be enumerated.  
    Wscript.Echo " "  
    Wscript.Echo "Query: " & Query2  
    For Each Resource2 In ListOfResources2       
        Wscript.Echo Resource2.ResourceID     
    Next  

    ' A further alternative is to query the members by using the actual collection class name specified in the MemberClassName property of SMS_Collection.   
    Query3 = "SELECT ResourceID FROM SMS_CM_Res_Coll_SMS00001"   

    ' Run query.  
    Set ListOfResources3 = connection.ExecQuery(Query3, , wbemFlagForwardOnly Or wbemFlagReturnImmediately)  

    ' The query returns a collection that needs to be enumerated.  
    Wscript.Echo " "  
    Wscript.Echo "Query: " & Query3  
    For Each Resource3 In ListOfResources3       
        Wscript.Echo Resource3.ResourceID     
    Next  

End Sub  
```  

```c#  
public void EnumerateCollectionMembers(WqlConnectionManager connection)  
{  
    // Set required variables.  
    // Note:  Values must be manually added to the queries below.  

    try  
    {  
        // The following example shows how to enumerate the members of the All Systems (SMS00001) collection.  
        string Query1 = "SELECT ResourceID FROM SMS_FullCollectionMembership WHERE CollectionID = 'SMS00001'";  

        // Run query.  
        IResultObject ListOfResources1 = connection.QueryProcessor.ExecuteQuery(Query1);  

        // The query returns a collection that needs to be enumerated.  
        Console.WriteLine(" ");  
        Console.WriteLine("Query: " + Query1);  
        foreach (IResultObject Resource1 in ListOfResources1)  
        {  
            Console.WriteLine(Resource1["ResourceID"].IntegerValue);  
        }  

        // A slower alternative is to use the SMS_CollectionMember_a association class.  
        string Query2 = "SELECT ResourceID FROM SMS_CollectionMember_a WHERE CollectionID = 'SMS00001'";  

        // Run query.  
        IResultObject ListOfResources2 = connection.QueryProcessor.ExecuteQuery(Query2);  

        // The query returns a collection that needs to be enumerated.  
        Console.WriteLine(" ");  
        Console.WriteLine("Query: " + Query2);  
        foreach (IResultObject Resource2 in ListOfResources2)  
        {  
            Console.WriteLine(Resource2["ResourceID"].IntegerValue);  
        }  

        // A further alternative is to query the members by using the actual collection class name specified in the MemberClassName property of SMS_Collection.  
        string Query3 = "SELECT ResourceID FROM SMS_CM_Res_Coll_SMS00001";  

        // Run query.  
        IResultObject ListOfResources3 = connection.QueryProcessor.ExecuteQuery(Query3);  

        // The query returns a collection that needs to be enumerated.  
        Console.WriteLine(" ");  
        Console.WriteLine("Query: " + Query3);  
        foreach (IResultObject Resource3 in ListOfResources3)  
        {  
            Console.WriteLine(Resource3["ResourceID"].IntegerValue);  
        }  
    }  

    catch (SmsException eX)  
    {  
        Console.WriteLine("Failed to run queries. Error: " + eX.Message);  
        throw;  
    }  
}  
```  

 The example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`connection`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](/windows/win32/wmisdk/swbemservices)|A valid connection to the SMS Provider.|  

## Compiling the Code  
 The C# example requires:  

### Namespaces  
 System  

 Microsoft.ConfigurationManagement.ManagementProvider  

 Microsoft.ConfigurationManagement.ManagementProvider.WqlQueryEngine  

### Assembly  
 adminui.wqlqueryengine  

 microsoft.configurationmanagement.managementprovider  

 mscorlib  

## Robust Programming  
 For more information about error handling, see [About Configuration Manager Errors](../../../../develop/core/understand/about-configuration-manager-errors.md).  

## See Also  
 [SMS_CollectionMember_a Server WMI Class](../../../../develop/reference/core/clients/collections/sms_collectionmember_a-server-wmi-class.md)   
 [SMS_Collection Server WMI Class](../../../../develop/reference/core/clients/collections/sms_collection-server-wmi-class.md)   
 [Software distribution overview](../../servers/configure/software-distribution-overview.md)
 [About deployments](../../servers/configure/about-software-distribution-deployments.md)
