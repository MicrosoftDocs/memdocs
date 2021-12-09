---
title: "Create a Dynamic Collection"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: 7d27ea5b-8941-4453-b90b-35d9ad2891eb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# How to Create a Dynamic Collection
In Configuration Manager, your application uses the [SMS_Collection Server WMI Class](../../../../develop/reference/core/clients/collections/sms_collection-server-wmi-class.md) to define the attributes of a collection, such as the membership rules and the refresh schedule. The `MemberClassName` property contains the system-generated class name that contains the members of the collection.  

 Members of a collection are specified by using direct rules, query rules, or both. Direct rules define an explicit resource, whereas query rules define a dynamic collection that is regularly evaluated based on the current state of the site.  

> [!NOTE]
>  When creating a direct membership rule, remember that the rule must always have the same name as the computer that the rule specifies.  

 Your application uses the [SMS_CollectionRuleQuery Server WMI Class](../../../../develop/reference/core/clients/collections/sms_collectionrulequery-server-wmi-class.md) class to define query rules. The query must be valid and can specify the collection to contain resources such as "All users in the corporate domain." The application can then use the query to ensure that a program is targeted for software distribution to all computers that meet the criteria. As the site changes and the collection is re-evaluated, members of the collection are automatically added and deleted.  

> [!NOTE]
>  When running a query against a dynamic collection, ensure that the SMS Provider is loaded or that another method or query has already run.  

 Collections are closely tied to packages, programs and advertisements. For more information, see [Software Distribution Overview](../../../../develop/core/servers/configure/software-distribution-overview.md).  

 These examples require the following values:  

-   A Windows Management Instrumentation (WMI) connection object.  

-   A new dynamic collection name.  

-   A new dynamic collection comment.  

-   The 'owned by this site' flag.  

-   A query (string).  

-   A static rule name.  

-   A collection identifier to limit the scope of membership.  

> [!NOTE]
>  If the All Systems (SMS00001) collection has been removed from the site server, the VBScript example does not work.  

 Example of the subroutine call in Visual Basic:  

```  
Call CreateDynamicCollection(swbemconnection, "New Dynamic Collection Name", "New dynamic collection comment.", true, "SELECT * from SMS_R_System", "New Rule Name", "SMS00001")  
```  

 Example of the method call in C#:  

```  
CreateDynamicCollection(WMIConnection, "New Dynamic Collection Name", "New dynamic collection comment.", true, "SELECT * from SMS_R_System", "New Rule Name", "SMS00001")  
```  

### To create a dynamic collection  

1.  Set up a connection to the SMS Provider. For more information, see [SMS Provider fundamentals](../../understand/sms-provider-fundamentals.md).  

2.  Create the new collection object by using the [SMS_Collection Server WMI Class](../../../../develop/reference/core/clients/collections/sms_collection-server-wmi-class.md) class.  

3.  Create the rule by using the [SMS_CollectionRuleQuery Server WMI Class](../../../../develop/reference/core/clients/collections/sms_collectionrulequery-server-wmi-class.md) class.  

4.  Add the rule to the collection.  

5.  Refresh the collection.  

## Example  
 The following example method creates a dynamic collection by using the [SMS_Collection Server WMI Class](../../../../develop/reference/core/clients/collections/sms_collection-server-wmi-class.md) and the [SMS_CollectionRuleQuery Server WMI Class](../../../../develop/reference/core/clients/collections/sms_collectionrulequery-server-wmi-class.md) classes and class properties.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../../develop/core/understand/calling-code-snippets.md).  

```vbs  

' Setup a connection to the local provider.  
Set swbemLocator = CreateObject("WbemScripting.SWbemLocator")  
Set swbemconnection= swbemLocator.ConnectServer(".", "root\sms")  
Set providerLoc = swbemconnection.InstancesOf("SMS_ProviderLocation")  

For Each Location In providerLoc  
    If location.ProviderForLocalSite = True Then  
        Set swbemconnection = swbemLocator.ConnectServer(Location.Machine, "root\sms\site_" + Location.SiteCode)  
        Exit For  
    End If  
Next  

Call CreateDynamicCollection(swbemconnection, "New Dynamic Collection Name", "New dynamic collection comment.", true, "SELECT * from SMS_R_System", "New Rule Name", "SMS00001")  

Sub CreateDynamicCollection(connection, newCollectionName, newCollectionComment, ownedByThisSite, queryForRule, ruleName, limitToCollectionID)  

    ' Create the collection.  
    Set newCollection = connection.Get("SMS_Collection").SpawnInstance_  
    newCollection.Name = newCollectionName  
    newCollection.Comment = newCollectionComment  
    newCollection.OwnedByThisSite = ownedByThisSite  
    newCollection.LimitToCollectionID = limitToCollectionID  

    ' Save the new collection and save the collection path for later.  
    Set collectionPath = newCollection.Put_      

    ' Create a new collection rule object for validation.  
    Set queryRule = connection.Get("SMS_CollectionRuleQuery")  

    ' Validate the query (good practice before adding it to the collection).   
    validQuery = queryRule.ValidateQuery(queryForRule)  

    ' Continue with processing, if the query is valid.  
    If validQuery Then  

        ' Create the query rule.  
        Set newQueryRule = QueryRule.SpawnInstance_  
        newQueryRule.QueryExpression = queryForRule  
        newQueryRule.RuleName = ruleName  

        ' Add the new query rule to a variable.  
        Set newCollectionRule = newQueryRule  

        ' Get the collection.  
        Set newCollection = connection.Get(collectionPath.RelPath)  

        ' Add the rules to the collection.  
        newCollection.AddMembershipRule newCollectionRule  

        ' Call RequestRefresh to initiate the collection evaluator.  
        newCollection.RequestRefresh False  

    End If  

End Sub  
```  

