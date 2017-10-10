---
title: "Change Maintenance Window Properties for a Collection"
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
ms.assetid: c73f7ea3-5f13-4b93-897e-ef865418ccfdsearchScope: - ConfigMgr SDK
caps.latest.revision: 9
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Change the Maintenance Window Properties for a Collection
You can change maintenance window properties for a collection, in System Center Configuration Manager, by using the [SMS_CollectionSettings Server WMI Class](../../../../develop/reference/core/clients/collections/sms_collectionsettings-server-wmi-class.md) and [SMS_ServiceWindow Server WMI Class](../../../../develop/reference/core/servers/configure/sms_servicewindow-server-wmi-class.md) classes and properties.  

### To change the properties of a maintenance window  

1.  Set up a connection to the SMS Provider. For more information, see [About the SMS Provider in Configuration Manager](../../../../develop/core/understand/about-the-sms-provider-in-configuration-manager.md).  

2.  Get the existing collection settings instance by using the existing collection ID provided.  

3.  Get the existing service window object by using the existing service window ID provided.  

4.  Change an existing property value (in this case the maintenance window description).  

5.  Save the collection settings instance and properties.  

> [!NOTE]
>  The steps in the example method include additional steps, primarily to handle the overhead of dealing with the service window objects, which are stored as embedded objects in the collection settings instance.  

## Example  
 The following example method changes the properties of a specific maintenance window instance.  

> [!IMPORTANT]
>  This assumes that the collection instance can modified. This might not be the case at child sites, where the collections are owned by the parent site(s).  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../../develop/core/understand/calling-code-snippets.md).  

```vbs  

Sub ChangeMaintenanceWindowProperties(connection,                                 _  
                                      targetCollectionID,                         _  
                                      targetServiceWindowID,                            _  
                                      newMaintenanceWindowDescription,            _  
                                      newMaintenanceWindowServiceWindowSchedules, _  
                                      newMaintenanceWindowIsEnabled)  

    ' Get the specific collection settings instance.  
    Set collectionSettingsInstance = connection.Get("SMS_CollectionSettings.CollectionID='" & targetCollectionID &"'" )  

    ' Populate the local array list with the existing service window objects (from the target collection).  
    tempMaintenanceWindowArray = collectionSettingsInstance.ServiceWindows   

    ' Enumerate through the array list to access each maintenance window object.  
    For Each maintenanceWindow in tempMaintenanceWindowArray  

         ' If the service window ID matches the one passed in to the function, change the specific values.  
         If maintenanceWindow.ServiceWindowID = targetServiceWindowID Then          

            ' Populate retrieved SMS_ServiceWindow object with the new maintenance window values.      
            maintenanceWindow.Description = newMaintenanceWindowDescription  
            maintenanceWindow.ServiceWindowSchedules = newMaintenanceWindowServiceWindowSchedules  
            maintenanceWindow.IsEnabled = newMaintenanceWindowIsEnabled            

         End If  

    Next  

    ' Replace the existing service window objects from the target collection with the temporary array that includes the modified service window.  
    collectionSettingsInstance.ServiceWindows = tempMaintenanceWindowArray  

    ' Save the new values in the collection settings instance associated with the collection ID.  
    collectionSettingsInstance.Put_  

    ' Output success message.  
    wscript.echo "Maintenance Window " & targetServiceWindowID & " modified."  

End Sub  

```  

```c#  

public void ChangeMaintenanceWindowProperties(WqlConnectionManager connection,  
                                              string targetCollectionID,  
                                              string serviceWindowID,  
                                              string newMaintenanceWindowDescription)  
{  
    try  
    {  
        // Create a new array list to hold the service window objects.  
        List<IResultObject> tempMaintenanceWindowArray = new List<IResultObject>();  

        // Establish connection to collection settings instance associated with the Collection ID.  
        IResultObject collectionSettings = connection.GetInstance(@"SMS_CollectionSettings.CollectionID='" + targetCollectionID + "'");  

        // Populate the array list with the existing service window objects (from the target collection).  
        tempMaintenanceWindowArray = collectionSettings.GetArrayItems("ServiceWindows");  

        // Enumerate through the array list to access each maintenance window object.  
        foreach (IResultObject maintenanceWindow in tempMaintenanceWindowArray)  
        {  
            // If the service window ID matches the one passed in to the function, change the specific values.  
            if (maintenanceWindow["ServiceWindowID"].StringValue == serviceWindowID)  
            {  
                maintenanceWindow["Description"].StringValue = newMaintenanceWindowDescription;  
                break;  
            }  
        }  

        // Replace the existing service window objects from the target collection with the temporary array that includes the new service window.  
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
|`connection`<br /><br /> `swebemServices`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](https://msdn.microsoft.com/library/aa393854.aspx)|A valid connection to the SMS Provider.|  
|`targetCollectionID`|-   Managed: `String`<br />-   VBScript: `String`|The ID of the collection.|  
|`serviceWindowID`|-   Managed: `String`<br />-   VBScript: `String`|The ID of the maintenance window for which to change properties.|  
|`newMaintenanceWindowDescription`|-   Managed: `String`<br />-   VBScript: `String`|The description of the new maintenance window.|  

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
 [Software Distribution Maintenance Windows](../../../../develop/core/servers/configure/software-distribution-maintenance-windows.md)   
 [Software Distribution Packages](../../../../develop/core/servers/configure/software-distribution-packages.md)   
 [Software Distribution Programs](../../../../develop/core/servers/configure/software-distribution-programs.md)   
 [Software Distribution Advertisements](../../../../develop/core/servers/configure/software-distribution-advertisements.md)   
 [Configuration Manager Collections](../../../../develop/core/clients/collections/collections.md)   
 [Configuration Manager Software Distribution](../../../../develop/core/servers/configure/software-distribution.md)   
 [How to Use Configuration Manager Objects With WMI](../../../../develop/core/understand/how-to-use-configuration-manager-objects-with-wmi.md)   
 [How to Use Configuration Manager Objects With Managed Code](../../../../develop/core/understand/how-to-use-configuration-manager-objects-with-managed-code.md)   
 [How to Connect to a Configuration Manager Provider using Managed Code](../../../../develop/core/understand/how-to-connect-to-an-sms-provider-by-using-managed-code.md)   
 [How to Connect to a Configuration Manager Provider Using WMI](../../../../develop/core/understand/how-to-connect-to-an-sms-provider-in-configuration-manager-by-using-wmi.md)   
 [SMS_CollectionSettings Server WMI Class](../../../../develop/reference/core/clients/collections/sms_collectionsettings-server-wmi-class.md)   
 [SMS_ServiceWindow Server WMI Class](../../../../develop/reference/core/servers/configure/sms_servicewindow-server-wmi-class.md)   
 [Configuration Manager Schedules](../../../../develop/core/understand/schedules.md)   
 [How to Create a Schedule Token](../../../../develop/core/understand/how-to-create-a-schedule-token.md)
