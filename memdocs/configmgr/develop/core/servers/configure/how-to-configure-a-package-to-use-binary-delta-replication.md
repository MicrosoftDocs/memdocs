---
title: "Configure a Package to Use Binary Delta Replication"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: ffbb43e0-32f3-452a-9c94-9427b61817fa
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# How to Configure a Package to Use Binary Delta Replication
The following example shows how to configure an existing package to use binary delta replication, in Configuration Manager, by using the `SMS_Package` class and the `PkgFlags` class property.  

### To configure an existing package to use binary delta replication  

1.  Set up a connection to the SMS Provider.  

2.  Load the existing package object using `SMS_Package` class.  

3.  Modify the `PkgFlags` using the hexadecimal value for AP_USE_BINARY_DELTA_REP.  

4.  Save the package and the new package properties.  

## Example  
 The following example method configures an existing package to use binary delta replication.  

> [!IMPORTANT]
>  The hexadecimal values that define the `PkgFlags` property are listed in the `SMS_Package` class reference material.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../../develop/core/understand/calling-code-snippets.md).  

```vbs  

Sub ModifyPackageToUseBinaryDeltaReplication(connection, existingPackageID)  

    ' Define a constant with the hexadecimal value for AP_USE_BINARY_DELTA_REP.   
    Const AP_USE_BINARY_DELTA_REP = &H04000000  

    ' Get the specific advertisement instance to modify.     Dim packageToModify  
    Set packageToModify = connection.Get("SMS_Package.PackageID='" & existingPackageID & "'")  

    ' List the existing property values.  
    Wscript.Echo " "  
    Wscript.Echo "Values before change: "  
    Wscript.Echo "--------------------- "  
    Wscript.Echo "Package Name:   " & packageToModify.Name  
    Wscript.Echo "Package Flags:  " & packageToModify.PkgFlags  

    ' Set the new property value.  
    packageToModify.PkgFlags = packageToModify.PkgFlags OR AP_USE_BINARY_DELTA_REP  

    ' Save the advertisement.  
    packageToModify.Put_   

    ' Output the new property values.  
    Wscript.Echo " "  
    Wscript.Echo "Values after change: "  
    Wscript.Echo "--------------------- "  
    Wscript.Echo "Package Name:   " & packageToModify.Name  
    Wscript.Echo "Package Flags:  " & packageToModify.PkgFlags  

End Sub  

```  

```c#  

public void ModifyPackageToUseBinaryDeltaReplication(WqlConnectionManager connection, string existingPackageID)  
{  
    // Define a constant with the hexadecimal value for AP_USE_BINARY_DELTA_REP.   
    const Int32 AP_USE_BINARY_DELTA_REP = 0x04000000;  

    try  
    {  
        // Get the specific package instance to modify.   
        IResultObject packageToModify = connection.GetInstance(@"SMS_Package.PackageID='" + existingPackageID + "'");  

        // List the existing property values.  
        Console.WriteLine();  
        Console.WriteLine("Values before change:");  
        Console.WriteLine("_____________________");  
        Console.WriteLine("Package Name:  " + packageToModify["Name"].StringValue);  
        Console.WriteLine("Package Flags: " + packageToModify["PkgFlags"].IntegerValue);  

        // Modify the PkgFlags value to include the AP_USE_BINARY_DELTA_REP value.  
        packageToModify["PkgFlags"].IntegerValue = packageToModify["PkgFlags"].IntegerValue | AP_USE_BINARY_DELTA_REP;  

        // Save the package with the new value.  
        packageToModify.Put();  

        // Reload the package to verify the change.  
        packageToModify.Get();  

        // List the existing (modified) property values.  
        Console.WriteLine();  
        Console.WriteLine("Values after change:");  
        Console.WriteLine("_____________________");  
        Console.WriteLine("Package Name:  " + packageToModify["Name"].StringValue);  
        Console.WriteLine("Package Flags: " + packageToModify["PkgFlags"].IntegerValue);  
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
|`Connection`<br /><br /> `swbemServices`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](/windows/win32/wmisdk/swbemservices)|A valid connection to the SMS Provider.|  
|`existingPackageID`|-   Managed: `String`<br />-   VBScript: `String`|The ID of the existing package.|  

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

## .NET Framework Security  

## See Also  
 [Software distribution overview](software-distribution-overview.md)
 [SMS_SCI_Component Server WMI Class](../../../../develop/reference/core/servers/configure/sms_sci_component-server-wmi-class.md)
