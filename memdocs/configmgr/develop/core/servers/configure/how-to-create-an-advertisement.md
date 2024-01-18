---
title: Create a deployment
titleSuffix: Configuration Manager
description: Examples of how to programmatically create a Configuration Manager deployment.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: how-to
ms.assetid: 97f583d0-701b-41e5-8897-4e64bec0b85b
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# How to create a deployment

The following examples show how to create a Configuration Manager deployment with the [SMS_Advertisement](../../../reference/core/servers/configure/sms_advertisement-server-wmi-class.md) class and its properties.

> [!IMPORTANT]
> The account that creates the deployment needs the **Deploy Packages** permission for the collection and **Read** permission for the package.

## Overview

1. Set up a connection to the SMS Provider.

1. Create a new object of the `SMS_Advertisement` class.

1. Populate the new advertisement properties.

1. Save the new advertisement and properties.

## Examples

The following examples create an advertisement for software distribution.

For more information about calling the sample code, see [Calling Configuration Manager code snippets](../../understand/calling-code-snippets.md).

```vbs
Sub SWDCreateAdvertisement(connection, existingCollectionID, existingPackageID, existingProgramName, newAdvertisementName, newAdvertisementComment, newAdvertisementFlags, newRemoteClientFlags, newAdvertisementStartOfferDateTime, newAdvertisementStartOfferEnabled)  
    Dim newAdvertisement  
    ' Create the new advertisement object.  
    Set newAdvertisement = connection.Get("SMS_Advertisement").SpawnInstance_  

    ' Populate the advertisement properties.  
    newAdvertisement.CollectionID = existingCollectionID  
    newAdvertisement.PackageID = existingPackageID  
    newAdvertisement.ProgramName = existingProgramName  
    newAdvertisement.AdvertisementName = newAdvertisementName  
    newAdvertisement.Comment = newAdvertisementComment  
    newAdvertisement.AdvertFlags = newAdvertisementFlags  
    newAdvertisement.RemoteClientFlags = newRemoteClientFlags
    newAdvertisement.PresentTime = newAdvertisementStartOfferDateTime  
    newAdvertisement.PresentTimeEnabled = newAdvertisementStartOfferEnabled  

    ' Save the new advertisement and properties.  
    newAdvertisement.Put_   

    ' Output new advertisement name.  
    Wscript.Echo "Created advertisement: " & newAdvertisement.AdvertisementName  

End Sub  
```  

```c#  
public void CreateSWDAdvertisement(WqlConnectionManager connection, string existingCollectionID, string existingPackageID, string existingProgramName, string newAdvertisementName, string newAdvertisementComment, int newAdvertisementFlags, int newRemoteClientFlags, string newAdvertisementStartOfferDateTime, bool newAdvertisementStartOfferEnabled)  
{  
    try  
    {  
        // Create new advertisement instance.  
        IResultObject newAdvertisement = connection.CreateInstance("SMS_Advertisement");  

        // Populate new advertisement values.  
        newAdvertisement["CollectionID"].StringValue = existingCollectionID;  
        newAdvertisement["PackageID"].StringValue = existingPackageID;  
        newAdvertisement["ProgramName"].StringValue = existingProgramName;  
        newAdvertisement["AdvertisementName"].StringValue = newAdvertisementName;  
        newAdvertisement["Comment"].StringValue = newAdvertisementComment;  
        newAdvertisement["AdvertFlags"].IntegerValue = newAdvertisementFlags;  
        newAdvertisement["RemoteClientFlag"].IntegerValue = newRemoteClientFlags;
        newAdvertisement["PresentTime"].StringValue = newAdvertisementStartOfferDateTime;  
        newAdvertisement["PresentTimeEnabled"].BooleanValue = newAdvertisementStartOfferEnabled;  

        // Save the new advertisement and properties.  
        newAdvertisement.Put();  

        // Output new assignment name.  
        Console.WriteLine("Created advertisement: " + newAdvertisement["AdvertisementName"].StringValue);  
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
|`connection`<br /><br /> `swbemServices`|- Managed: `WqlConnectionManager`<br />- VBScript: [SWbemServices](/windows/desktop/WmiSdk/swbemservices)|A valid connection to the SMS Provider.|  
|`existingCollectionID`|String|The ID of an existing collection with which to associate the advertisement.|  
|`existingPackageID`|String|The ID of an existing package with which to associate the advertisement.|  
|`existingProgramName`|String|The name for the program associated with the advertisement.|  
|`newAdvertisementName`|String|The name for the new advertisement.|  
|`newAdvertisementComment`|String|A comment for the new advertisement.|  
|`newAdvertisementFlags`|Integer|Flags specifying options for the new advertisement.|  
|`newRemoteClientFlags`|Integer| Flags specifying how the program should run when the client connects either locally or remotely to a distribution point.|
|`newAdvertisementStartOfferDateTime`|String|The time when the new advertisement is first offered.|  
|`newAdvertisementStartOfferEnabled`|Boolean|`true` if the advertisement is offered.|  

## Compiling the code

The C# example requires:  

### Namespaces

- `System`

- `Microsoft.ConfigurationManagement.ManagementProvider`

- `Microsoft.ConfigurationManagement.ManagementProvider.WqlQueryEngine`

### Assembly

- `adminui.wqlqueryengine`

- `microsoft.configurationmanagement.managementprovider`

- `mscorlib`

## Robust programming

For more information about error handling, see [About Configuration Manager errors](../../understand/about-configuration-manager-errors.md).

## See also

- [Software distribution overview](software-distribution-overview.md)
- [About deployments](about-software-distribution-deployments.md)
