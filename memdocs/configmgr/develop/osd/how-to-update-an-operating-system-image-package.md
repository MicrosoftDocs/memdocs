---
title: Update an OS Image Package
titleSuffix: Configuration Manager
description: Update an operating system using a Windows Image file that is associated with the operating system package in Configuration Manager.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: c24fa670-0424-4ba1-9ca0-53e005f0d50a
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# How to Update an Operating System Image Package in Configuration Manager
In Configuration Manager, you update the Windows Image (WIM) file that is associated with the operating system package by calling the image package's [SMS_ImagePackage](../../develop/reference/osd/sms_imagepackage-server-wmi-class.md) class instance [ReloadImageProperties](../../develop/reference/osd/reloadimageproperties-method-in-class-sms_imagepackage.md) method. The image is updated based on the location defined in the `pkgSourcePath` property.  

### To update an operating system image package  

1.  Set up a connection to the SMS Provider. For more information, see [SMS Provider fundamentals](../core/understand/sms-provider-fundamentals.md).  

2.  Get the `SMS_ImagePackage` class instance you want to update.  

3.  Call the `ReloadImageProperties` class instance method.  

4.  Commit the `SMS_ImagePackage` class instance.  

## Example  
 The following example updates an operating system image package.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Sub UpdateOSImage(connection,imagePackageID, sourcePath)  

    Dim imagePackage  

    ' Get the image.  
    set imagePackage = connection.Get("SMS_ImagePackage.PackageID='" & imagePackageID & "'")  

    ' Update the source.  
    imagePackage.PkgSourcePath=sourcePath  
    imagePackage.Put_  
    imagePackage.RefreshPkgSource   

End Sub  
```  

```c#  
public void UpdateOSImage(  
    WqlConnectionManager connection,   
    string imagePackageId,   
    string sourcePath)  
{  
    try  
    {  
        // Get the image package.  
        IResultObject imagePackage = connection.GetInstance(@"SMS_ImagePackage.PackageID='" + imagePackageId + "'");  

        // Update the location.  
        imagePackage["PkgSourcePath"].StringValue = sourcePath;  
        imagePackage.Put();  
        imagePackage.ExecuteMethod("RefreshPkgSource", null);  
    }  
    catch (SmsException e)  
    {  
        Console.WriteLine(e.Message);  
        throw;  
    }  
}  
```  

 The example method has the following parameters:  

|Parameter|Type|Description|
|-|-|-|
|`connection`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](/windows/win32/wmisdk/swbemservices)|A valid connection to the SMS Provider.|  
|`imagePackageID`|-   Managed: `String`<br />-   VBScript: `String`|The package image identifier. It is available from `SMS_ImagePackage. PackageID`.|  
|`sourcePath`|-   Managed: `String`<br />-   VBScript: `String`|The path to the image package source in Universal Naming Convention (UNC) format.|  

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
 For more information about securing Configuration Manager applications, see [Configuration Manager role-based administration](../../develop/core/servers/configure/role-based-administration.md).  

## See also

[About image management](about-operating-system-deployment-image-management.md)
