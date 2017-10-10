---
title: "Assign an Advertisement to a Collection of Computers"
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
ms.assetid: fc94ef17-5ecf-44a9-9805-585ce5b8f402searchScope: - ConfigMgr SDK
caps.latest.revision: 12
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Assign an Advertisement to a Collection of Computers
You can assign an advertisement to a collection by using the `SMS_Advertisement` class in System Center Configuration Manager. Advertisements are closely tied to packages, programs and collections. For more information, see [Software Distribution Overview](../../../../develop/core/servers/configure/software-distribution-overview.md).  

> [!NOTE]
>  Detailed information about the `SMS_Advertisement` class and class properties is in the reference section of the System Center Configuration Manager Software Development Kit (SDK).  

### To assign an advertisement to a collection  

1.  Set up a connection to the SMS Provider.  

2.  Get the specific advertisement using the existing advertisement ID.  

3.  Populate the advertisement collection ID property with the existing collection ID.  

4.  Save the advertisement and properties.  

## Example  
 The following example method assigns a specific advertisement to a collection for use in software distribution.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../../develop/core/understand/calling-code-snippets.md).  

```vbs  

Sub SWDAssignAdvertisementCollection(connection, existingAdvertisementID, existingCollectionID)  

    ' Get the specific advertisement object.  
    Set advertisementToAssign = connection.Get("SMS_Advertisement.AdvertisementID='" & existingAdvertisementID & "'")  

    ' Fill the advertisement properties for collection.  
    advertisementToAssign.CollectionID = existingCollectionID  

    ' Save the advertisement.  
    advertisementToAssign.Put_  

    ' Output advertisement and collection information.  
    Wscript.Echo "Assigned advertisement: " & existingAdvertisementID  
    Wscript.Echo "                        " & advertisementToAssign.AdvertisementName  
    Wscript.Echo "To collection:          " & advertisementToAssign.CollectionID  

End Sub  
```  

```c#  
public void AssignSWDAdvertisementToCollection(WqlConnectionManager connection, string existingAdvertisementID, string existingCollectionID)  
{  
    try  
    {  
        // Get specific advertisement instance (using the passed in value existingAdvertisementID).  
        IResultObject advertisementToAssign = connection.GetInstance(@"SMS_Advertisement.AdvertisementID='" + existingAdvertisementID + "'");  

        // Populate the collection id property of the advertisement.  
        advertisementToAssign["CollectionID"].StringValue = existingCollectionID;  

        // Save the advertisment and properties.  
        advertisementToAssign.Put();  

        // Output advertisment and collection information.  
        Console.WriteLine("Assigned advertisement: " + existingAdvertisementID);  
        Console.WriteLine("                        " + advertisementToAssign["AdvertisementName"].StringValue);  
        Console.WriteLine("To collection:          " + existingCollectionID);  
    }  
    catch (SmsException ex)  
    {  
        Console.WriteLine("Failed to assign advertisement. Error: " + ex.Message);  
        throw;  
    }  
}  
```  

 The example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`connection`<br /><br /> `swebemServices`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](https://msdn.microsoft.com/library/aa393854.aspx)|A valid connection to the SMS Provider.|  
|`existingAdvertisementID`|-   Managed: `String`<br />-   VBScript: `String`|The ID of an existing advertisement.|  
|`existingCollectionID`|-   Managed: `String`<br />-   VBScript: `String`|The ID of an existing collection.|  

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
 [Configuration Manager Software Distribution](../../../../develop/core/servers/configure/software-distribution.md)   
 [Software Distribution Advertisements](../../../../develop/core/servers/configure/software-distribution-advertisements.md)   
 [SMS_Collection Server WMI Class](../../../../develop/reference/core/clients/collections/sms_collection-server-wmi-class.md)
