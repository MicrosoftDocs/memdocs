---
title: Create a Query
titleSuffix: Configuration Manager
description: Create an SMS_Query-based query by creating an instance of SMS_Query. The SMS_Query class Expression object defines a WQL query.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: how-to
ms.assetid: 08642b5a-210f-4d60-8544-b9519cbff053
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# How to Create a Configuration Manager Query
In Configuration Manager, you create an `SMS_Query`-based query by creating an instance of `SMS_Query`. The `SMS_Query` class `Expression` object defines a WQL query. If you want to limit the query results to a specific collection, specify the collection identifier in the `LimitToCollectionID` property.  

> [!NOTE]
>  When you create a query, it is displayed in the Configuration Manager console under **Queries**.  

### To create a query  

1.  Set up a connection to the SMS Provider. For more information, see [SMS Provider fundamentals](sms-provider-fundamentals.md).  

2.  Create an instance of [SMS_Query](../../../develop/reference/core/clients/manage/sms_query-server-wmi-class.md).  

3.  Populate the `SMS_Query` properties.  

4.  Commit the `SMS_Query`.  

5.  If required, retrieve the query object and get the query identifier.  

## Example  
 The following example method creates an `SMS_Query` class query that queries for all systems. The method returns the query identifier, which can be used as input to the example in [How to Run a Configuration Manager Query](../../../develop/core/understand/how-to-run-a-query.md).  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Function CreateQuery(connection)  
   On Error Resume Next  

   Dim query  
   Dim path  

   ' Create a query object.  
    Set query = connection.Get("SMS_Query").SpawnInstance_()  

    If Err.Number<>0 Then  
        Wscript.Echo "Couldn't create query object"  
        CreateQuery = Null  
        Exit Function  
    End If  

    ' Populate the object.  
    query.Comments = "A query for all systems"  
    query.Expression = "select Name, " + _  
    "SMSAssignedSites, " +              _  
    "IPAddresses, " +                   _  
    "IPSubnets, " +                     _  
    "OperatingSystemNameandVersion, " + _  
    "ResourceDomainORWorkgroup, " +     _  
    "LastLogonUserDomain, " +           _  
    "LastLogonUserName, " +             _  
    "SMSUniqueIdentifier, " +           _  
    "ResourceId, " +                    _  
    "ResourceType, " +                  _  
    "NetbiosName " +                    _  
    "from sms_r_system"  
    query.LimitToCollectionID = nothing  
    query.Name = "Query All Systems"  
    query.TargetClassName = "SMS_R_System"  

    ' Commit the object  
    path = query.Put_  

    If Err.Number<>0 Then  
        Wscript.Echo "Couldn't commit the query"  
        CreateQuery = Null  
        Exit Function  
    End If  

    WScript.Echo "Query created"  

    ' Get the object back to get the query identifier.  
    Set query = connection.Get(path)  
    CreateQuery = query.QueryID  

End Function  

```  

```c#  
public string CreateQuery(WqlConnectionManager connection)  
{  
    try  
    {  
        // Create an SMS_Query object.  
        IResultObject query = connection.CreateInstance("SMS_Query");  

        // Populate the object.  
        query["Comments"].StringValue = "A query for all systems";  
        query["Expression"].StringValue =   
            "select Name, " +  
            "SMSAssignedSites, " +  
            "IPAddresses, " +  
            "IPSubnets, " +  
            "OperatingSystemNameandVersion, " +  
            "ResourceDomainORWorkgroup, " +  
            "LastLogonUserDomain, " +  
            "LastLogonUserName, " +  
            "SMSUniqueIdentifier, " +  
            "ResourceId, " +  
            "ResourceType, " +  
            "NetbiosName " +  
            "from sms_r_system";  
        query["LimitToCollectionID"].StringValue = null;  
        query["Name"].StringValue = "Query All Systems";  
        query["TargetClassName"].StringValue = "SMS_R_System";  

        // Commit the query.  
        query.Put();  

        // Get the query - allows access to the queryID.  
        query.Get();  

        // Return the query identifier.  
        return query["QueryID"].StringValue;  
    }  
    catch (SmsException e)  
    {  
        Console.WriteLine("Failed to run the query: " + e.Message);  
        throw;  
    }  
}  

```  

 The example method has the following parameters:  

| Parameter | Type | Description |
| --------- | ---- | ----------- |
|`connection`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](/windows/win32/wmisdk/swbemservices)|-   A valid connection to the SMS Provider.|  

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
 For more information about securing Configuration Manager applications, see [Configuration Manager role-based administration](../../../develop/core/servers/configure/role-based-administration.md).  

## See Also  
 [About Configuration Manager Queries](../../../develop/core/understand/about-configuration-manager-queries.md)   
 [How to Run a Configuration Manager Query](../../../develop/core/understand/how-to-run-a-query.md)
