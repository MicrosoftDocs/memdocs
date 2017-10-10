---
title: "Create an Advertisement"
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
ms.assetid: 97f583d0-701b-41e5-8897-4e64bec0b85bsearchScope: - ConfigMgr SDK
caps.latest.revision: 11
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Create an Advertisement
The following example shows how to create an advertisement by using the `SMS_Advertisement` class and class properties in System Center Configuration Manager.  

> [!IMPORTANT]
>  To create an advertisement that targets a collection, you must have "Deploy Packages" permissions for the collection and "Read" permissions for the package.  

### To create an advertisement  

1.  Set up a connection to the SMS Provider.  

2.  Create the new advertisement object using the `SMS_Advertisement` class.  

3.  Populate the new advertisement properties.  

4.  Save the new advertisement and properties.  

## Example  
 The following example method creates an advertisement for software distribution.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../../develop/core/understand/calling-code-snippets.md).  

```vbs  

Sub SWDCreateAdvertisement(connection, existingCollectionID, existingPackageID, existingProgramName, newAdvertisementName, newAdvertisementComment, newAdvertisementFlags, newAdvertisementStartOfferDateTime, newAdvertisementStartOfferEnabled)  
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
    newAdvertisement.PresentTime = newAdvertisementStartOfferDateTime  
    newAdvertisement.PresentTimeEnabled = newAdvertisementStartOfferEnabled  

    ' Save the new advertisement and properties.  
    newAdvertisement.Put_   

    ' Output new advertisement name.  
    Wscript.Echo "Created advertisement: " & newAdvertisement.AdvertisementName  

End Sub  
```  

```c#  
public void CreateSWDAdvertisement(WqlConnectionManager connection, string existingCollectionID, string existingPackageID, string existingProgramName, string newAdvertisementName, string newAdvertisementComment, int newAdvertisementFlags, string newAdvertisementStartOfferDateTime, bool newAdvertisementStartOfferEnabled)  
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
        newAdvertisement["PresentTime"].StringValue = newAdvertisementStartOfferDateTime;  
        newAdvertisement["PresentTimeEnabled"].BooleanValue = newAdvertisementStartOfferEnabled;  

        // Save the new advertisment and properties.  
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
|`connection`<br /><br /> `swbemServices`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](https://msdn.microsoft.com/library/aa393854.aspx)|A valid connection to the SMS Provider.|  
|`existingCollectionID`|-   Managed: `String`<br />-   VBScript: `String`|The ID of an existing collection with which to associate the advertisement.|  
|`existingPackageID`|-   Managed: `String`<br />-   VBScript: `String`|The ID of an existing package with which to associate the advertisement.|  
|`existingProgramName`|-   Managed: `String`<br />-   VBScript: `String`|The name for the program associated with the advertisement.|  
|`newAdvertisementName`|-   Managed: `String`<br />-   VBScript: `String`|The name for the new advertisement.|  
|`newAdvertisementComment`|-   Managed: `String`<br />-   VBScript: `String`|A comment for the new advertisement.|  
|`newAdvertisementFlags`|-   Managed: `Integer`<br />-   VBScript: `Integer`|Flags specifying options for the new advertisement.|  
|`newAdvertisementStartOfferDateTime`|-   Managed: `String`<br />-   VBScript: `String`|The time when the new advertisement is first offered.|  
|`newAdvertisementStartOfferEnabled`|-   Managed: `Boolean`<br />-   VBScript: `Boolean`|`true` if the advertisement is offered.|  

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
