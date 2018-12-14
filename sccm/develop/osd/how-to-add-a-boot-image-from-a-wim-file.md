---
title: "Add a Boot Image from a WIM File"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: c995b2e6-c364-4d59-8bc7-d8ef3596a0fd
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# How to Add a Boot Image from a WIM File in Configuration Manager
You add a boot image from a Windows Image (WIM) file to System Center Configuration Manager by creating an instance of [SMS_BootImagePackage](../../develop/reference/osd/sms_bootimagepackage-server-wmi-class.md). The property ImagePath must be set to the Universal Naming Convention (UNC) path to the WIM file. The property ImageIndex is the index to the required image within the WIM file.  

 If the boot image requires Windows drivers, you specify them in the `ReferencedDrivers` property, which is an array of [SMS_Driver_Details](../../develop/reference/osd/sms_driver_details-server-wmi-class.md).  

> [!NOTE]
>  When the boot image is updated, for example, when a System Center Configuration Manager binary or boot image property is changed, the boot image must be updated by calling the [SMS_BootImagePackage](../../develop/reference/osd/sms_bootimagepackage-server-wmi-class.md) class [RefreshPkgSource](../../develop/reference/osd/refreshpkgsource-method-in-class-sms_bootimagepackage.md) method.  

### To add a boot image from a WIM file  

1.  Set up a connection to the SMS Provider. For more information, see [About the SMS Provider in Configuration Manager](../../develop/core/understand/about-the-sms-provider-in-configuration-manager.md).  

2.  Create an instance of SMS_BootImagePackage.  

3.  Set at least the Name, ImagePath, and ImageIndex properties.  

4.  Commit the changes.  

## Example  
 The following example method adds a boot image from a WIM file.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Sub AddBootImagePackage(connection, name, description, pathToWim)  

    Dim bootImagePackage   

    Set bootImagePackage = connection.Get("SMS_BootImagePackage").SpawnInstance_()  
    ' Populate the new package properties.  
    bootImagePackage.Name = name  
    bootImagePackage.Description = description  

    bootImagePackage.ImagePath = pathToWim  'UNC path to WIM file.  
    bootImagePackage.ImageIndex = 1 ' Index into WIM file for image  

    bootImagePackage.Put_  

End Sub  
```  

```c#  
public void AddBootImage(  
    WqlConnectionManager connection,   
    string name,   
    string description,   
    string pathToWim)  
{  
    try  
    {  
        // Create new boot image package object.  
        IResultObject bootImagePackage = connection.CreateInstance("SMS_BootImagePackage");  

        // Populate new boot image package properties.  
        bootImagePackage["Name"].StringValue = name;  
        bootImagePackage["Description"].StringValue = description;  
        bootImagePackage["ImagePath"].StringValue = pathToWim; // UNC path required.  
        bootImagePackage["ImageIndex"].IntegerValue = 1; // Index into WIM file for image.  

        // Save new package and new package properties.  
        bootImagePackage.Put();  
    }  
    catch (SmsException e)  
    {  
        Console.WriteLine();  
        Console.WriteLine("Failed to create package. Error: " + e.Message);  
        throw;  
    }  
}  
```  

 The sample method has the following parameters:  

||||  
|-|-|-|  
|Parameter|Type|Description|  
|`connection`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](https://msdn.microsoft.com/library/aa393854.aspx)|A valid connection to the SMS Provider.|  
|`name`|-   Managed: `String`<br />-   VBScript: `String`|Name for the new boot image package.|  
|`description`|-   Managed: `String`<br />-   VBScript: `String`|Description for the boot image package.|  
|`pathToWIM`|-   Managed: `Integer`<br />-   VBScript: `Integer`|UNC path to the image.|  

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
 [How to add a Windows Driver to a Configuration Manager Boot Image Package](../../develop/osd/how-to-add-a-windows-driver-to-a-configuration-manager-boot-image-package.md)   
 [How to Assign a Package to a Distribution Point](../../develop/core/servers/configure/how-to-assign-a-package-to-a-distribution-point.md)   
 [Operating System Deployment Image Management](../../develop/osd/operating-system-deployment-image-management.md)
