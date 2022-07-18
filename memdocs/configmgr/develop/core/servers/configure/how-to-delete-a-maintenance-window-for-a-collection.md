---
description: Learn how to delete a maintenance window for a collection in Configuration Manager with the following example.
title: "Delete a Maintenance Window for a Collection"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: 257a15d2-4408-41ae-9277-77acca0cc914
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# How to Delete a Maintenance Window for a Collection
You can delete maintenance window, in Configuration Manager, by using the [SMS_CollectionSettings Server WMI Class](../../../../develop/reference/core/clients/collections/sms_collectionsettings-server-wmi-class.md) and [SMS_ServiceWindow Server WMI Class](../../../../develop/reference/core/servers/configure/sms_servicewindow-server-wmi-class.md) classes and properties.  

### To delete a maintenance window for a collection  

1.  Set up a connection to the SMS Provider. For more information, see [SMS Provider fundamentals](../../understand/sms-provider-fundamentals.md).  

2.  Get an existing collection settings instance by using the collection ID provided.  

3.  Get the existing service window object by using the maintenance window ID provided.  

4.  Delete the existing maintenance window.  

5.  Save the collection settings instance and properties.  

> [!NOTE]
>  The example method includes additional steps, primarily to handle the overhead of dealing with the service window objects, which are stored as embedded objects in the collection settings instance.  

## Example  
 The following example method deletes a specific maintenance window instance for a collection.  

> [!IMPORTANT]
>  This assumes that the collection instance can modified. This might not be the case at child sites, where the collections are owned by the parent site or sites.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../../develop/core/understand/calling-code-snippets.md).  

```c#  
public void DeleteMaintenanceWindowfromCollection(WqlConnectionManager connection,   
                                                  string targetCollectionID,   
                                                  string serviceWindowID)  
{  
    try  
    {  
        // Create a new array list to hold the service window objects.  
        List<IResultObject> tempMaintenanceWindowArray = new List<IResultObject>();  

        // Establish connection to collection settings instance associated with the target collection ID.  
        IResultObject collectionSettings = connection.GetInstance(@"SMS_CollectionSettings.CollectionID='" + targetCollectionID + "'");  

        // Populate the array list with the existing service window objects (from the target collection).  
        tempMaintenanceWindowArray = collectionSettings.GetArrayItems("ServiceWindows");  

        // Enumerate through the array list to access each maintenance window object.  
        foreach (IResultObject maintenanceWindow in tempMaintenanceWindowArray)  
        {  
            // If the maintenance window ID matches the one passed in to the function, delete the maintenance window.  
            if (maintenanceWindow["ServiceWindowID"].StringValue == serviceWindowID)  
            {  
                tempMaintenanceWindowArray.Remove(maintenanceWindow);  
                Console.WriteLine("Deleted:");  
                Console.WriteLine("Maintenance Window Name: " + maintenanceWindow["Name"].StringValue);  
                Console.WriteLine("Maintenance Windows Service Window ID: " + maintenanceWindow["ServiceWindowID"].StringValue);  
                break;  
            }  
        }  

        // Replace the existing service window objects from the target collection with the temporary array that includes the new maintenance window.  
        collectionSettings.SetArrayItems("ServiceWindows", tempMaintenanceWindowArray);  

        // Save the new values in the collection settings instance associated with the Collection ID.  
        collectionSettings.Put();  
    }  

    catch (SmsException ex)  
    {  
        Console.WriteLine("Failed. Error: " + ex.InnerException.Message);  
        throw;  
    }  
}  

```  

 The example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`connection`|-   Managed: `WqlConnectionManager`|A valid connection to the SMS Provider.|  
|`targetCollectionID`|-   Managed: `String`|The ID of the collection.|  
|`serviceWindowID`|-   Managed: `String`|The ID of the maintenance window to delete.|  

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
 [About maintenance windows](about-maintenance-windows.md)
 [Software distribution overview](software-distribution-overview.md)
 [About deployments](about-software-distribution-deployments.md)
 [Objects overview](../../understand/configuration-manager-objects-overview.md)
 [How to Connect to a Configuration Manager Provider using Managed Code](../../../../develop/core/understand/how-to-connect-to-an-sms-provider-by-using-managed-code.md)   
 [How to Connect to a Configuration Manager Provider Using WMI](../../../../develop/core/understand/how-to-connect-to-an-sms-provider-in-configuration-manager-by-using-wmi.md)   
 [SMS_CollectionSettings Server WMI Class](../../../../develop/reference/core/clients/collections/sms_collectionsettings-server-wmi-class.md)   
 [SMS_ServiceWindow Server WMI Class](../../../../develop/reference/core/servers/configure/sms_servicewindow-server-wmi-class.md)
