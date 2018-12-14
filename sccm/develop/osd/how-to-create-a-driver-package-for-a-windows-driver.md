---
title: "Create a Driver Package for a Windows Driver"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: c4e64b28-2159-4286-b1ef-4935c7e07e14
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# How to Create a Driver Package for a Windows Driver in Configuration Manager
You create a package for an operating system deployment driver, in System Center Configuration Manager, by creating a [SMS_DriverPackage Server WMI Class](../../develop/reference/osd/sms_driverpackage-server-wmi-class.md) object. To add a driver to the package, you call the [AddDriverContent Method in Class SMS_DriverPackage](../../develop/reference/osd/adddrivercontent-method-in-class-sms_driverpackage.md).  

 Driver packages are used to store the content associated with drivers. When creating a driver package, the source location should initially be an empty share that the SMS Provider has read and write access to. When a driver is added to a driver package, using `AddDriverContent`, the SMS Provider will copy the content from the driver source location to a subdirectory in the driver package share.  

 It is necessary to add the content that is associated with a driver to a driver package and assign it to a distribution point before the client can use it. You get the driver content from the [SMS_CIToContent Server WMI Class](../../develop/reference/sum/sms_citocontent-server-wmi-class.md) object where the `CI_ID` property matches the driver identifier.  

> [!NOTE]
>  It is possible for multiple drivers to share the same content. This typically happens when there are multiple .inf files in the same directory.  

 `AddDriverContent` can be used to add multiple drivers to a package simultaneously. To do this, add multiple content IDs. The `bRefreshDPs` parameter should be set to `false` if another call will be made. This ensures the package is only updated on the distribution point once.  

 When you call `AddDriverContent`, you specify a set of package source locations. Typically this is the [SMS_Driver Server WMI Class](../../develop/reference/osd/sms_driver-server-wmi-class.md) object `ContentSourcePath` property, but it can be overridden if the provider does not have access to the original source location.  

### To create a driver package and add driver content  

1.  Set up a connection to the SMS Provider. For more information, see [About the SMS Provider in Configuration Manager](../../develop/core/understand/about-the-sms-provider-in-configuration-manager.md).  

2.  Create an [SMS_DriverPackage](../../develop/reference/osd/sms_driverpackage-server-wmi-class.md) object.  

3.  Set the `PkgSourceFlag` property of the `SMS_DriverPackage` object to `2` (Storage Direct).  

4.  Commit the `SMS_DriverPackage` object.  

5.  Get the `SMS_DriverPackage` object.  

6.  Put the list of drivers that you want to add to the package in the [AddDriverContent](../../develop/reference/osd/adddrivercontent-method-in-class-sms_driverpackage.md) method `ContentIDs` in parameter.  

7.  Put the list of driver content source paths in the `AddDriverContent` method `ContentSourcePath` in parameter.  

8.  Call the `AddDriverContent` method.  

9. Call the [RefreshPkgSource Method in Class SMS_DriverPackage](../../develop/reference/osd/refreshpkgsource-method-in-class-sms_driverpackage.md) to complete the operation.  

10. Assign the driver package to a distribution point. For more information, see [How to Assign a Package to a Distribution Point](../../develop/core/servers/configure/how-to-assign-a-package-to-a-distribution-point.md).  

## Example  
 The following example method creates a package for a supplied driver identifier, represented by the `CI_ID` property of the [SMS_Driver Server WMI Class](../../develop/reference/osd/sms_driver-server-wmi-class.md) object. The method also takes a new package name, description, and package source path as parameters.  

