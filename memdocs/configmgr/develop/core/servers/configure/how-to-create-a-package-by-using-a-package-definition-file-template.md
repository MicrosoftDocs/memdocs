---
title: "Create a Package Using a Package Definition File Template"
titleSuffix: "Configuration Manager"
description: The following example shows how to create a package and program by using a package definition file template in Configuration Manager.
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: 5dc3adf6-88e4-4fd1-bd33-ca868a586019
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# How to Create a Package by Using a Package Definition File Template
The following example shows how to create a package and program by using a package definition file template in Configuration Manager. The package definition file template contains the default values that are used to create `SMS_Package` and `SMS_Program` objects. The following example uses the `SMS_PDF_Package` class and the `GetPDFData` method to load the package definition file template information and to create a package and the related programs.  

### To create a package by using a package definition file template  

1.  Set up a connection to the SMS Provider.  

2.  Create the new package object by using the `SMS_PDF_Package` class.  

3.  Populate any additional package properties.  

4.  Load the program information and associate each program with the package.  

## Example  
 The following example method creates a new package by using a package definition file.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../../develop/core/understand/calling-code-snippets.md).  

```vbs  

Sub SWDCreatePDFPackage(connection, existingPDF_ID, newPackageSourceFlag, newPackageSourcePath)  
    ' The PDF_ID must be passed in.  
    ' The PDF_ID can be identified through the SMS_PDF_Package class.  

    Dim newPDFPackage  
    Dim returnCode  
    Dim newPackage  
    Dim newPackagePath  
    Dim packageID  
    Dim program  
    Dim arrayOfPrograms  

    ' Package Creation  
    ' ----------------       
    ' Create new SMS_PDF_Package instance.  
    Set newPDFPackage = connection.Get("SMS_PDF_Package")  

    ' Load the Package Definition File data using the GetPDFData method.  
    returnCode = newPDFPackage.GetPDFData(existingPDF_ID, newPackage, arrayOfPrograms)  

    ' Assign any additional package properties.  
    newPackage.PkgSourceFlag = newPackageSourceFlag  
    newPackage.PkgSourcePath = newPackageSourcePath  

    ' Save the package path and get the Package ID.  
    Set newPackagePath = newPackage.Put_  
    packageID = newPackagePath.Keys("PackageID")  

    ' Program Creation   
    ' -----------------      
    ' Enumerate through the program array and create the programs.  
    For Each program In arrayOfPrograms  
        program.PackageID = packageID  
        program.Put_  
    Next  

End Sub  
```  

 The example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`connection`|-   VBScript: [SWbemServices](/windows/win32/wmisdk/swbemservices)|A valid connection to the SMS Provider.|  
|`existingPDF_ID`|-   VBScript: `Integer`|ID of the package definition file.|  
|`newPackageSourceFlag`|-   VBScript: `Integer`|The package source.|  
|`newPackageSourcePath`|-   VBScript: `String`|The path to the package source.|  

## Robust Programming  
 For more information about error handling, see [About Configuration Manager Errors](../../../../develop/core/understand/about-configuration-manager-errors.md).  

## See Also  
 [Software distribution overview](software-distribution-overview.md)
 [SMS_SCI_Component Server WMI Class](../../../../develop/reference/core/servers/configure/sms_sci_component-server-wmi-class.md)
