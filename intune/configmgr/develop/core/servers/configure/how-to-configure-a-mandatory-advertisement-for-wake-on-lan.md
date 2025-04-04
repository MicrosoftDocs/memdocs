---
description: Learn how to configure an existing mandatory advertisement for Wake On LAN by using the SMS_Advertisement class and properties.
title: Configure a Mandatory Advertisement for Wake On LAN
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: how-to
ms.assetid: 4cf2d556-eda8-42c1-9ad2-2e1229798e98
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# How to Configure a Software Distribution Mandatory Advertisement for Wake On LAN
You can configure an existing mandatory advertisement for Wake On LAN by using the `SMS_Advertisement` class and properties.  

### To configure a mandatory advertisement for Wake On LAN  

1.  Set up a connection to the SMS Provider.  

2.  Get the specific advertisement using the provided advertisement ID.  

3.  Replace the `AdvertFlags` property value with the value indicating Wake On LAN.  

4.  Save the advertisement with the new property  

## Example  
 The following example method configures a software distribution mandatory advertisement for Wake On LAN.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../../develop/core/understand/calling-code-snippets.md).  

```vbs  

Sub SetWOLOnAdvertisment(connection, existingAdvertisementID)  

    ' Define a constant with the hexadecimal value for WAKE_ON_LAN_ENABLED.   
    Const WAKE_ON_LAN_ENABLED = &H00400000  
    Dim advertisementToModify  
    ' Get the specific advertisement instance to modify.   
    Set advertisementToModify = connection.Get("SMS_Advertisement.AdvertisementID='" & existingadvertisementID & "'")  

    ' List the existing property values.  
    Wscript.Echo " "  
    Wscript.Echo "Values before change: "  
    Wscript.Echo "--------------------- "  
    Wscript.Echo "Advertisement Name:            " & advertisementToModify.AdvertisementName  
    Wscript.Echo "Advertisement Flags (integer): " & advertisementToModify.AdvertFlags  

    ' Set the new property value.  
    advertisementToModify.AdvertFlags = advertisementToModify.AdvertFlags OR WAKE_ON_LAN_ENABLED  

    ' Save the advertisement.  
    advertisementToModify.Put_   

    ' Output the new property values.  
    Wscript.Echo " "  
    Wscript.Echo "Values after change:  "  
    Wscript.Echo "--------------------- "  
    Wscript.Echo "Advertisement Name:             " & advertisementToModify.AdvertisementName  
    Wscript.Echo "Advertisement Flags (integer):  " & advertisementToModify.AdvertFlags  

End Sub  

```  

```c#  

public void SetWOLOnAdvertisment(WqlConnectionManager connection,  
                                 string existingAdvertisementID)  
{  
    // Define a constant with the hexadecimal value for WAKE_ON_LAN_ENABLED.   
    const Int32 WAKE_ON_LAN_ENABLED = 0x00400000;  

    try  
    {  
        // Get the specific advertisement instance to modify.   
        IResultObject advertisementToModify = connection.GetInstance(@"SMS_Advertisement.AdvertisementID='" + existingAdvertisementID + "'");  

        // List the existing property values.  
        Console.WriteLine();  
        Console.WriteLine("Values before change:");  
        Console.WriteLine("_____________________");  
        Console.WriteLine("Advertisement Name:            " + advertisementToModify["AdvertisementName"].StringValue);  
        Console.WriteLine("Advertisement Flags (integer): " + advertisementToModify["AdvertFlags"].IntegerValue);  

        // Modify the AdvertFlags value to include the WAKE_ON_LAN_ENABLED value.  
        advertisementToModify["AdvertFlags"].IntegerValue = advertisementToModify["AdvertFlags"].IntegerValue | WAKE_ON_LAN_ENABLED;  

        // Save the advertisement with the new value.  
        advertisementToModify.Put();  

        // Reload the advertisement to verify the change.  
        advertisementToModify.Get();  

        // List the existing (modified) property values.  
        Console.WriteLine();  
        Console.WriteLine("Values after change:");  
        Console.WriteLine("_____________________");  
        Console.WriteLine("Advertisement Name:            " + advertisementToModify["AdvertisementName"].StringValue);  
        Console.WriteLine("Advertisement Flags (integer): " + advertisementToModify["AdvertFlags"].IntegerValue);  
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
|`connection`<br /><br /> `swebemServices`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](/windows/win32/wmisdk/swbemservices)|A valid connection to the SMS Provider.|  
|`existingAdvertisementID`|-   Managed: `String`<br />-   VBScript: `String`|The ID of the advertisment.|  

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
 [About deployments](about-software-distribution-deployments.md)
 [Software distribution overview](software-distribution-overview.md)
