---
title: "Create a Package"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 2c295b3b-e23c-4084-ad4a-8bba328ef6fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# How to Create a Package
The following example shows how to create a package in System Center Configuration Manager by using the `SMS_Package` class and class properties.  

### To create a package  

1. Set up a connection to the SMS Provider.  

2. Create the new package object by using the `SMS_Package` class.  

3. Populate the new package properties.  

   > [!TIP]
   >  When you are creating a Virtual Application Package, you must set the `SMS_Package` properties to specific values. Instances of the `SMS_VirtualApp` class must reference instances of the `SMS_Package` class that use the properties described in the following table.  

    Virtual Application Package  

   | Property Name |       Property Value        |
   |---------------|-----------------------------|
   |  PackageType  |              7              |
   | PkgSourceFlag |              2              |
   | PkgSourcePath | \\\someserver\somesharepath |


4. Save the package.  

## Example  
 The following example method creates a new package and populates its properties for use in software distribution.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../../develop/core/understand/calling-code-snippets.md).  

```vbs  

Sub CreatePackage(connection, newPackageName, newPackageDescription, newPackageSourceFlag, newPackageSourcePath)  

    ' Create the new package object.     Dim newPackage  
    Set newPackage = connection.Get("SMS_Package").SpawnInstance_  

    ' Populate the new package properties.  
    newPackage.Name = newPackageName  
    newPackage.Description = newPackageDescription  
    newPackage.PkgSourceFlag = newPackageSourceFlag  
    newPackage.PkgSourcePath = newPackageSourcePath  

    ' Save the package.  
    newPackage.Put_  

    ' Output the new package name.  
    wscript.echo "Created package: "  & newPackageDescription  

End Sub  
```  

```c#  
public void CreatePackage(WqlConnectionManager connection, string newPackageName, string newPackageDescription, int newPackageSourceFlag, string newPackageSourcePath)  
{  
    try  
    {  
        // Create new package object.  
        IResultObject newPackage = connection.CreateInstance("SMS_Package");  

        // Populate new package properties.  
        newPackage["Name"].StringValue = newPackageName;  
        newPackage["Description"].StringValue = newPackageDescription;  
        newPackage["PkgSourceFlag"].IntegerValue = newPackageSourceFlag;  
        newPackage["PkgSourcePath"].StringValue = newPackageSourcePath;  

        // Save new package and new package properties.  
        newPackage.Put();  

        // Output new package name.  
        Console.WriteLine("Created package: " + newPackageName);  
    }  

    catch (SmsException ex)  
    {  
        Console.WriteLine("Failed to create package. Error: " + ex.Message);  
        throw;  
    }  
}  
```  

 The example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`connection`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](https://msdn.microsoft.com/library/aa393854.aspx)|A valid connection to the SMS Provider.|  
|`newPackageName`|-   Managed: `String`<br />-   VBScript: `String`|The name of the new package.|  
|`newPackageDescription`|-   Managed: `String`<br />-   VBScript: `String`|The description for the new package.|  
|`newPackageSourceFlag`|-   Managed: `Integer`<br />-   VBScript: `Integer`|The package source.|  
|`newPackageSourcePath`|-   Managed: `String`<br />-   VBScript: `String`|The path to the package source.|  

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
 [Software Distribution Packages](../../../../develop/core/servers/configure/software-distribution-packages.md)   
 [SMS_Package Server WMI Class](../../../../develop/reference/core/servers/configure/sms_package-server-wmi-class.md)   
 [PowerShell Cmdlet: New-CMPackage](http://go.microsoft.com/fwlink/?LinkId=309284)
