---
title: "Create a Deployment Package"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: e32f4162-ec92-475f-8b39-f283de85d9e0
author: aczechowski
ms.author: aaroncz
manager: dougeby


---
# How to Create a Deployment Package
You create a software updates deployment package, in Configuration Manager, by creating an instance of the `SMS_SoftwareUpdatesPackage` class and populating the properties.  

### To create a software updates deployment package  

1.  Set up a connection to the SMS Provider.  

2.  Create the new package object by using the `SMS_SoftwareUpdatesPackage` class.  

3.  Populate the new package properties.  

4.  Save the new package and properties.  

## Example  
 The following example method shows how to create a software updates deployment package by using the `SMS_SoftwareUpdatesPackage` class and class properties.  

> [!NOTE]
>  The package location must be unique, and the updates must be available in the package source.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

 Example of the subroutine call in Visual Basic:  

```vbscript

Call CreateSUMDeploymentPackage(swbemServices,                  _  
                                "New SUM Deployment Package",   _  
                                "New SUM Package Description",  _  
                                2,                              _  
                                "\\ServerOne\SUM_TestPackageSource")  

```  

 Example of the method call in C#:  

```csharp

SUMSnippets.CreateSUMDeploymentPackage(WMIConnection,  
                                       "New SUM Deployment Package",  
                                       "New SUM Package Description",  
                                       2,  
                                       "\\\\ServerOne\\SUM_TestPackageSource");  
```  

```vbscript  

Sub CreateSUMDeploymentPackage(connection,                 _  
                               newPackageName,             _  
                               newPackageDescription,      _  
                               newPackageSourceFlag,       _  
                               newPackageSourcePath)  

    ' Create the new SUM package object.  
    Set newSUMDeploymentPackage = connection.Get("SMS_SoftwareUpdatesPackage").SpawnInstance_  

    ' Populate the new SUM package properties.  
    newSUMDeploymentPackage.Name = newPackageName  
    newSUMDeploymentPackage.Description = newPackageDescription  
    newSUMDeploymentPackage.PkgSourceFlag = newPackageSourceFlag  
    newSUMDeploymentPackage.PkgSourcePath = newPackageSourcePath             

    ' Save the new SUM package object and properties.  
    newSUMDeploymentPackage.Put_  

    ' Output the new SUM package name.  
    Wscript.Echo "Created the new SUM Deployment Package: " & newPackageName  

 End Sub  

```  

```csharp  

public void CreateSUMDeploymentPackage(WqlConnectionManager connection,  
                                       string newPackageName,  
                                       string newPackageDescription,  
                                       int newPackageSourceFlag,  
                                       string newPackageSourcePath)  

{  
    try  
    {  
        // Create the new SUM package object.  
        IResultObject newSUMDeploymentPackage = connection.CreateInstance("SMS_SoftwareUpdatesPackage");  

        // Populate the new SUM package properties.  
        newSUMDeploymentPackage["Name"].StringValue = newPackageName;  
        newSUMDeploymentPackage["Description"].StringValue = newPackageDescription;  
        newSUMDeploymentPackage["PkgSourceFlag"].IntegerValue = newPackageSourceFlag;  
        newSUMDeploymentPackage["PkgSourcePath"].StringValue = newPackageSourcePath;  

        // Save the new SUM package and new package properties.  
        newSUMDeploymentPackage.Put();  

        // Output the new SUM package name.  
        Console.WriteLine("Created the new SUM Deployment Package: " + newPackageName);  
    }  

    catch (SmsException ex)  
    {  
        Console.WriteLine("Failed to create the SUM Deployment Package. Error: " + ex.Message);  
        throw;  
    }  
}  

```  

 The example method has the following parameters:  

|Parameter|Type|Description|
|---------|----|-----------|
|`connection`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](/windows/win32/wmisdk/swbemservices)|A valid connection to the SMS Provider.|  
|`newDeploymentPackageName`|-   Managed: `String`<br />-   VBScript: `String`|The new deployment package name.|  
|`newDeploymentPackageDescription`|-   Managed: `String`<br />-   VBScript: `String`|The description for the new deployment package.|  
|`newPackageSourceFlag`|-   Managed: `Integer`<br />-   VBScript: `Integer`|The new package source flag.|  
|`newPackageSourcePath`|-   Managed: `String`<br />-   VBScript: `String`|The new package source path.<br /><br /> The package location must be unique and the updates must be available in the package source.|  

## Compiling the Code  
 This C# example requires:  

### Namespaces  
 System  

 System.Collections.Generic  

 System.Text  

 Microsoft.ConfigurationManagement.ManagementProvider  

 Microsoft.ConfigurationManagement.ManagementProvider.WqlQueryEngine  

### Assembly  
 adminui.wqlqueryengine  

 microsoft.configurationmanagement.managementprovider  

## Robust Programming  
 For more information about error handling, see [About Configuration Manager Errors](../../develop/core/understand/about-configuration-manager-errors.md).  

## .NET Framework Security  
 For more information about securing Configuration Manager applications, see [Configuration Manager role-based administration](../../develop/core/servers/configure/role-based-administration.md).  

## See Also  
 [About software update deployments](about-software-updates-deployments.md)
 [How to Assign a Package to a Distribution Point](../../develop/core/servers/configure/how-to-assign-a-package-to-a-distribution-point.md)   
 [SMS_SoftwareUpdatesPackage](../../develop/reference/sum/sms_softwareupdatespackage-server-wmi-class.md)