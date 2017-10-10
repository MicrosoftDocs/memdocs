---
title: "Allow Reboots Outside of a Maintenance Window"
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
ms.assetid: c2f7999b-533d-493f-b2b4-079b25c36f2dsearchScope: - ConfigMgr SDK
caps.latest.revision: 10
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Configure a Advertisement to Allow Reboots Outside of a Maintenance Window
The following example shows how to configure an advertisement to allow reboots outside of a maintenance window by using the `SMS_Advertisement` class and the `AdvertFlags` class property in System Center Configuration Manager.  

### To configure an advertisement to allow reboots outside of a maintenance window  

1.  Set up a connection to the SMS Provider.  

2.  Load an existing advertisement object using the `SMS_Advertisement` class.  

3.  Modify the `AdvertFlags` property using the hexadecimal value for `REBOOT_OUTSIDE_OF_MAINTENANCE_WINDOW`.  

4.  Save the modified advertisement and properties.  

## Example  
 The following example method configures an existing advertisement to allow reboots outside of a maintenance window.  

> [!IMPORTANT]
>  The hexadecimal values that define the `AdvertFlags` property are listed in the `SMS_Advertisement` reference material.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../../develop/core/understand/calling-code-snippets.md).  

```vbs  

Sub ModifyAdvertisementToRebootOutsideOfMaintenanceWindows(connection, existingAdvertisementID)  

    ' Define a constant with the hexadecimal value for the REBOOT_OUTSIDE_OF_MAINTENANCE_WINDOWS.   
    Const REBOOT_OUTSIDE_OF_MAINTENANCE_WINDOWS = &H00200000  
    Dim advertisementToModify  
    ' Get the specific advertisement instance to modify.   
    Set advertisementToModify = connection.Get("SMS_Advertisement.AdvertisementID='" & existingAdvertisementID & "'")  

    ' List the existing property values.  
    Wscript.Echo " "  
    Wscript.Echo "Values before change: "  
    Wscript.Echo "--------------------- "  
    Wscript.Echo "Advertisement Name:             " & advertisementToModify.AdvertisementName  
    Wscript.Echo "Advertisement Flags (integer):  " & advertisementToModify.AdvertFlags  

    ' Set the new property value.  
    advertisementToModify.AdvertFlags = advertisementToModify.AdvertFlags OR REBOOT_OUTSIDE_OF_MAINTENANCE_WINDOWS  

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

public void ModifySWDAdvertisementToRebootOutsideOfMaintenanceWindows(WqlConnectionManager connection,   
                                                                  string existingAdvertisementID)  
{  
    // Define a constant with the hexadecimal value for REBOOT_OUTSIDE_OF_MAINTENANCE_WINDOWS.   
    const Int32 REBOOT_OUTSIDE_OF_MAINTENANCE_WINDOWS = 0x00200000;  

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

        // Modify the AdvertFlags value to include the REBOOT_OUTSIDE_OF_MAINTENANCE_WINDOWS value.  
        advertisementToModify["AdvertFlags"].IntegerValue = advertisementToModify["AdvertFlags"].IntegerValue | REBOOT_OUTSIDE_OF_MAINTENANCE_WINDOWS;  

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
|`connection`<br /><br /> `swbemServices`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](https://msdn.microsoft.com/library/aa393854.aspx)|A valid connection to the SMS Provider.|  
|`existingAdvertisementID`|-   Managed: `String`<br />-   VBScript: `String`|The ID of the advertisement to modify.|  

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
