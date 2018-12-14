---
title: "Delete a Collection"
titleSuffix: "Configuration Manager"
ms.date: 12/06/2016
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 18161bed-17b9-49df-bb83-20082f519bd8
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# How to Delete a Collection
Your application can delete a collection in System Center Configuration Manager by using the [SMS_Collection Server WMI Class](../../../../develop/reference/core/clients/collections/sms_collection-server-wmi-class.md) and class properties.  

> [!IMPORTANT]
>
> - Care should be exercised when deleting any System Center Configuration Manager object.
>
> - We recommend that if you are deleting several collections, you do so one at a time, to allow database operations time to manage changes associated with the deletions.  

 Collections are closely tied to packages, programs, and advertisements. For more information, see [Software Distribution Overview](../../../../develop/core/servers/configure/software-distribution-overview.md).  

 These examples require the following values:  

- A Windows Management Instrumentation (WMI) connection object.  

- An existing collection ID.  

  The following code is an example of the subroutine call in Visual Basic:  

```  
Call DeleteCollection(swbemServices,"ABC00010")  
```  

 The following code is an example of the method call in C#:  

```  
DeleteCollection(WMIConnection,"ABC00010")  
```  

### To delete a collection  

1.  Set up a connection to the SMS Provider. For more information, see [About the SMS Provider in Configuration Manager](../../../../develop/core/understand/about-the-sms-provider-in-configuration-manager.md).  

2.  Get the specific collection instance by using the collection ID provided.  

3.  Delete the collection by using the delete method.  

## Example  
 The following example method deletes a collection.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../../develop/core/understand/calling-code-snippets.md).  

```vbs  

' Setup a connection to the local provider.  
Set swbemLocator = CreateObject("WbemScripting.SWbemLocator")  
Set swbemServices= swbemLocator.ConnectServer(".", "root\sms")  
Set providerLoc = swbemServices.InstancesOf("SMS_ProviderLocation")  

For Each Location In providerLoc  
    If location.ProviderForLocalSite = True Then  
        Set swbemServices = swbemLocator.ConnectServer(Location.Machine, "root\sms\site_" + Location.SiteCode)  
        Exit For  
    End If  
Next  

Call DeleteCollection(swbemServices,"ABC00010")  

Sub DeleteCollection(connection, collectionIDToDelete)  

    ' Get the specific collection instance to delete.  
    Set collectionToDelete = connection.Get("SMS_Collection.CollectionID='" & collectionIDToDelete & "'")  

    ' Delete the collection.  
    collectionToDelete.Delete_  

    ' Display change information.  
    Wscript.Echo "Deleted collection: " & collectionIDToDelete  

End Sub  
```  

```c#  
public void DeleteCollection(WqlConnectionManager connection, string collectionIDToDelete)  
{  
    //  Note:  On delete, the provider cleans up the SMS_CollectionSettings and SMS_CollectToSubCollect objects.  

    try  
    {  
        // Get the specific collection instance to delete.  
        IResultObject collectionToDelete = connection.GetInstance(@"SMS_Collection.CollectionID='" + collectionIDToDelete + "'");  

        // Delete the collection.  
        collectionToDelete.Delete();  

        // Output the ID of the deleted collection.  
        Console.WriteLine("Deleted collection: " + collectionIDToDelete);  
    }  

    catch (SmsException ex)  
    {  
        Console.WriteLine("Failed to delete collection. Error: " + ex.Message);  
        throw;  
    }  
}  

```  

 The example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`connection`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](https://msdn.microsoft.com/library/aa393854.aspx)|A valid connection to the SMS Provider.|  
|`collectionIDToDelete`|-   Managed: `String`<br />-   VBScript: `String`|Unique auto-generated ID containing eight characters. For more information, see the `CollectionID` property of [SMS_Collection Server WMI Class](../../../../develop/reference/core/clients/collections/sms_collection-server-wmi-class.md).|  

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
 [Configuration Manager Collections](../../../../develop/core/clients/collections/collections.md)   
 [Configuration Manager Software Distribution](../../../../develop/core/servers/configure/software-distribution.md)   
 [Software Distribution Packages](../../../../develop/core/servers/configure/software-distribution-packages.md)   
 [Software Distribution Programs](../../../../develop/core/servers/configure/software-distribution-programs.md)   
 [Software Distribution Advertisements](../../../../develop/core/servers/configure/software-distribution-advertisements.md)   
 [How to Use Configuration Manager Objects With WMI](../../../../develop/core/understand/how-to-use-configuration-manager-objects-with-wmi.md)   
 [How to Use Configuration Manager Objects With Managed Code](../../../../develop/core/understand/how-to-use-configuration-manager-objects-with-managed-code.md)   
 [How to Connect to a Configuration Manager Provider using Managed Code](../../../../develop/core/understand/how-to-connect-to-an-sms-provider-by-using-managed-code.md)   
 [How to Connect to a Configuration Manager Provider Using WMI](../../../../develop/core/understand/how-to-connect-to-an-sms-provider-in-configuration-manager-by-using-wmi.md)
