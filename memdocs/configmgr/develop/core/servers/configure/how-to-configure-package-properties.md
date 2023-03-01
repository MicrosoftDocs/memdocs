---
description: Learn how the following example shows how to configure the properties of an existing package, in Configuration Manager, by using the SMS_Package class.
title: Configure Package Properties
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: 60d90c19-2810-4f10-860f-aa3087f35b03
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# How to Configure Package Properties
The following example shows how to configure the properties of an existing package, in Configuration Manager, by using the `SMS_Package` class.  

### To configure an existing package  

1.  Set up a connection to the SMS Provider.  

2.  Load the existing package object by using `SMS_Package` class.  

3.  Populate any package properties (this example uses package description).  

4.  Save the package and the new package properties.  

## Example  
 The following example method configures package properties for software distribution.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../../develop/core/understand/calling-code-snippets.md).  

```vbs  

Sub ConfigurePackageProperties(connection, existingPackageID, newPackageDescription)  

    ' Get the specific package object.     Dim packageToConfigure  
    Set packageToConfigure = connection.Get("SMS_Package.PackageID='" & existingPackageID & "'")  

    ' Replace the existing package property (in this case the package description).  
    packageToConfigure.Description = newPackageDescription  

    ' Save the package with the modified properties.  
    packageToConfigure.Put_  

    ' Output package ID and package name.  
    wscript.echo "Configured Package "    
    wscript.echo "Package ID:        "  & packageToConfigure.PackageID  
    wscript.echo "Package Name:      "  & packageToConfigure.Name  

End Sub  

```  

```c#  

public void ConfigurePackageProperties(WqlConnectionManager connection, string existingPackageID, string newPackageDescription)  
{  
    try  
    {  
        // Get specific package instance to modify.  
        IResultObject packageToConfigure = connection.GetInstance(@"SMS_Package.PackageID='" + existingPackageID + "'");  

        // Replace the existing package property with the new value (in this case the package description).  
        packageToConfigure["Description"].StringValue = newPackageDescription;  

        // Save package and modified package properties.  
        packageToConfigure.Put();  

        // Output package ID and package name.  
        Console.WriteLine("Configured Package ");  
        Console.WriteLine("Package ID:        " + packageToConfigure["PackageID"].StringValue);  
        Console.WriteLine("Package Name:      " + packageToConfigure["Name"].StringValue);  
    }  

    catch (SmsException ex)  
    {  
        Console.WriteLine("Failed to configure package. Error: " + ex.Message);  
        throw;  
    }  
}  

```  

 The example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`connection`<br /><br /> `swbemServices`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](/windows/win32/wmisdk/swbemservices)|A valid connection to the SMS Provider.|  
|`existingPackageID`|-   Managed: `String`<br />-   VBScript: `String`|The ID of the existing package.|  
|`newPackageDescription`|-   Managed: `String`<br />-   VBScript: `String`|The description for the new package.|  

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
 [SMS_SCI_Component Server WMI Class](../../../../develop/reference/core/servers/configure/sms_sci_component-server-wmi-class.md)
