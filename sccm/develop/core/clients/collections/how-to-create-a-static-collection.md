---
title: "Create a Static Collection"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 53023832-57ca-47f9-96bb-ab8ab4827172
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# How to Create a Static Collection
In System Center Configuration Manager, your application uses [SMS_Collection Server WMI Class](../../../../develop/reference/core/clients/collections/sms_collection-server-wmi-class.md) to define the attributes of a collection, such as the membership rules and the refresh schedule. The `MemberClassName` property contains the system-generated class name that contains the members of the collection.  

 Members of a collection are specified by using direct rules, query rules, or both. Direct rules define an explicit resource, and query rules define a dynamic collection that is regularly evaluated based on the current state of the site.  

> [!NOTE]
>  When creating a direct membership rule, remember that the rule must always have the same name as the computer that the rule specifies.  

 Your application uses the [SMS_CollectionRuleDirect Server WMI Class](../../../../develop/reference/core/clients/collections/sms_collectionruledirect-server-wmi-class.md) class to define direct rules. This approach is used for resources that are static in nature. For example, if you have a limited number of licenses for a particular software application, the application should use direct rules to advertise to specific computers or users.  

 Collections are closely tied to packages, programs and advertisements. For more information, see [Software Distribution Overview](../../../../develop/core/servers/configure/software-distribution-overview.md).  

 The following examples require the following values:  

-   A Windows Management Instrumentation (WMI) connection object.  

-   A new static collection name.  

-   A new static collection comment.  

-   The 'owned by this site' flag.  

-   A resource class name.  

-   A resource ID.  

-   A collection identifier to limit the scope of membership.  

> [!NOTE]
>  If the All Systems (SMS00001) collection has been removed from the site server, the VBScript example will not work.  

 Example of the subroutine call in Visual Basic:  

```  
Call CreateStaticCollection(swbemconnection, "New Static Collection Name", "New static collection comment.", true, "SMS_R_System", 2, "SMS00001")  
```  

 Example of the method call in C#:  

```  
CreateStaticCollection (WMIConnection, "New Static Collection Name", "New static collection comment.", true, "SMS_R_System", 2, "SMS00001")  
```  

### To create a static collection  

1.  Set up a connection to the SMS Provider. For more information, see [About the SMS Provider in Configuration Manager](../../../../develop/core/understand/about-the-sms-provider-in-configuration-manager.md).  

2.  Create the new collection object by using the [SMS_Collection Server WMI Class](../../../../develop/reference/core/clients/collections/sms_collection-server-wmi-class.md) class.  

3.  Create the direct rule by using the [SMS_CollectionRuleDirect Server WMI Class](../../../../develop/reference/core/clients/collections/sms_collectionruledirect-server-wmi-class.md) class.  

4.  Add the rule to the collection.  

5.  Refresh the collection.  

## Example  
 The following example method creates a collection.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../../develop/core/understand/calling-code-snippets.md).  

```vbs  

' Set up a connection to the local provider.  
Set swbemLocator = CreateObject("WbemScripting.SWbemLocator")  
Set swbemconnection= swbemLocator.ConnectServer(".", "root\sms")  
Set providerLoc = swbemconnection.InstancesOf("SMS_ProviderLocation")  

For Each Location In providerLoc  
    If location.ProviderForLocalSite = True Then  
        Set swbemconnection = swbemLocator.ConnectServer(Location.Machine, "root\sms\site_" + Location.SiteCode)  
        Exit For  
    End If  
Next  

Call CreateStaticCollection(swbemconnection, "New Static Collection Name", "New static collection comment.", true, "SMS_R_System", 2, "SMS00001")  

Sub CreateStaticCollection(connection, newCollectionName, newCollectionComment, ownedByThisSite, resourceClassName, resourceID, limitToCollectionID)  

    ' Create the collection.  
    Set newCollection = connection.Get("SMS_Collection").SpawnInstance_  
    newCollection.Comment = newCollectionComment  
    newCollection.Name = newCollectionName  
    newCollection.OwnedByThisSite = ownedByThisSite  
    newCollection.LimitToCollectionID = limitToCollectionID  

    ' Save the new collection and save the collection path for later.  
    Set collectionPath = newCollection.Put_      

    ' Create the direct rule.  
    Set newDirectRule = connection.Get("SMS_CollectionRuleDirect").SpawnInstance_  
    newDirectRule.ResourceClassName = resourceClassName  
    newDirectRule.ResourceID = resourceID  

    ' Add the new query rule to a variable.  
    Set newCollectionRule = newDirectRule  

    ' Get the collection.  
    Set newCollection = connection.Get(collectionPath.RelPath)  

    ' Add the rules to the collection.  
    newCollection.AddMembershipRule newCollectionRule  

    ' Call RequestRefresh to initiate the collection evaluator.   
    newCollection.RequestRefresh False  

End Sub  
```  

