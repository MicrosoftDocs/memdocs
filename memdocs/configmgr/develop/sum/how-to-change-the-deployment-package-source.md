---
title: "Change the Deployment Package Source"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: d931362e-25f6-4316-ab95-32b5771f670c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# How to Change the Deployment Package Source
You change the deployment package source for a software updates deployment package, in Configuration Manager, by obtaining an instance of the [SMS_SoftwareUpdatesPackage](../../develop/reference/sum/sms_softwareupdatespackage-server-wmi-class.md) class and by using the [ValidateNewPackageSource](../../develop/reference/sum/validatenewpackagesource-method-in-class-sms_softwareupdatespackage.md) method.  

> [!NOTE]
>  The package source for most other types of packages can be changed in the console. However, this option is not available for software updates packages.  

### To change the deployment package source  

1.  Set up a connection to the SMS Provider.  

2.  Obtain an existing package object by using the `SMS_SoftwareUpdatesPackage` class.  

3.  Verify the package source by using the `ValidateNewPackageSource` method.  

4.  Change the package source for an existing software updates deployment package by changing the `PkgSourcePath` property of the package.  

## Example  
 The following example method shows how to change the deployment package source for a software updates deployment package by using the `SMS_SoftwareUpdatesPackage` class and the `ValidateNewPackageSource` method.  

> [!NOTE]
>  All of the updates available in the old package source must be available in the new package source (the content source path, passed in as the `newPackageSourceLocation` variable in the below scripts).  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

 Example of the subroutine call in Visual Basic:  

```vbscript

' PREWORK FOR ChangeDeploymentPackageSource  

' Define the new package location to validate (package location must be UNC).  
newPackageSourceLocation = "\\SMSSERVER\source1"  

Call ChangeDeploymentPackageSource(swbemServices,             _  
                                   "ABC00003",                _  
                                   newPackageSourceLocation)  

```  

 Example of the method call in C#:  

```csharp

//PREWORK FOR ChangeDeploymentPackageSource.  

// Define the new package location to validate (package location must be UNC).  
string newPackageSourceLocation = "\\\\SMSSERVER\\source1";  

// Load the validateNewPackageSource parameters into an object to pass to the method.  
Dictionary<string, object> validateNewPackageSourceParameters = new Dictionary<string, object>();  
validateNewPackageSourceParameters.Add("PackageSource", newPackageSourceLocation);  

//The method call.  
SUMSnippets.ChangeDeploymentPackageSource(WMIConnection,  
                                          "ABC00003",  
                                          validateNewPackageSourceParameters,  
                                          newPackageSourceLocation);  

```  

```vbscript  

Sub ChangeDeploymentPackageSource(connection,                   _  
                                  existingSUMPackageID,         _  
                                  newDeploymentPackageLocation)   

    On Error Resume Next  

    ' Get an existing SUM Deployment Package to change.  
    Set existingSUMDeploymentPackage = connection.Get("SMS_SoftwareUpdatesPackage.PackageID='" & existingSUMPackageID & "'")    

    ' Check the package source for the existing SUM Deployment Package using the ValidateNewPackageSource method.  
    existingSUMDeploymentPackage.ValidateNewPackageSource(newDeploymentPackageLocation)  

    ' Check the error information from the SWBemLasError object to determine success or failure of the ValidateNewPackageSource method.  
    If Err.Number = 0 Then  

        ' Output a success message if the new package location is valid.  
        Wscript.Echo "The new location of the SUM deployment package validated. "  
        Wscript.Echo "Updating the SUM deployment package with the new package location.  "  

       ' Update the StoredPkgPath property of the existing deployment package   
       ' with the new source location if the package location is valid.  
       existingSUMDeploymentPackage.PkgSourcePath = newDeploymentPackageLocation  

       ' Save the updated package deployment package.  
       existingSUMDeploymentPackage.Put_  

    Else  

        ' Output a failure message if the new deployment package location is not valid.  
        Wscript.Echo "The new location of the SUM deployment package failed to validate. "  

    End If       

 End Sub  

```  

```csharp 

public void ChangeDeploymentPackageSource(WqlConnectionManager connection,  
                                          string existingSUMPackageId,  
                                          Dictionary<string, object> validateNewPackageSourceParameters,  
                                          string newPackageSource)  
{  
    try  
    {  
        // Get the specific SUM Deployment Package to change.  
        IResultObject existingSUMDeploymentPackage = connection.GetInstance(@"SMS_SoftwareUpdatesPackage.PackageId='" + existingSUMPackageId + "'");  

        // Validate the existing SUM Deployment Package content using the ValidateContent method.  
        // Note: The method will throw an exception, if the package source does not validate.   
        existingSUMDeploymentPackage.ExecuteMethod("ValidateNewPackageSource", validateNewPackageSourceParameters);  

        // Output a success message if the new package location is valid.  
        Console.WriteLine("The new location of the SUM deployment package validated.  ");  

        // Update the PkgSourcePath property of the existing deployment package with the new source location.  
        existingSUMDeploymentPackage["PkgSourcePath"].StringValue = newPackageSource;  

        // Save the package properties.  
        existingSUMDeploymentPackage.Put();  

        // Output a success message that the package location was updated.  
        Console.WriteLine("Updated the SUM deployment package with the new package location.  ");  
    }  
    catch (SmsException ex)  
    {  
        Console.WriteLine("Failed to validate the new package source.");  
        Console.WriteLine("Failed to update the SUM deployment package.");   
        Console.WriteLine("Error: " + ex.Message);         
        throw;  
    }  
}  

```  

 The example method has the following parameters:  

|Parameter|Type|Description|
|---------|----|-----------| 
|`connection`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](/windows/win32/wmisdk/swbemservices)|A valid connection to the SMS Provider.|  
|`existingSUMPackageID`|-   Managed: `String`<br />-   VBScript: `String`|The package ID for an existing software updates deployment package.|  
|`validateNewPackageSource`|-   Managed: `dictionary` object|The `validateNewPackageSource` is a dictionary object containing the parameters that the `ValidateNewPackageSource` method requires.<br /><br /> `PackageSource`|  
|`newPackageSourceLocation`|-   Managed: `String`<br />-   VBScript: `String`|The new deployment package source location. The source path must be a Universal Naming Convention (UNC) path. All of the updates available in the old package source must be available in the new package source.|  

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
 [SMS_SoftwareUpdatesPackage](../../develop/reference/sum/sms_softwareupdatespackage-server-wmi-class.md)   
 [ValidateNewPackageSource Method in Class SMS_SoftwareUpdatesPackage](../../develop/reference/sum/validatenewpackagesource-method-in-class-sms_softwareupdatespackage.md)
