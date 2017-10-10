---
title: "Add an OS Image Package"
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
ms.assetid: faa80d51-ac31-4802-b778-c26bc003ddb3searchScope: - ConfigMgr SDK
caps.latest.revision: 9
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Add an Operating System Image Package in Configuration Manager
In System Center Configuration Manager, you add an operating system image package by creating an instance of [SMS_ImagePackage](../../develop/reference/osd/sms_imagepackage-server-wmi-class.md) class. The path to the Windows Image (WIM) file is specified in the **PkgSourcePath** property as a Universal Naming Convention (UNC) path.  

### To create an operating system image package  

1.  Set up a connection to the SMS Provider. For more information, see [About the SMS Provider in Configuration Manager](../../develop/core/understand/about-the-sms-provider-in-configuration-manager.md).  

2.  Create an instance of SMS_ImagePackage.  

3.  Specify the path to the WIM file in **PkgSourcePath**.  

4.  Commit the SMS_ImagePackage class instance.  

## Example  
 The following example method creates an operating system package.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Sub AddOSImagePackage(connection, newImagePackageName, newImagePackageDescription, newImagePackageSourcePath)  

    Dim newImagePackage  

    Set newImagePackage = connection.Get("SMS_ImagePackage").SpawnInstance_()  
    ' Populate the new package properties.  
    newImagePackage.Name = newImagePackageName  
    newImagePackage.Description = newImagePackageDescription  
    newImagePackage.PkgSourceFlag = 2  
    newImagePackage.PkgSourcePath = newImagePackageSourcePath  

    ' Save the package.  
     newImagePackage.Put_  

End Sub  
```  

```c#  
public void AddOSImagePackage(  
    WqlConnectionManager connection,   
    string newImagePackageName,   
    string newImagePackageDescription,   
    string newImagePackageSourcePath)  
{  
    try  
    {  
        // Create new package object.  
        IResultObject newImagePackage = connection.CreateInstance("SMS_ImagePackage");  

        // Populate new package properties.  
        newImagePackage["Name"].StringValue = newImagePackageName;  
        newImagePackage["Description"].StringValue = newImagePackageDescription;  
        newImagePackage["PkgSourceFlag"].IntegerValue = (int)PackageSourceFlag.StorageDirect;  
        newImagePackage["PkgSourcePath"].StringValue = newImagePackageSourcePath;  

        // Save new package and new package properties.  
        newImagePackage.Put();  
    }  
    catch (SmsException e)  
    {  
        Console.WriteLine();  
        Console.WriteLine("Failed to create package. Error: " + e.Message);  
        throw;  
    }  
}  
```  

 The example method has the following parameters:  

||||  
|-|-|-|  
|Parameter|Type|Description|  
|`connection`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](https://msdn.microsoft.com/library/aa393854.aspx)|A valid connection to the SMS Provider.|  
|`newImagePackageName`|-   Managed: `String`<br />-   VBScript: `String`|The new image package name.|  
|`newImagePackageDescription`|-   Managed: `String`<br />-   VBScript: `String`|The new image package description|  
|`newImagePackageSourcePath`|-   Managed: `String`<br />-   VBScript: `String`|The UNC path to the WIM file.|  

## Compiling the Code  
 The C# example has the following compilation requirements:  

### Namespaces  
 System  

 System.Collections.Generic  

 System.Text  

 Microsoft.ConfigurationManagement.ManagementProvider  

 Microsoft.ConfigurationManagement.ManagementProvider.WqlQueryEngine  

### Assembly  
 microsoft.configurationmanagement.managementprovider  

 adminui.wqlqueryengine  

## Robust Programming  
 For more information about error handling, see [About Configuration Manager Errors](../../develop/core/understand/about-configuration-manager-errors.md).  

## .NET Framework Security  
 For more information about securing Configuration Manager applications, see [Securing Configuration Manager Applications](../../develop/core/understand/securing-configuration-manager-applications.md).  

## See Also  
 [Operating System Deployment Image Management](../../develop/osd/operating-system-deployment-image-management.md)   
 [How to Assign a Package to a Distribution Point](../../develop/core/servers/configure/how-to-assign-a-package-to-a-distribution-point.md)   
 [Operating System Deployment Image Management](../../develop/osd/operating-system-deployment-image-management.md)