```c#  
public void CreateStaticCollection(WqlConnectionManager connection, string newCollectionName, string newCollectionComment, bool ownedByThisSite, string resourceClassName, int resourceID, string limitToCollectionID)  
{  
    try  
    {  
        // Create a new SMS_Collection object.  
        IResultObject newCollection = connection.CreateInstance("SMS_Collection");  

        // Populate new collection properties.  
        newCollection["Name"].StringValue = newCollectionName;  
        newCollection["Comment"].StringValue = newCollectionComment;  
        newCollection["OwnedByThisSite"].BooleanValue = ownedByThisSite;  
        newCollection["LimitToCollectionID"].StringValue = limitToCollectionID;   

        // Save the new collection object and properties.    
        // In this case, it seems necessary to 'get' the object again to access the properties.    
        newCollection.Put();  
        newCollection.Get();  

        // Create a new static rule object.  
        IResultObject newStaticRule = connection.CreateInstance("SMS_CollectionRuleDirect");  
        newStaticRule["ResourceClassName"].StringValue = resourceClassName;  
        newStaticRule["ResourceID"].IntegerValue = resourceID;  

        // Add the rule. Although not used in this sample, staticID contains the query identifier.                     
        Dictionary<string, object> addMembershipRuleParameters = new Dictionary<string, object>();  
        addMembershipRuleParameters.Add("collectionRule", newStaticRule);  
        IResultObject staticID = newCollection.ExecuteMethod("AddMembershipRule", addMembershipRuleParameters);  

        // Start collection evaluator.  
        Dictionary<string, object> requestRefreshParameters = new Dictionary<string, object>();  
        requestRefreshParameters.Add("IncludeSubCollections", false);  
        newCollection.ExecuteMethod("RequestRefresh", requestRefreshParameters);  

        // Output message.  
        Console.WriteLine("Created collection" + newCollectionName);  
    }  

    catch (SmsException ex)  
    {  
        Console.WriteLine("Failed to create collection. Error: " + ex.Message);  
        throw;  
    }  
}  
```  

 The example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`connection`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](https://msdn.microsoft.com/library/aa393854.aspx)|A valid connection to the SMS Provider.|  
|`newCollectionName`|-   Managed: `String`<br />-   VBScript: `String`|The unique name that represents the collection in the Configuration Manager console.|  
|`newCollectionComment`|-   Managed: `String`<br />-   VBScript: `String`|General comment or note that documents the collection.|  
|`ownedByThisSite`|-   Managed: `Boolean`<br />-   VBScript: `Boolean`|`true` if the collection originated at the local Configuration Manager site.|  
|`resourceClassName`|-   Managed: `String`<br />-   VBScript: `String`|The resource name of the static rule object.|  
|`resourceID`|-   Managed: `Integer`<br />-   VBScript: `Integer`|The resource ID.|  
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
 For more information about securing Configuration Manager applications, see [Securing Configuration Manager Applications](../../../../develop/core/understand/securing-configuration-manager-applications.md).  

## See Also  
 [SMS_Collection Server WMI Class](../../../../develop/reference/core/clients/collections/sms_collection-server-wmi-class.md)   
 [SMS_CollectionRuleDirect Server WMI Class](../../../../develop/reference/core/clients/collections/sms_collectionruledirect-server-wmi-class.md)   
 [Configuration Manager Collections](../../../../develop/core/clients/collections/collections.md)   
 [Configuration Manager Software Distribution](../../../../develop/core/servers/configure/software-distribution.md)   
 [Software Distribution Packages](../../../../develop/core/servers/configure/software-distribution-packages.md)   
 [Software Distribution Programs](../../../../develop/core/servers/configure/software-distribution-programs.md)   
 [Software Distribution Advertisements](../../../../develop/core/servers/configure/software-distribution-advertisements.md)   
 [How to Use Configuration Manager Objects with WMI](../../../../develop/core/understand/how-to-use-configuration-manager-objects-with-wmi.md)   
 [How to Use Configuration Manager Objects with Managed Code](../../../../develop/core/understand/how-to-use-configuration-manager-objects-with-managed-code.md)   
 [How to Connect to an SMS Provider in Configuration Manager by Using Managed Code](../../../../develop/core/understand/how-to-connect-to-an-sms-provider-by-using-managed-code.md)   
 [How to Connect to an SMS Provider in Configuration Manager by Using WMI](../../../../develop/core/understand/how-to-connect-to-an-sms-provider-in-configuration-manager-by-using-wmi.md)
