---
title: "Add an OS Install Package"
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
ms.assetid: 3410a7c8-03b1-4c9e-874a-05324fcb569esearchScope: - ConfigMgr SDK
caps.latest.revision: 9
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Add an Operating System Install Package in Configuration Manager
You add an operating system install package to System Center Configuration Manager by creating and populating an instance of [SMS_OperatingSystemInstallPackage](../../develop/reference/osd/sms_operatingsysteminstallpackage-server-wmi-class.md).  

### To add an operating system install package  

1.  Set up a connection to the SMS Provider. For more information, see [About the SMS Provider in Configuration Manager](../../develop/core/understand/about-the-sms-provider-in-configuration-manager.md).  

2.  Create an instance of [SMS_OperatingSystemInstallPackage](../../develop/reference/osd/sms_operatingsysteminstallpackage-server-wmi-class.md).  

3.  Set at least the *Name*, *PkgSourceFlag*, and *PkgSourcePath* properties.  

4.  Commit the changes.  

## Example  
 The following example method adds an operating system install package.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Sub AddOSInstallPackage(connection, name, description, path)  

    Dim osInstallPackage  

    Set osInstallPackage = connection.Get("SMS_OperatingSystemInstallPackage").SpawnInstance_()  
    ' Populate the new package properties.  
    osInstallPackage.Name = name  
    osInstallPackage.Description = description  

    osInstallPackage.PkgSourceFlag=2  
    osInstallPackage.PkgSourcePath = path  

    ' Write the package.  
    osInstallPackage.Put_  

End Sub  
```  

```c#  
public void AddOSInstallPackage(  
    WqlConnectionManager connection,   
    string name,   
    string description,   
    string path)  
{  
    try  
    {  
        // Create new operating system image package object.  
        IResultObject osInstallPackage = connection.CreateInstance("SMS_OperatingSystemInstallPackage");  

        // Populate operating system package properties.  
        osInstallPackage["Name"].StringValue = name;  
        osInstallPackage["Description"].StringValue = description;  
        osInstallPackage["PkgSourceFlag"].IntegerValue = (int)PackageSourceFlag.StorageDirect;  
        osInstallPackage["PkgSourcePath"].StringValue = path;  

        // Save operating system package.  
        osInstallPackage.Put();  
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
|`name`|-   Managed: `String`<br />-   VBScript: `String`|Name for the new operating system image package.|  
|`description`|-   Managed: `String`<br />-   VBScript: `String`|Description for the operating system image package.|  
|`path`|-   Managed: `Integer`<br />-   VBScript: `Integer`|Universal Naming Convention (UNC) path to the image Windows Image (WIM) file.|  

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
 [How to Assign a Package to a Distribution Point](../../develop/core/servers/configure/how-to-assign-a-package-to-a-distribution-point.md)   
 [Operating System Deployment Image Management](../../develop/osd/operating-system-deployment-image-management.md)
