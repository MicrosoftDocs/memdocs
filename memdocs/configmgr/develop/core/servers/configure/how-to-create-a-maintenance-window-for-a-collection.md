---
title: Create a Maintenance Window for a Collection
titleSuffix: Configuration Manager
description: Your application can create a Configuration Manager maintenance window by using the SMS_CollectionSettings Server WMI Class and SMS_ServiceWindow Server WMI Classes and properties.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: how-to
ms.assetid: 4be75225-213b-4a32-a704-71c1fbc700e9
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# How to Create a Maintenance Window for a Collection
Your application can create a Configuration Manager maintenance window by using the [SMS_CollectionSettings Server WMI Class](../../../../develop/reference/core/clients/collections/sms_collectionsettings-server-wmi-class.md) and [SMS_ServiceWindow Server WMI Class](../../../../develop/reference/core/servers/configure/sms_servicewindow-server-wmi-class.md) classes and properties.  

### To create a maintenance window  

1.  Set up a connection to the SMS Provider. For more information, see [SMS Provider fundamentals](../../understand/sms-provider-fundamentals.md).  

2.  Get the existing collection settings instance by using the supplied collection ID.  

3.  Create and populate the properties of a new service window object by using the [SMS_ServiceWindow Server WMI Class](../../../../develop/reference/core/servers/configure/sms_servicewindow-server-wmi-class.md) class.  

4.  Add the new `SMS_ServiceWindow` object to the collection settings instance obtained earlier.  

5.  Save the collection settings instance and properties.  

> [!NOTE]
>  The example below includes additional steps, primarily to handle the overhead of dealing with the maintenance window objects, which are stored as embedded objects in the collection settings instance.  

## Example  
 The following example method creates a maintenance window for a collection, assuming that the collection instance can modified. This might not be the case at child sites, where the collections are owned by the parent site(s).  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../../develop/core/understand/calling-code-snippets.md).  

```vbs  

Sub CreateMaintenanceWindow(connection,                                 _  
                            targetCollectionID,                         _  
                            newMaintenanceWindowName,                   _  
                            newMaintenanceWindowDescription,            _  
                            newMaintenanceWindowServiceWindowSchedules, _  
                            newMaintenanceWindowIsEnabled,              _  
                            newMaintenanceWindowServiceWindowType)  

    ' Build a query to get the specified collection.   
     collectionSettingsQuery = "SMS_CollectionSettings.CollectionID='" & targetCollectionID & "'"  

    ' Get the collection settings instance for the targetCollectionID.  
    Set allCollectionSettings = connection.ExecQuery("Select * From SMS_CollectionSettings Where CollectionID = '" & targetCollectionID & "'")  

    ' If a collection settings instance does not exist for the target collection, create one.  
    If allCollectionSettings.Count = 0 Then  
        Wscript.Echo "Creating collection settings instance."  
        Set collectionSettingsInstance = connection.Get("SMS_CollectionSettings").SpawnInstance_  
        collectionSettingsInstance.CollectionID = targetCollectionID  
        collectionSettingsInstance.Put_  
    End If    

    ' Get the specific collection settings instance.  
    Set collectionSettingsInstance = connection.Get("SMS_CollectionSettings.CollectionID='" & targetCollectionID &"'" )  

    ' Create and populate a temporary SMS_ServiceWindow object with the new maintenance window values.   
    Set tempServiceWindowObject = connection.Get("SMS_ServiceWindow").SpawnInstance_  

    ' Populate temporary SMS_ServiceWindow object with the new maintenance window values.  
    tempServiceWindowObject.Name = newMaintenanceWindowName  
    tempServiceWindowObject.Description = newMaintenanceWindowDescription  
    tempServiceWindowObject.ServiceWindowSchedules = newMaintenanceWindowServiceWindowSchedules  
    tempServiceWindowObject.IsEnabled = newMaintenanceWindowIsEnabled  
    tempServiceWindowObject.ServiceWindowType = newMaintenanceWindowServiceWindowType  

    ' Populate the local array list with the existing service window objects (from the target collection).  
    tempServiceWindowArray = collectionSettingsInstance.ServiceWindows  

    ' Add the newly created service window object to the temporary array.  
    ReDim Preserve tempServiceWindowArray (Ubound(tempServiceWindowArray) + 1)  
    Set tempServiceWindowArray(Ubound(tempServiceWindowArray)) = tempServiceWindowObject  

    ' Replace the existing service window objects from the target collection with the temporary array that includes the new service window.  
    collectionSettingsInstance.ServiceWindows = tempServiceWindowArray  

    ' Save the collection settings instance with the new service window object.  
    collectionSettingsInstance.Put_  

    ' Output success message.  
    wscript.echo "New Maintenance Window created."  

End Sub  

```  

