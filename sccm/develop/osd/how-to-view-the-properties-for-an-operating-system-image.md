---
title: "View the Properties for an OS Image"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 0d66813b-8579-48e7-a155-f90d4d7c4e10
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# How to View the Properties for an Operating System Image
In System Center Configuration Manager, you view the image properties for the Windows Image (WIM) file that is contained in an operating system package by calling the [SMS_ImagePackage](../../develop/reference/osd/sms_imagepackage-server-wmi-class.md) class instance [GetImageProperties](../../develop/reference/osd/getimageproperties-method-in-class-sms_imagepackage.md) method.  

 The image properties are available in XML format.  

### To view image properties  

1.  Set up a connection to the SMS Provider. For more information, see [About the SMS Provider in Configuration Manager](../../develop/core/understand/about-the-sms-provider-in-configuration-manager.md).  

2.  Get the `SMS_ImagePackage` class instance that you want to update.  

3.  Call the [GetImageProperties](../../develop/reference/osd/getimageproperties-method-in-class-sms_imagepackage.md) class instance method.  

4.  Access property XML by using the *ImageProperty* parameter.  

## Example  
 The following example displays the operating system image package property XML that defines the package.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Sub ViewOSImage(connection,imagePackageID)  

    Dim imagePackage  
    Dim inParam  
    Dim outParams  

    ' Get the image.  
    Set imagePackage = connection.Get("SMS_ImagePackage.PackageID='" & imagePackageID & "'")  

    ' Obtain an InParameters object specific  
    ' to the method.  
    Set inParam = imagePackage.Methods_("GetImageProperties"). _  
        inParameters.SpawnInstance_()  

    ' Add the input parameters.  
    inParam.Properties_.Item("SourceImagePath") =  imagePackage.PkgSourcePath  

    ' Execute the method.  
    Set outParams = connection.ExecMethod("SMS_ImagePackage", "GetImageProperties", inParam)  

    ' Display the image properties XML.  
    Wscript.echo "ImageProperty: " & outParams.ImageProperty  

End Sub  
```  

```c#  
public void ViewOSImage(  
    WqlConnectionManager connection,   
    string imagePackageId)  
{  
    try  
    {  
        IResultObject imagePackage = connection.GetInstance(@"SMS_ImagePackage.PackageID='" + imagePackageId + "'");  

        Dictionary<string, Object> inParams = new Dictionary<string, object>();  

        inParams.Add("SourceImagePath", imagePackage["PkgSourcePath"].StringValue);  
        IResultObject result = connection.ExecuteMethod("SMS_ImagePackage", "GetImageProperties", inParams);  

        Console.WriteLine(result["ImageProperty"].StringValue);  
    }  
    catch (SmsException e)  
    {  
        Console.WriteLine(e.Message);  
        throw;  
    }  
}  
```  

 The example method has the following parameters:  

||||  
|-|-|-|  
|Parameter|Type|Description|  
|`connection`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](https://msdn.microsoft.com/library/aa393854.aspx)|A valid connection to the SMS Provider.|  
|`imagePackageID`|-   Managed: `String`<br />-   VBScript: `String`|The package image identifier. It is available from `SMS_ImagePackage. PackageID`.|  

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
