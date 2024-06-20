---
title: Apply custom client settings
titleSuffix: Configuration Manager
description: Use the SDK to apply custom client settings.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: how-to
ms.assetid: b171d930-dd3f-4587-ad24-058448fcfa30
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
---

# How to apply custom client settings

In Configuration Manager, you apply custom client settings by creating an instance of a Client Configuration class, and then deploying the custom client settings by creating an instance of the `SMS_ClientSettingsAssignment` class and associating the instance of the Client Configuration class and a target collection.  

### To apply custom client settings

1.  Set up a connection to the SMS Provider.  

2.  Create an instance of a Client Configuration class (such as `SMS_StateSystemConfig` used below).  

3.  Populate specific custom client agent settings.  

4.  Create an instance of the `SMS_ClientSettingsAssignment` class.  

5.  Populate the client settings assignment values. `ClientSettingsID` to identify the custom client settings instance and `CollectionID` to identify the target collection for the deployment of the custom client settings.  

## Example

The following example applies custom client settings by creating an instance of a Client Configuration class, and then deploying the custom client settings by creating an instance of the `SMS_ClientSettingsAssignment` class and associating the instance of the Client Configuration class and a target collection.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../../develop/core/understand/calling-code-snippets.md).  

```c#  

public void ApplyCustomClientSettings(WqlConnectionManager connection,string targetCollectionID){
    try
    {
        // Create a new instance of specific client agent settings (in this case State Messaging)
        IResultObject newCustomClientAgentSettings = connection.CreateEmbeddedObjectInstance("SMS_StateSystemConfig");

        // Populate specific custom client agent settings
        newCustomClientAgentSettings["BulkSendInterval"].IntegerValue = 120;
        newCustomClientAgentSettings["BulkSendIntervalHigh"].IntegerValue = 5;
        newCustomClientAgentSettings["BulkSendIntervalLow"].IntegerValue = 30;

        // Create a new array list to hold the custom client agent settings object(s)
        List<IResultObject> tempAgentConfigurationsArray = new List<IResultObject>();

        // Add the custom client agent settings embedded object to the local array list
        tempAgentConfigurationsArray.Add(newCustomClientAgentSettings);

        // Create a new instance of SMS_ClientSettings
        IResultObject newClientSettings = connection.CreateInstance("SMS_ClientSettings");

        // Populate the client agent settings
        newClientSettings["Name"].StringValue = "Custom State Messaging Configuration";

        // Add the array of custom client agent settinsg object(s) to the AgentConfigurations property
        newClientSettings.SetArrayItems("AgentConfigurations", tempAgentConfigurationsArray);

        // Save and retrieve the new instance of SMS_ClientSettings
        newClientSettings.Put();
        newClientSettings.Get();

        // Get the SettingsID value of the new SMS_ClientSettings instance
        Int32 SettingsID = newClientSettings["SettingsID"].IntegerValue;

        // Create a new instance of SMS_ClientSettingsAssignment
        IResultObject newClientSettingsAssignment = connection.CreateInstance("SMS_ClientSettingsAssignment");

        // Populate the client settings assignment values
        // ClientSettingsID to identify the custom client settings
        // CollectionID to identify the target collection for the custom client settings
        newClientSettingsAssignment["ClientSettingsID"].IntegerValue = SettingsID;
        newClientSettingsAssignment["CollectionID"].StringValue = targetCollectionID;

        // Save the new instance of the client settings assignment.
        newClientSettingsAssignment.Put();
    }
    catch (SmsException ex)
    {
        Console.WriteLine("Failed. Error: " + ex.InnerException.Message);
    }
}
```  

 The example method has the following parameters:  

| Parameter | Type | Description |
| --------- | ---- | ----------- |
|`connection`|-   Managed: `WqlConnectionManager`|A valid connection to the SMS Provider.|  
|`targetCollectionID`|-   Managed: `String`|The target collection for the custom client settings deployment.|  

## Compiling the Code  
 This C# example requires:  

### Namespaces  
 System  

 System.Collections.Generic  

 System.Text  

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
 [Configuration Manager SDK](../../../../develop/core/misc/system-center-configuration-manager-sdk.md)   
 [SMS_ClientSettingsAssignment Server WMI Class](../../../../develop/reference/core/clients/config/sms_clientsettingsassignment-server-wmi-class.md)