```c#  
public void CreateDynamicCollection(WqlConnectionManager connection, string newCollectionName, string newCollectionComment, bool ownedByThisSite, string query, string ruleName, string LimitToCollectionID){    try    {        // Create new SMS_Collection object.        IResultObject newCollection = connection.CreateInstance("SMS_Collection");        // Populate the new collection object properties.        newCollection["Name"].StringValue = newCollectionName;        newCollection["Comment"].StringValue = newCollectionComment;        newCollection["OwnedByThisSite"].BooleanValue = ownedByThisSite;        newCollection["LimitToCollectionID"].StringValue = LimitToCollectionID;        // Save the new collection object and properties.        // In this case, it seems necessary to 'get' the object again to access the properties.        newCollection.Put();        newCollection.Get();        // Validate the query.        Dictionary<string, object> validateQueryParameters = new Dictionary<string, object>();        validateQueryParameters.Add("WQLQuery", query);        IResultObject result = connection.ExecuteMethod("SMS_CollectionRuleQuery", "ValidateQuery", validateQueryParameters);        // Create query rule.        IResultObject newQueryRule = connection.CreateInstance("SMS_CollectionRuleQuery");        newQueryRule["QueryExpression"].StringValue = query;        newQueryRule["RuleName"].StringValue = ruleName;        // Add the rule. Although not used in this sample, QueryID contains the query identifier.                           Dictionary<string, object> addMembershipRuleParameters = new Dictionary<string, object>();        addMembershipRuleParameters.Add("collectionRule", newQueryRule);        IResultObject queryID = newCollection.ExecuteMethod("AddMembershipRule", addMembershipRuleParameters);        // Start collection evaluator.        newCollection.ExecuteMethod("RequestRefresh", null);        Console.WriteLine("Created collection: " + newCollectionName);    }    catch (SmsException ex)    {        Console.WriteLine("Failed to create collection. Error: " + ex.Message);        throw;    }}   
```  

 The example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`connection`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](/windows/win32/wmisdk/swbemservices)|A valid connection to the SMS Provider.|  
|`newCollectionName`|-   Managed: `String`<br />-   VBScript: `String`|The unique name that represents the collection in the Configuration Manager console.|  
|`newCollectionComment`|-   Managed: `String`<br />-   VBScript: `String`|General comment or note that documents the collection.|  
|`ownedByThisSite`|-   Managed: `Boolean`<br />-   VBScript: `Boolean`|`true` if the collection originated at the local Configuration Manager site.|  
|`query`|-   Managed: `String`<br />-   VBScript: `String`|WQL SELECT statement having results that are used to populate the collection. The statement must specify a resource class name.|  
|`ruleName`|-   Managed: `String`<br />-   VBScript: `String`|Descriptive name that identifies the rule.|  
|`limitToCollectionID`|-   Managed: `String`<br />-   VBScript: `String`|Collection identifier to limit the scope of membership.|  

## Compiling the Code  
 The C# example requires:  

### Namespaces  
 System  

 System.Collections.Generic  

 System.ComponentModel  

 Microsoft.ConfigurationManagement.ManagementProvider  

 Microsoft.ConfigurationManagement.ManagementProvider.WqlQueryEngine  

### Assembly  
 adminui.wqlqueryengine  

 microsoft.configurationmanagement.managementprovider  

## Robust Programming  
 For more information about error handling, see [About Configuration Manager Errors](../../../../develop/core/understand/about-configuration-manager-errors.md).  

## .NET Framework Security  
 For more information about securing Configuration Manager applications, see [Configuration Manager role-based administration](../../../../develop/core/servers/configure/role-based-administration.md).  

## See Also  
 [SMS_Collection Server WMI Class](../../../../develop/reference/core/clients/collections/sms_collection-server-wmi-class.md)   
 [SMS_CollectionRuleQuery Server WMI Class](../../../../develop/reference/core/clients/collections/sms_collectionrulequery-server-wmi-class.md)   
 [Software distribution overview](../../servers/configure/software-distribution-overview.md)
 [About deployments](../../servers/configure/about-software-distribution-deployments.md)
 [Objects overview](../../understand/configuration-manager-objects-overview.md)
 [How to Connect to an SMS Provider in Configuration Manager by Using Managed Code](../../../../develop/core/understand/how-to-connect-to-an-sms-provider-by-using-managed-code.md)   
 [How to Connect to an SMS Provider in Configuration Manager by Using WMI](../../../../develop/core/understand/how-to-connect-to-an-sms-provider-in-configuration-manager-by-using-wmi.md)