> [!NOTE]
>  The `packageSourcePath` parameter must be supplied as a Universal Naming Convention (UNC) network path, for example, \\\localhost\Drivers\ATIVideo\\.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Sub CreateDriverPackage(connection, driverId, newPackageName, newPackageDescription,  newPackageSourcePath)  

    Dim newPackage  
    Dim driver   
    Dim packageSources  
    Dim refreshDPs  
    Dim content   
    Dim path  
    Dim contentIds  
    Dim index  
    Dim item  

    ' Create the new driver package object.  
    Set newPackage = connection.Get("SMS_DriverPackage").SpawnInstance_  

    ' Populate the new package properties.  
    newPackage.Name = newPackageName  
    newPackage.Description = newPackageDescription  
    newPackage.PkgSourceFlag = 2 ' Storage direct  
    newPackage.PkgSourcePath = newPackageSourcePath  

    ' Save the package.  
    path=newPackage.Put_  

    ' Get the newly created package (Do this to call AddDriverContent).  
    Set newPackage=connection.Get(path)  

    ' Get the driver  
    Set driver = connection.Get("SMS_Driver.CI_ID=" & driverId )  

    ' Get the driver content.  
    Set content = connection.ExecQuery("Select * from SMS_CIToContent where CI_ID=" & driverId)  

    If content.Count = 0 Then  
        Wscript.Echo "No content found"  
        Exit Sub  
    End If  

    ' Create Array to hold driver content identifiers.  
    contentIds = Array()  
    ReDim contentIds(content.Count-1)  
    index = 0  

    For Each item In content           
        contentIds(index) = item.ContentID   
        index = index+1         
    Next  

    ' Create sources path Array.  
    packageSources = Array(driver.ContentSourcePath)  
    refreshDPs = False  

    ' Add the driver content.  
    Call newPackage.AddDriverContent(contentIds,packageSources,refreshDPs)  
    wscript.echo "Done"  

End Sub  
```  

```c#  
public void CreateDriverPackage(  
    WqlConnectionManager connection,   
    int driverId,   
    string newPackageName,   
    string newPackageDescription,   
    string newPackageSourcePath)  
{  
    try  
    {  
        if (Directory.Exists(newPackageSourcePath) == false)  
        {  
            throw new DirectoryNotFoundException("Package source path does not exist");  
        }  

        // Create new package object.  
        IResultObject newPackage = connection.CreateInstance("SMS_DriverPackage");  

        IResultObject driver = connection.GetInstance("SMS_Driver.CI_ID=" + driverId);  

        newPackage["Name"].StringValue = newPackageName;  
        newPackage["Description"].StringValue = newPackageDescription;  
        newPackage["PkgSourceFlag"].IntegerValue = (int)PackageSourceFlag.StorageDirect;  
        newPackage["PkgSourcePath"].StringValue = newPackageSourcePath;  

        // Save new package and new package properties.  
        newPackage.Put();  

        newPackage.Get();  

        // Get the content identifier.  
        List<int> contentIDs = new List<int>();  
        IResultObject content = connection.QueryProcessor.ExecuteQuery("Select * from SMS_CIToContent where CI_ID=" + driverId);  

        foreach (IResultObject ro in content)  
        {  
            contentIDs.Add(ro["ContentID"].IntegerValue);  
        }  

        // Get the package source.  
        List<string> packageSources = new List<string>();  
        packageSources.Add(driver["ContentSourcePath"].StringValue);  

        Dictionary<string, Object> inParams = new Dictionary<string, object>();  

        inParams.Add("bRefreshDPs", true);  
        inParams.Add("ContentIDs", contentIDs.ToArray());  
        inParams.Add("ContentSourcePath", packageSources.ToArray());  

        newPackage.ExecuteMethod("AddDriverContent", inParams);  
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
|`driverId`|-   Managed: `Integer`<br />-   VBScript: `Integer`|The driver identifier (`SMS_Driver.CI_ID`).|  
|`newPackageName`|-   Managed: `String`<br />-   VBScript: `String`|The name for the package.|  
|`newPackageDescription`|-   Managed: `String`<br />-   VBScript: `String`|A description for the new package.|  
|`newPackageSourcePath`|-   Managed: `String`<br />-   VBScript:  `String`|A valid UNC network path to the driver.|  

## Compiling the Code  
 This C# example requires:  

### Namespaces  
 System  

 System.Collections.Generic  

 System.Text  

 System.IO  

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
 [SMS_Driver Server WMI Class](../../develop/reference/osd/sms_driver-server-wmi-class.md)   
 [AddDriverContent Method in Class SMS_DriverPackage](../../develop/reference/osd/adddrivercontent-method-in-class-sms_driverpackage.md)
