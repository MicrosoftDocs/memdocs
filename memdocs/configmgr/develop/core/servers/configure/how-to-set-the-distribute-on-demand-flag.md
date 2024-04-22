---
title: Set the Distribute on Demand Flag
titleSuffix: Configuration Manager
description: The following example shows how to set the "distribute on demand" flag property of an existing package by using the SMS_Package Server WMI Class class in Configuration Manager.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: how-to
ms.assetid: 0b87554c-cfd2-4f26-822d-b5b42d3d5bd0
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# How to Set the Distribute on Demand Flag
The following example shows how to set the "distribute on demand" flag property of an existing package by using the [SMS_Package Server WMI Class](../../../../develop/reference/core/servers/configure/sms_package-server-wmi-class.md) class in Configuration Manager.  

### To set the distribute on demand flag  

1.  Set up a connection to the SMS Provider. For more information, see [SMS Provider fundamentals](../../understand/sms-provider-fundamentals.md).  

2.  Load the existing package object by using [SMS_Package Server WMI Class](../../../../develop/reference/core/servers/configure/sms_package-server-wmi-class.md) class.  

3.  Populate the package flag property.  

4.  Save the package and the new package properties.  

## Example  
 The following example method sets the "distribute on demand" flag for a package.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../../develop/core/understand/calling-code-snippets.md).  

```vbs  

Sub SetDistributeOnDemandFlag(connection,         _  
                              existingPackageID)  

    ' Define a constant with the hexadecimal value for the DISTRIBUTE_ON_DEMAND.   
    DISTRIBUTE_ON_DEMAND = &H40000000  

    ' Get the specific package instance to modify.   
    Set packageToModify = connection.Get("SMS_Package.PackageID='" & existingpackageID & "'")  

    ' List the existing property values.  
    Wscript.Echo " "  
    Wscript.Echo "Values before change: "  
    Wscript.Echo "--------------------- "  
    Wscript.Echo "Package Name:            " & packageToModify.Name  
    Wscript.Echo "Package Flags (integer): " & packageToModify.PkgFlags  

    ' Set the new property value.  
    packageToModify.PkgFlags = packageToModify.PkgFlags OR DISTRIBUTE_ON_DEMAND  

    ' Save the package.  
    packageToModify.Put_   

    ' Output the new property values.  
    Wscript.Echo " "  
    Wscript.Echo "Values after change:  "  
    Wscript.Echo "--------------------- "  
    Wscript.Echo "Package Name:             " & packageToModify.Name  
    Wscript.Echo "Package Flags (integer):  " & packageToModify.PkgFlags  

End Sub  

```  

```c#  

public void SetDistributeOnDemandFlag(WqlConnectionManager connection,  
                                      string existingPackageID)  
{  
    // Define a constant with the hexadecimal value for DISTRIBUTE_ON_DEMAND.   
    const Int32 DISTRIBUTE_ON_DEMAND = 0x40000000;  

    try  
    {  
        // Get the specific package instance to modify.   
        IResultObject packageToModify = connection.GetInstance(@"SMS_Package.PackageID='" + existingPackageID + "'");  

        // List the existing property values.  
        Console.WriteLine();  
        Console.WriteLine("Values before change:");  
        Console.WriteLine("_____________________");  
        Console.WriteLine("Package Name:            " + packageToModify["Name"].StringValue);  
        Console.WriteLine("Package Flags (integer): " + packageToModify["PkgFlags"].IntegerValue);  

        // Modify the PkgFlags value to include the DISTRIBUTE_ON_DEMAND value.  
        packageToModify["PkgFlags"].IntegerValue = packageToModify["PkgFlags"].IntegerValue | DISTRIBUTE_ON_DEMAND;  

        // Save the package with the new value.  
        packageToModify.Put();  

        // Reload the package to verify the change.  
        packageToModify.Get();  

        // List the existing (modified) property values.  
        Console.WriteLine();  
        Console.WriteLine("Values after change:");  
        Console.WriteLine("_____________________");  
        Console.WriteLine("Package Name:            " + packageToModify["Name"].StringValue);  
        Console.WriteLine("Package Flags (integer): " + packageToModify["PkgFlags"].IntegerValue);  
    }  
    catch (SmsException ex)  
    {  
        Console.WriteLine("Failed to modify package. Error: " + ex.Message);  
        throw;  
    }  
}  

```  

 The example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`connection`<br /><br /> `swebemServices`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](/windows/win32/wmisdk/swbemservices)|A valid connection to the SMS Provider.|  
|`existingPackageID`|-   Managed: `String`<br />-   VBScript: `String`|The ID of the package.|  

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
 [Software distribution overview](software-distribution-overview.md)
 [Objects overview](../../understand/configuration-manager-objects-overview.md)
 [How to Connect to an SMS Provider in Configuration Manager by Using Managed Code](../../../../develop/core/understand/how-to-connect-to-an-sms-provider-by-using-managed-code.md)   
 [How to Connect to an SMS Provider in Configuration Manager by Using WMI](../../../../develop/core/understand/how-to-connect-to-an-sms-provider-in-configuration-manager-by-using-wmi.md)   
 [SMS_Package Server WMI Class](../../../../develop/reference/core/servers/configure/sms_package-server-wmi-class.md)