```c#  

public void CreateMaintenanceWindow(WqlConnectionManager connection,   
                                    string targetCollectionID,   
                                    string newMaintenanceWindowName,   
                                    string newMaintenanceWindowDescription,   
                                    string newMaintenanceWindowServiceWindowSchedules,   
                                    bool newMaintenanceWindowIsEnabled,   
                                    int newMaintenanceWindowServiceWindowType)  
{  
    try  
    {  
        // Create an object to hold the collection settings instance (used to check whether a collection settings instance exists).   
        IResultObject collectionSettingsInstance = null;  

        // Get the collection settings instance for the targetCollectionID.  
        IResultObject allCollectionSettings = connection.QueryProcessor.ExecuteQuery("Select * from SMS_CollectionSettings where CollectionID='" + targetCollectionID + "'");  

        // Enumerate the allCollectionSettings collection (there should be just one item) and save the instance.  
        foreach (IResultObject collectionSetting in allCollectionSettings)  
        {  
            collectionSettingsInstance = collectionSetting;  
        }  

        // If a collection settings instance does not exist for the target collection, create one.  
        if (collectionSettingsInstance == null)  
        {  
            collectionSettingsInstance = connection.CreateInstance("SMS_CollectionSettings");  
            collectionSettingsInstance["CollectionID"].StringValue = targetCollectionID;  
            collectionSettingsInstance.Put();  
            collectionSettingsInstance.Get();  
        }  

        // Create a new array list to hold the service window object.  
        List<IResultObject> tempServiceWindowArray = new List<IResultObject>();  

        // Create and populate a temporary SMS_ServiceWindow object with the new maintenance window values.  
        IResultObject tempServiceWindowObject = connection.CreateEmbeddedObjectInstance("SMS_ServiceWindow");  

        // Populate temporary SMS_ServiceWindow object with the new maintenance window values.  
        tempServiceWindowObject["Name"].StringValue = newMaintenanceWindowName;  
        tempServiceWindowObject["Description"].StringValue = newMaintenanceWindowDescription;  
        tempServiceWindowObject["ServiceWindowSchedules"].StringValue = newMaintenanceWindowServiceWindowSchedules;  
        tempServiceWindowObject["IsEnabled"].BooleanValue = newMaintenanceWindowIsEnabled;  
        tempServiceWindowObject["ServiceWindowType"].IntegerValue = newMaintenanceWindowServiceWindowType;  

        // Populate the local array list with the existing service window objects (from the target collection).  
        tempServiceWindowArray = collectionSettingsInstance.GetArrayItems("ServiceWindows");  

        // Add the newly created service window object to the local array list.  
        tempServiceWindowArray.Add(tempServiceWindowObject);  

        // Replace the existing service window objects from the target collection with the temporary array that includes the new service window.  
        collectionSettingsInstance.SetArrayItems("ServiceWindows", tempServiceWindowArray);  

        // Save the new values in the collection settings instance associated with the target collection.  
        collectionSettingsInstance.Put();  
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
|`connection`<br /><br /> `swebemServices`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](/windows/win32/wmisdk/swbemservices)|A valid connection to the SMS Provider.|  
|`targetCollectionID`|-   Managed: `String`<br />-   VBScript: `String`|The ID of the collection.|  
|`newMaintenanceWindowName`|-   Managed: `String`<br />-   VBScript: `String`|The name of the new maintenance window.|  
|`newMaintenanceWindowDescription`|-   Managed: `String`<br />-   VBScript: `String`|The description of the new maintenance window.|  
|`newMaintenanceWindowServiceWindowSchedules`|-   Managed: `String`<br />-   VBScript: `String`|The service schedules for the new maintenance window.|  
|`newMaintenanceWindowIsEnabled`|-   Managed: `Boolean`<br />-   VBScript: `Boolean`|`true` if the new maintenance window is enabled.|  
|`newMaintenanceWindowServiceWindowType`|-   Managed: `Integer`<br />-   VBScript: `Integer`|Type for the new maintenance window.|  

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
 [About schedules](../../understand/about-configuration-manager-schedules.md)
 [How to Create a Schedule Token](../../../../develop/core/understand/how-to-create-a-schedule-token.md)
