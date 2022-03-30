---
title: "Modify Advertisement Properties"
titleSuffix: "Configuration Manager"
description: "In Configuration Manager, the following example shows how to modify an existing advertisement by using the SMS_Advertisement class and class properties."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: 343783ae-0951-47cc-896e-bf74420fcb22
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# How to Modify Advertisement Properties
The following example shows how to modify an existing advertisement, in Configuration Manager, by using the `SMS_Advertisement` class and class properties.  

### To modify advertisement properties  

1.  Set up a connection to the SMS Provider.  

2.  Get the specific advertisement using an existing advertisement ID.  

3.  Replace the existing advertisement property (in this case, advertisement comment).  

4.  Save the new advertisement and properties.  

## Example  
 The following example method modifies advertisement properties for software distribution.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../../develop/core/understand/calling-code-snippets.md).  

```vbs  

Sub ModifyAdvertisement(connection, existingAdvertisementID, newAdvertisementComment )  
    Dim advertisementToModify  
    ' Get the specific advertisement instance to modify.   
    Set advertisementToModify = connection.Get("SMS_Advertisement.AdvertisementID='" & existingAdvertisementID & "'")  

    ' List the existing property values.  
    Wscript.Echo " "  
    Wscript.Echo "Values before change: "  
    Wscript.Echo "--------------------- "  
    Wscript.Echo "Advertisement Name: " & advertisementToModify.AdvertisementName  
    Wscript.Echo "Comment:            " & advertisementToModify.Comment  

    ' Set the new property value.  
    advertisementToModify.Comment = newAdvertisementComment  

    ' Save the advertisement.  
    advertisementToModify.Put_   

    ' Output the new property values.  
    Wscript.Echo " "  
    Wscript.Echo "Values after change:  "  
    Wscript.Echo "--------------------- "  
    Wscript.Echo "Advertisement Name: " & AdvertisementToModify.AdvertisementName  
    Wscript.Echo "Comment:            " & AdvertisementToModify.Comment  

End Sub  
```  

```c#  
public void ModifySWDAdvertisement(WqlConnectionManager connection, string existingAdvertisementID, string newAdvertisementComment)  
{  
    try  
    {  
        // Get the specific advertisement instance to modify.   
        IResultObject advertisementToModify = connection.GetInstance(@"SMS_Advertisement.AdvertisementID='" + existingAdvertisementID + "'");  

        // List the existing property values.  
        Console.WriteLine();  
        Console.WriteLine("Values before change:");  
        Console.WriteLine("_____________________");  
        Console.WriteLine("Advertisement Name: " + advertisementToModify["AdvertisementName"].StringValue);  
        Console.WriteLine("Comment: " + advertisementToModify["Comment"].StringValue);  

        // Set the new property value to  be modified.  
        advertisementToModify["Comment"].StringValue = newAdvertisementComment;  

        // Save the advertisement with the new value.  
        advertisementToModify.Put();  

        // Output the new property values.  
        Console.WriteLine();  
        Console.WriteLine("Values after change:");  
        Console.WriteLine("____________________");  
        Console.WriteLine("Advertisement Name: " + advertisementToModify["AdvertisementName"].StringValue);  
        Console.WriteLine("Comment: " + newAdvertisementComment);  
    }  
    catch (SmsException ex)  
    {  
        Console.WriteLine("Failed to modify advertisement. Error: " + ex.Message);  
        throw;  
    }  
}  
```  

 The example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`connection`<br /><br /> `swbemServices`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](/windows/win32/wmisdk/swbemservices)|A valid connection to the SMS Provider.|  
|`existingAdvertisementID`|-   Managed: `String`<br />-   VBScript: `String`|The ID of the advertisement to modify.|  
|`newAdvertisementComment`|-   Managed: `String`<br />-   VBScript: `String`|The new comment for the advertisement.|  

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
 [Software distribution overview](software-distribution-overview.md)
 [About deployments](about-software-distribution-deployments.md)
