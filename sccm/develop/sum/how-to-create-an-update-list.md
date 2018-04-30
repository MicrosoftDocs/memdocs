---
title: "Create an Update List"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 21702068-b002-4f19-b84a-6e63fb032678
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# How to Create an Update List
You create an update list that contains a set of software updates, in System Center Configuration Manager, by creating an instance of the [SMS_AuthorizationList](../../develop/reference/sum/sms_authorizationlist-server-wmi-class.md) class and populating the properties.  

### To create an update list  

1.  Set up a connection to the SMS Provider.  

2.  Create the new update list object using the `SMS_AuthorizationList` class.  

3.  Populate the new update list properties.  

4.  Save the new update list and properties.  

## Example  
 The following example method shows how to create an update list that contains a set of software updates by creating an instance of the `SMS_AuthorizationList` class and populating the properties.  

> [!IMPORTANT]
>  The `LocalizedInformation` property that is used in this example requires an object array (embedded array) of the description information.  

 In the example, the `LocaleID` property is hard-coded to English (U.S.). If you need the locale for non-U.S. installations, you can get it from the [SMS_Identification Server WMI Class](../../develop/reference/core/servers/configure/sms_identification-server-wmi-class.md) `LocaleID` property.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

 The following example shows the subroutine call in Visual Basic:  

```  

' Prework for CreateSUMUpdateList  
' Create the array of CI_IDs.  
dim newUpdates   
newUpdates = Array(9)  

' Create and populate an SMS_CI_LocalizedProperties object.  
set SMSCILocalizedProperties = swbemservices.Get("SMS_CI_LocalizedProperties").SpawnInstance_  

SMSCILocalizedProperties.Description = "Test Description"  
SMSCILocalizedProperties.DisplayName = "Test Display Name"  
SMSCILocalizedProperties.InformativeURL = "Test URL"  
SMSCILocalizedProperties.LocaleID = "1033"  

' Create an array to hold the SMS_CI_LocalizedProperties object.  
dim newDescriptionInfo  
newDescriptionInfo = Array(SMSCILocalizedProperties)  

' Call the CreateSUMUpdateList method.  
Call CreateSUMUpdateList(swbemServices,       _  
                         newUpdates,          _  
                         newDescriptionInfo)  
```  

 The following example shows the method call in C#:  

```  

// Prework for CreateSUMUpdateList  
// Create array list (to hold the array of Localized Properties).  
List<IResultObject> newDescriptionInfo = new List <IResultObject>();    
IResultObject SMSCILocalizedProperties = WMIConnection.CreateEmbeddedObjectInstance("SMS_CI_LocalizedProperties");  

// Populate the initial array values (this could be a loop to added more localized info).  
SMSCILocalizedProperties["Description"].StringValue = "4 CI_IDs - 9,34,53,72 ";  
SMSCILocalizedProperties["DisplayName"].StringValue = "Test Display Name";   
SMSCILocalizedProperties["InformativeURL"].StringValue = "Test URL";  
SMSCILocalizedProperties["LocaleID"].StringValue = "1033";  

// Add the 'embedded properties' to newDescriptionInfo.  
newDescriptionInfo.Add(SMSCILocalizedProperties);  

// Create the array of CI_IDs.  
int[] newCI_ID = new int[] { 9, 34, 53, 72 };  

// Call the CreateSUMUpdateList method.  
SUMSnippets.CreateSUMUpdateList(WMIConnection,  
                                newCI_ID,  
                                newDescriptionInfo);  

```  

```vbs  

Sub CreateSUMUpdateList(connection,         _  
                        newUpdates,         _  
                        newDescriptionInfo)                                  

    ' Create the new UpdateList object.   
    Set newUpdateList = connection.Get("SMS_AuthorizationList").SpawnInstance_  

    ' Populate the UpdateList properties.  
    ' Updates is an int32 array that maps to the CI_ID in SMS_SoftwareUpdate.  
    newUpdateList.Updates = newUpdates  
    ' Need to pass embedded properties (LocalizedInformation) here.   
    newUpdateList.LocalizedInformation = newDescriptionInfo  

    ' Save the new UpdateList and properties.  
    newUpdateList.Put_   

    ' Output the new UpdateList name.  
    Wscript.Echo "Created Update List " & newUpdateList.LocalizedDisplayName                    

End Sub  
```  

```c#  

public void CreateSUMUpdateList(WqlConnectionManager connection,                                   
                                 int [] newUpdates,  
                                 List<IResultObject> newDescriptionInfo)  
{  
    try  
    {  
        // Create the new SMS_AuthorizationList object.  
        IResultObject newUpdateList = connection.CreateInstance("SMS_AuthorizationList");  

        // Populate the new SMS_AuthorizationList object properties.  
        // Updates is an int32 array that maps to the CI_ID in SMS_SoftwareUpdate.  
        newUpdateList["Updates"].IntegerArrayValue = newUpdates;  
        // Pass embedded properties (LocalizedInformation) here.  
        newUpdateList.SetArrayItems("LocalizedInformation", newDescriptionInfo);  

        // Save changes.  
        newUpdateList.Put();  

        Console.WriteLine();  
        Console.WriteLine("Created Update List. " );  

    }  

    catch (SmsException ex)  
    {  
        Console.WriteLine("Failed to create update list. Error: " + ex.Message);  
        throw;  
    }  
}  

```  

 The example method has the following parameters:  

||||  
|-|-|-|  
|Parameter|Type|Description|  
|`Connection`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](https://msdn.microsoft.com/library/aa393854.aspx)|A valid connection to the SMS Provider.|  
|`newUpdates`|-   Managed: `Integer` array<br />-   VBScript: `Integer` array|An array of the updates that is associated with the Update List.|  
|`newDescriptionInfo`|-   Managed: `Object` array<br />-   VBScript: `Object` array|An object array (embedded properties) of the type `LocalizedInformation`.|  

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
 For more information about error handling, see [About Configuration Manager Errors](../../develop/core/understand/about-configuration-manager-errors.md).  

## .NET Framework Security  
 For more information about securing Configuration Manager applications, see [Securing Configuration Manager Applications](../../develop/core/understand/securing-configuration-manager-applications.md).  

## See Also  
 [System Center Configuration Manager Software Development Kit](../../develop/core/misc/system-center-configuration-manager-sdk.md)   
 [Configuration Manager Software Updates](../../develop/sum/software-updates.md)   
 [Other Deployment Options](../../develop/sum/synchronizing-the-software-update-point.md)   
 [SMS_AuthorizationList](../../develop/reference/sum/sms_authorizationlist-server-wmi-class.md)
